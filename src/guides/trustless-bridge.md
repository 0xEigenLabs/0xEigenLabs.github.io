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

The user calls the `bridgeAsset` method on L1 smart contract, and deposits an amount of asset into the bridge contract, the `bridgeAsset` inserts a new leaf on the L1 Merkle tree and emits an event of the `bridgeAsset` paramters, the user watches the on-chain events and calculates the Merkle Proof p_1 locally, where:

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


**L2 -> L1**

* Deposit on L2:

The user calls the `bridgeAsset` method on L2 smart contract, and deposits an amount of asset into the bridge contract, the `bridgeAsset` inserts a new leaf on the L2 Merkle tree and emits an event of the `bridgeAsset` paramters, the user watches the on-chain events and calculates the Merkle Proof p_2 locally, where:

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
