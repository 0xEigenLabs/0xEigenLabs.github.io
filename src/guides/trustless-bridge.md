# Eigen Trustless Bridge

The bridge handles the asset briding between L1 and L2. 


<center>
<img src="/img/zkvm/zkvm-bridge.png">
</center>


Bridge.sol: A smart contract deployed on both L1 and L2, allowing the end user to deposit assets into, the smart contract mains a Merkle Tree, and each deposit will generate a Merkle Proof. The end user uses this Merkle Proof to claim its asset on L2/L1.

GlobalExitRoot.sol/GlobalExitRoot.sol:  maintain the valid Merkle Tree Root for L1/L2.

Verifier.sol: A smart contract verifying the Groth16 proof from L2.

Bridge-service:  A L1 smart contract client built on eigen-sdk-js. The Cardano and TON should integrate its `web3.js` into the bridge service.

eigen-sdk-js:  Like web3.js for Ethereum, it’s a Javascript SDK to interact with Ethereum Smart contract and L2 node(eigen-zeth). The Cardano and TON use it to communicate with L2 only.

eigen-zeth:  a customized zkEVM node.

## How it works
For Cardano/TON,  the address is derived from different elliptic curves from ETH.

**L1 -> L2**

* Deposit on L1:

insert a new leaf on the L1 Merkle tree, and the user gets the Merkle proof p_1.
Leaf := amount and public key(pk_l2)
Merkle proof := <leaf, merkle path>

* Claim on L2:

The user submits a transaction to eigen-zeth, which contains the Merkle proof p_1 as it’s calldata.

In the L2 bridge contract, it does:

1. [NOT NEED]Verify the public key(pk_l1) in the leaf,  is well mapped to the user’s L2 public key, pk_l2;

2. Verify the Merkle proof with the leaf;

3. If step 2 succeeds, Mint the L2 token to pk_l2 with `leaf.amount`; or deny the minting request.


**L2 -> L1**

insert a new leaf on the L2 Merkle tree, and the user gets the Merkle proof p_2.
Leaf := amount and public key(pk_l1)
Merkle proof := <leaf, merkle path>

In the L1 bridge contract, it does:

1. Verify the ZKP, the ZKP is to verify the correct execution of the L2 state tree. The state tree keeps track of the state transition in the L2 smart contract.  The problem is that we can not bind the ZKP with transactions/batch content right now.

2. Verify the Merkle proof with the leaf;

3. If step 2 succeeds, Unlock the L1 token to pk_l1 with `leaf.amount`; or deny the unlocking request.

