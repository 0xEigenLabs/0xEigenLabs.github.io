# Data Availability

In the context of blockchain, data availability refers to the assurance by network participants that the data published by users is faithfully proposed and stored in certain nodes of the network, and that these nodes can prove this property to other participants.

DAS: data availability sampling, is the new primitive that enables DA provider’s light nodes to verify DA efficiently. Instead of downloading all data, light nodes only download a tiny portion of each block.
Data Segmentation: The blockchain data is divided into small pieces or chunks.
Random Sampling by Nodes: Nodes in the network randomly select and download only some of these chunks rather than the entire data set.
Probabilistic Verification: By analyzing these samples, nodes can probabilistically verify the availability of the entire data set. If the sampled chunks are available and valid, it is highly likely that the rest of the data is also available and valid.

Since we use zkVM to support different L1 for scalalibity, like ETH, Cardano or TON. Some L1s provide cheap on-chain blob storage, and most of them not. Eigen zkVM integrates with some DA solution and enables developers to publish and verify their data.



