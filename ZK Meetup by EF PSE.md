# ZK Meetup by EF PSE

* binary operations expensive in circom groth16

* proof aggregation & recursion -- plonk

  * tornado cash v1 - every proof is verified on chain costs 100k gas
    * use proof agg to compress into 1
  * v2 - deposit expensive calculate snark firendly primitives which is evm unfriendly
    * can use keccak?
    * everybody knows merkle proof no private there
    * private is signature
    * verify sig * proof
  * v3 - prover cheaper by having a server that makes a proof of every elememnt in the tree then download by user
    * user agg merkle proof with spend part

* social network, bright id but privacy leak (need to share connections of social graph)

  * https://ethdos.xyz/
  * supply sig or proof
    * if sig.valid from user_x check
      * result score is 1
    * if proof valid
      * score = proof.score + 1
  * every peer gives their peers a signature which shows they are connected
    * everyone who is connected to x makes zkp which proves that they are connected then take score 1
      * Send proof to peers
        * those peers create proofs that they are 2 steps away then pass its proof to their peers
      * continue toll 6 degrees of separation https://en.wikipedia.org/wiki/Six_degrees_of_separation

  * issues
    * if X is a sybil then you lose
    * brightid uses different algo each other --> diffi to impl
    * 6 theory correct? hmm / random walks? hm.. too

* plonkish goals: aggregation toolbox
  * aggregate many circom plonk proofs inside a halo2 proof (similar to han0110 plonk-verifier)
  * to help semaphore, maci, zkporu, unirep scale...
  * nice hook
* plonkish new goal to new DSL
  * agg changes the landscape of DSL
  * new zkps should be written in many languages
  * agg toolbox is to connect many lang together
* agg -- more verifiable work
  * don't finish till finishing all
  * recursion is 100% of the proofs in side the one then you can continue to later



## Plonkish Arithmetization

* Custom Gates
* Lookup Arguments





## how to contribute to zkEVM

https://github.com/privacy-scaling-explorations/zkevm-specs