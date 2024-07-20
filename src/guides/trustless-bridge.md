# Eigen Trustless Bridge

The bridge handles the asset briding between L1 and L2. 


<center>
<img src="/img/zkvm/zkvm-bridge.png">
</center>


Bridge.sol: a smart contract deployed on both L1 and L2, allowing the end user to deposit assets into, the smart contract maintains a Merkle Tree, and each deposit will generate a Merkle Proof. The end user uses this Merkle Proof to claim its asset on L2/L1.

GlobalExitRoot.sol/GlobalExitRootL2.sol:  maintain the valid Merkle Tree Root for L1/L2.

Verifier.sol: a smart contract verifying the Groth16 proof from L2.

Bridge-service:  a L1 smart contract client built on eigen-sdk-js. The Cardano and TON should integrate its `web3.js` into the bridge service.

eigen-sdk-js:  like web3.js for Ethereum, it’s a Javascript SDK to interact with Ethereum Smart contract and L2 node(eigen-zeth). The Cardano and TON use it to communicate with L2 only.

eigen-zeth:  a customized zkEVM node.

For Cardano/TON account, the address is derived from different elliptic curves from ETH, so is the EC pairing scheme. 

|   | Signature Scheme | EC Pairings|
|---|---|---|
| Ethereum | ECDSA  | BN254  |
| Cadano  |  Ed25519 | BLS12381  | 
|  TON |  Ed25519 | BLS12381  | 

More details can be found on our [Medium](https://eigenlab.medium.com/ecdsa-vs-ed25519-7b31c9698831).


## How it works

**L1 -> L2**

* Deposit on L1:

The user calls the `bridgeAsset` method on L1 smart contract, and deposits an amount of asset into the bridge contract, the `bridgeAsset` inserts a new leaf on the L1 Merkle tree and emits an event of the `bridgeAsset` paramters, the user watches the onchain events and calculates the Merkle Proof p_1 locally, where:

```
Leaf := amount and public key(pk_l2)
Merkle Proof := <Leaf, Merkle path>
```
After deposit, the Bridge.sol contract will call the GlobalExitRoot.sol contract to update the new L1 exit merkle tree(EMT) root, thereby calculating the new global exit merkle tree(GEMT) root. The bridge service listens for events from the GlobalExitRoot.sol contract to get the new GEMT root. The new GEMT root is submitted to the GlobalExitRootL2.sol contract. The L2 bridge contract can get the GMT.

* Claim on L2:

The user submits a transaction to eigen-zeth, which contains the Merkle proof p_1 as it’s calldata.

In the L2 bridge contract, it does:

1. [NOT NEED]Verify the public key(pk_l1) in the leaf,  is well mapped to the user’s L2 public key, pk_l2;

2. The sequencer synchronizes the L1 EMT root and update the EMT manager on L2. 

3. Verify the Merkle proof with the leaf over the L1 EMT root;

4. If step 3 succeeds, Mint the L2 token to pk_l2 with `leaf.amount`; or deny the minting request.

**Detailed steps:**

1. The user calls deposit through the SDK. 
2. The SDK calls the bridgeAsset function of the Bridge contract with the following parameters:
    - destinationNetwork
    - destinationAddress
    - amount
    - tokenAddress
3. The Bridge contract interacts with the GlobalExitRoot contract. If the L2 does not have the corresponding token, a wrapped token will be created, and the amount of the original tokens will be transferred to the Bridge contract. The deposit is executed, generating a new L1EMTRoot. The parameters for the deposit are as follows:
    ```
    getLeafValue(
        _LEAF_TYPE_ASSET,
        originNetwork,
        originTokenAddress,
        destinationNetwork,
        destinationAddress,
        leafAmount,
        keccak256(metadata)
    )

    metadata = abi.encode(
        _safeName(token),
        _safeSymbol(token),
        _safeDecimals(token)
    );
    ```

4. The bridge-service listens to the Bridge contract. After detecting a BridgeEvent, it retrieves the L1 EMT root from the GlobalExitRoot. 

5. The bridge-service then updates the L2's GEMT (GlobalExitRootL2).

6. The user calls deposit_claim through the SDK, requiring the transaction hash of the deposit. 

7. The SDK obtains the merkle proof, L1 EMT root, and L2 EMT root from the bridge-service. 

8. The SDK then calls the claimAsset function of the Bridge contract with the following parameters:

    - smtProof
    - index
    - mainnetExitRoot, L1 EMT root
    - rollupExitRoot, L2 EMT root
    - originNetwork,
    - originTokenAddress,
    - destinationNetwork,
    - destinationAddress,
    - amount,
    - metadata,

9. The GlobalExitRoot contract calls the Verifier contract to verify the merkle proof. Upon successful verification, it transfers the funds to the destination address on L2.

**L2 -> L1**

* Deposit on L2:

The user calls the `bridgeAsset` method on L2 smart contract, and deposits an amount of asset into the bridge contract, the `bridgeAsset` inserts a new leaf on the L2 Merkle tree and emits an event of the `bridgeAsset` paramters, the user watches the onchain events and calculates the Merkle Proof p_2 locally, where:

```
Leaf := amount and public key(pk_l1)
Merkle Proof := <Leaf, merkle path>
```

After deposit, the Bridge.sol contract will call the GlobalExitRootL2.sol contract to update the new L2 EMT. The bridge service listens for events from the GlobalExitRootL2.sol contract to get the new rollup exit merkle tree root(REMT root). The new REMT root and the corresponding block number will be stored in the bridge service database. After each block is proved by the eigen-zeth node, the functions sequenceBatches and verifyBatches in the EigenZkVM contract will be called. Before calling verifyBatches, the REMT corresponding to this block will be obtained through the bridge service. After the verifyBatches function is successfully executed, the GEMT of the GlobalExitRoot.sol contract will be updated.

In the L1 bridge contract, it does:

1. Verify the ZKP, the ZKP is to verify the correct execution of the L2 state tree. The state tree keeps track of the state transition in the L2 smart contract.  The problem is that we can not bind the ZKP with transactions/batch content right now.

2. Verify the Merkle proof with the leaf;

3. If step 2 succeeds, Unlock the L1 token to pk_l1 with `leaf.amount`; or deny the unlocking request.

* Claim on L1:

The user submits a transaction to eigen-zeth, which contains the Merkle proof p_1 as it’s calldata.

In the L1 bridge contract, it does:

1. [NOT NEED]Verify the public key(pk_l2) in the leaf,  is well mapped to the user’s L1 public key, pk_l1;

2. The sequencer synchronizes the L2 EMT root and update the EMT manager on L1. 

3. Verify the Merkle proof with the leaf over the L2 EMT root;

4. If step 3 succeeds, Transfer the L1 token from Bridge.sol contract address to pk_l1 with `leaf.amount`; or deny the minting request.

**Detailed steps:**

1. The user calls withdraw through the SDK. 

2. The SDK calls the bridgeAsset function of the Bridge contract on L2 with the following parameters:
    - destinationNetwork
    - destinationAddress
    - amount
    - tokenAddress

3. The Bridge contract interacts with the GlobalExitRootL2 contract, destroys the user's tokens, and executes a deposit, generating a new L2EMTRoot. 

4. The bridge-service listens to the Bridge contract on L2. After detecting a BridgeEvent, it retrieves the L2EMT root from the GlobalExitRootL2 and stores it in the database.

5. Eigen-Zeth retrieves the GEMT from the GlobalExitRoot contract on L1 for each transaction. After obtaining the GEMT

6. Eigen-Zeth calls the sequence_batches function of the ZkVM with an array of the following structure:

    ```
    BatchData {
        transactions: rlp_vec,
        global_exit_root,
        timestamp: block.timestamp.as_u64(),
    };
    ```

7. Eigen-Zeth retrieves the L2 EMT root from the bridge-service. 

8. Eigen-Zeth then calls the verify_batches function of the ZkVM with the following parameters, where proof_data.proof refers to the ZKP proof:

    ```
    verify_batches(
        0,
        last_verified_block,
        last_verified_block + 1,
        zeth_last_rollup_exit_root,
        proof_data.post_state_root,
        proof_data.proof,
        proof_data.public_input,
    )
    ```

9. The ZkVM contract calls the Groth16Verifier contract to verify the ZKP proof. After successful verification

10. The ZkVM contract calls the GlobalExitRoot contract to update the GEMT.

11. The user calls withdraw_exit through the SDK and needs to provide the transaction hash of the withdraw.

12. The SDK obtains the merkle proof, L1 EMT root, and L2 EMT root from the bridge-service. 

13. The SDK then calls the ClaimAsset function of the Bridge contract on L2.
