=========================
PDBFT Consensus Algorithm
=========================

| The early public chain systems primarily adopted consensus mechanisms based on proof of work (PoW). Under this mechanism, hardware performance directly determines the computing power, that is, the ability to successfully generate blocks. A consensus algorithm based on PoW requires a significant amount of computing power, resulting in a lower TPS (transactions per second) throughput, such as the 3 to 7 TPS provided by Bitcoin. The PoW algorithm is also vulnerable to 51% attacks, so users are forced to wait for several block confirmations before a transaction is processed.

| In order to overcome these problems, PCHAIN adopted a new consensus mechanism - PDBFT which is based on proof of equity (PoE). In PDBFT, each validator needs to hold a certain number of tokens in advance to obtain voting rights, and consensus is reached by voting to generate new blocks. Compared with the more secure network environment of consortium blockchain, the validator in the public chain is more vulnerable to attack and may act maliciously. This is named a Byzantine node, displaying uncertain or unpredictable behavior. For example, it may propose illegitimate blocks, deliberately cast opposing votes, or send different votes to various nodes. Byzantine nodes may even work together in bad faith.

| These behaviors affect the consensus of the blockchain network and present a major problem for the public chain. Currently, modified PBFT-based algorithms are widely used in the industry, such as Hyperledger Fabric 0.6, IstanbulBFT, and Tendermint. Although the PBFT protocol can solve issues of Byzantine fault tolerance, the following problems restrict its application in large-scale public chains:

- PBFT assumes that the validator set remains unchanged, but in the public chain, the validator should be able to join and exit more freely.

- PBFT will not actively change the leader and will only do that in the event of a timeout. On one hand, the leader is more vulnerable to attacks. On the other, the leader may selectively package some transactions so that the others cannot be executed.

- In PBFT, votes of all validators need to be transmitted to all nodes through broadcasting, so the overall communication overhead is O(n2), which greatly limits its application in larger networks.

| After long-term research and development, the PCHAIN team proposed a new consensus protocol called PDBFT which can successfully solve the above problems, making it suitable for large-scale public chains. Main features of this consensus mechanism include:

- Regular replacement of validator set. This allows the validator to join and exit the mechanism more freely. Each validator can choose whether to participate in the validator set campaign for the next Epoch. All validators of the next Epoch are then determined through consensus. The new validator set takes effect after the current Epoch ends.

- Active change of the leader. This makes it more difficult to attack the leader. After each round of PDBFT consensus, the leader will be changed regardless if consensus is reached or need to move to another consensus round. The leader of the new consensus round is randomly generated based on the consensus information of the previous block and can be verified by other validators. Since the generation of the new leader depends only on the consensus of the previous block and the state of current consensus, no node knows the next leader in advance. Thus, the probability of a successful attack is greatly reduced.

- A reduction in the communication cost of broadcasting the votes from O(n2) to O(n). In contrast to voting by broadcasting to the whole network, each validator will send votes to the current leader. After receiving majority (2/3+) votes, the leader will aggregate them through the aggregate signature algorithm. The size of the aggregated signature is the same as that of a single signature, and each validator can verify whether majority nodes have voted correctly by verifying the aggregate signature. The leader will finally broadcast the aggregate to all validators, thus the communication overhead of the protocol is reduced to O(n). This greatly improves the extendibility of the protocol and makes large-scale applications possible.
