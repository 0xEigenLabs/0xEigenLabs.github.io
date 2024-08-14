# Sequencer

## What is a sequencer

A sequencer is a set of entities responsible for receiving Layer 2 transactions, determining their order, executing them, packaging blocks, and maintaining the Layer 2 state.

## Centralized sequencers

Centralized Sequencers are key components in some Layer 2 blockchain scaling solutions. Their primary role is to receive, order, and batch transactions before submitting them to the Layer 1 blockchain for final settlement. Most of them are implemented using consensus algorithms similar to POA.

Advantages: 

- Efficiency: Centralized control allows for rapid transaction processing and lower latency.
- Simplicity: Centralized Sequencers streamline coordination, especially in high-traffic situations.

Challenges:

- Single point of failure: A single point of failure contradicts the decentralization ethos of blockchain, potentially leading to system vulnerabilities.
- Censorship Potential: Centralized Sequencers could selectively delay or block transactions, threatening fairness and transparency.
- Monopoly Over MEV: Centralized Sequencers can monopolize Miner Extractable Value (MEV) by controlling transaction order. This centralization allows them to capture all MEV profits, leading to unfair advantages, profit concentration, and potential manipulation, which undermines blockchain decentralization.

## Eigen-Zeth's Decentralized Sequencers

Eigen Zeth uses ETH2 (Lighthouse + Reth) as its decentralized sequencers, meaning Eigen Zeth's sequencers are based on a PoS blockchain.

Lighthouse: Lighthouse is an Ethereum consensus client that connects to other Ethereum consensus clients to form a resilient and decentralized proof-of-stake blockchain. Lighthouse implements the Gasper algorithm, which is a combination of Casper FFG (Casper the Friendly Finality Gadget) and LMD-GHOST (Latest Message Driven - Greediest Heaviest Observed SubTree). This algorithm is used in Ethereum 2.0 (ETH2) to achieve Proof of Stake (PoS) consensus.

Reth: Reth is an Ethereum execution client written in Rust.

### Architecture

<center>
<img src="/img/zkvm/sequencer/sequencer-architecture.png">
</center>
