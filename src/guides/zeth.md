# Eigen Zeth

A "Type 0" zkEVM.

## Eigen Zeth Architecture

<center>
<img src="/img/zkvm/zeth/zeth-architecture.png">
</center>
As illustrated in the figure above, Eigen Zeth include these components:

- **Watcher**: Monitors and synchronizes blocks confirmed by the Layer 2 sequencer.
- **Proposer**: Packages a specified number of blocks into a batch in sequential order.
- **Settlement**: Generates a proof for the batched blocks and calls the settlement layer's verify function for final settlement.
- **Custom Eigen Reth Node**: A custom Layer 2 node based on Reth, designed to receive transactions, determine their order on Layer 2, and generate and confirm Layer 2 blocks.

## Transaction

### Transaction Lifecycle

<center>
<img src="/img/zkvm/zeth/transaction-lifecycle.png">
</center>
The transaction life cycle in the Eigen Network contains the following three phases:

1. **Pending**: The user submits a transaction to the L2 sequencer. The transaction enters the transaction pool and becomes Pending, waiting to be included in a block by the sequencer.
2. **Sequenced**: The sequencer packages the transaction into a block. At this stage, the transaction is confirmed on Layer 2, and the transactions in this block become Committed.
3. **Batching**: A certain number of Layer 2 blocks are packaged sequentially into a batch. The transactions in the batch enter the Batching state.
4. **Submitted**: Once the batch is complete, it is sent to the DA layer. The transactions in this batch are now Submitted.
5. **Finalized**: The Settlement component generates a proof for the batch and calls the Layer 1 Verify contract for final settlement. After verification and inclusion in Layer 1, these transactions become Finalized.

## Deployment

[Document](https://github.com/0xEigenLabs/eigen-prover?tab=readme-ov-file#server)
