# Week2 Assignment ZKU

#### 1. Rank the four hashes and provide explanations in four different aspects: gas cost, capacity, proof generation efficiency, and proof size.

When comparing the hash functions SHA256, MiMC, Poseidon, and Pedersen, the following ranking holds true in the various categories:

##### Gas Cost

* SHA256 < Poseidon < Pedersen < MiMC

- https://ethresear.ch/t/gas-and-circuit-constraint-benchmarks-of-binary-and-quinary-incremental-merkle-trees-using-the-poseidon-hash-function/7446/3

##### Capacity (the number of inputs it can take in circomlib templates)

* MiMC ~~ Poseidon > Pedersen > SHA256

- https://ethresear.ch/t/gas-and-circuit-constraint-benchmarks-of-binary-and-quinary-incremental-merkle-trees-using-the-poseidon-hash-function/7446/3
- https://eprint.iacr.org/2019/458.pdf

##### Proof generation efficiency

* SHA256 < Poseidon < Pedersen ~~ MiMC
* SHA256 is not efficient in zkSNARKS because it does lots of boolean operations whereas the circuit required for a zkCircuit is an arithmetic circuit.

- https://ethresear.ch/t/gas-and-circuit-constraint-benchmarks-of-binary-and-quinary-incremental-merkle-trees-using-the-poseidon-hash-function/7446/3
- https://z.cash/technology/jubjub/

##### Proof size

* SHA256 > MiMC > Poseidon ~~ Pedersen

- https://ethresear.ch/t/gas-and-circuit-constraint-benchmarks-of-binary-and-quinary-incremental-merkle-trees-using-the-poseidon-hash-function/7446/3
- https://z.cash/technology/jubjub/

#### 2. In `circuits/MerkleTree.circom`, complete the code for the following templates (feel free to add any helper templates for intermediate components and it’s ok to reference existing repos as long as their licenses permit):

https://github.com/Web3-Study-with-Sigrid-Jin/zku-cohort-4-week2/tree/master/Part1

#### 3. How is Tornado Cash Nova different from Tornado Cash Classic? What are the key upgrades/improvements and what changes in the technical design make these possible?

First, funds are directly linked to a given wallet address. There is no private note or key. Users can access their funds by connecting to the pool with the appropriate address. User can deposit/withdraw arbitrary amounts of ETH, before with Tornado Classic, the user to deposit/withdraw a fixed amount of a given token within each pool. 

Second, custody is either acquired by the act of depositing tokens into the pool or by registering in the pool and receiving shielded transfers from another address. In order to accomplish these things, a random area of bytes is computed using the Pedersen Hash, then sends the token and the 20 MiMC hash to the smart contract. The contract is then inserted into the Merkle Tree.

To process a withdrawal, the same area of bytes is splited into two seperate parts: the secret on one side and the nullifier on the other side. The nullifier is a public input that is sent on-chain to be checked with the smark contract and the Merkle tree data and prevents double spending.

Tornado Cash Nova uses Gnosis Chain as a Layer2, which allows for cheaper fees with fast transctions, and it as a L2 is much faster with dealing with Mainnet compared to 3 hours on Polygon.

#### 4. **What is the role of the relayers in the Tornado Cash protocols? Why are relayers needed?**

https://www.youtube.com/watch?v=BaFg4NF_ZOs

Relayers are from the essentials parts of Tornado Cash, they are recommended to be used in order to preserve privacy while paying gas fees to do ETH transfer transactions, because otherwise if user choose to connect with the wallet, this payment of gas fees can compromise the anonymity of the user. They are acting as a third party, for managing the entire withdrawing process.

#### 5. What is Semaphore? Explain in 4-8 sentences how it works.

It is a set of tools that forms a system that allows an authorized user to act on certain information without revealing any information about the user. It is a system that allows any user to signal their endorsement of an arbitrary string, revealing only that they have been previously approved to do so, and not their specific identity. In order for this process to take place, some proofs must be completed. It must be proved that the user is authorized to do the signaling and that they signal is unique, depending on the use case. This is done through smart contracts and circuits utilizing a Merkle Tree.

#### 6. How does Semaphore prevent double signing (or double withdrawal in the case of mixers)? Explain the mechanism in 4-8 sentences.

https://medium.com/coinmonks/to-mixers-and-beyond-presenting-semaphore-a-privacy-gadget-built-on-ethereum-4c8b00857c9b

A Semaphore has multiple mechanisms to prevent double signing or double withdrawal. First is the Merkle tree structure. If any transaction cannot be verified inside of the Merkle tree, then it must false, thus nullifying the possibility of a double sign. Furthermore, the user trying to authenticate is a registered user, meaning that they have a unique authorization token. This token can be used to track the users transactions and understand their true identity and where their tokens have been used.

The users register first their identity by doing an identity commitment, which is equal to the hash of the pk: the user's EdDSA public key, in: identity nullifier, it: identity trapdoor. And then proof the current merkle root, with the generated merkle root of the merkle path with the generated identity commitment.

Then users can do their first transaction safely with an external nullifier, and the contract accepts this transaction because that is the first signal. However, if the users tried to execute another transaction with the same en: external nullifier, the contract will reject it.

#### 7. A lot of applications have already been built based on derivations from Semaphore, such as for voting, survey or opinion, and authentication. Can you suggest two more ideas for ZK applications that can be built upon Semaphore?

Resale transaction verification, social media verification.

## ZK-EVM

* 한국어: https://medium.com/@dodive/%EB%B2%88%EC%97%AD%EC%9A%94%EC%95%BD-%EB%B9%84%ED%83%88%EB%A6%AD-%EB%B6%80%ED%85%8C%EB%A6%B0%EC%9D%98-the-different-types-of-zk-evms-d5ae61de9360

![img](https://miro.medium.com/max/700/0*yBXBhh6Fj-gzFhrZ)

![img](https://miro.medium.com/max/700/1*mItDUyyh6mTaq8iW2un0sw.png)

https://twitter.com/LuozhuZhang/status/1538166119785111552

https://immutablex.medium.com/ground-up-guide-zkevm-evm-compatibility-rollups-787b6e88108e

https://trapdoortech.medium.com/zkp-zkevm-a9b046789b4e
https://hackmd.io/Hy_nqH4yTOmjjS9nbOArgw#Links
https://immutablex.medium.com/ground-up-guide-zkevm-evm-compatibility-rollups-787b6e88108e 