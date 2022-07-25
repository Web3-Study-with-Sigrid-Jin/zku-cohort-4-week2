## Assignments

### Week 1 Bonus

* Matrix operations could also be used to verify that someone knows a solution to a [system of (linear) equations](https://en.wikipedia.org/wiki/System_of_linear_equations) without revealing the solution itself. In bonus/SystemOfEquations.circom, implement a general circuit that verifies an input x solves the system of equations Ax=b, where A and b are also signal inputs.
* Then run npm run test to prove that the solution to the following system of equations is x=15, y=17, z=19.
```
x + y + z = 51
x + 2y + 3z = 106
2x - y + z = 32
```

### Part 1 Hashes and Merkle Tree

In this question, we will visit the different types of hashes available in Circom (and Solidity) and grow some Merkle trees!

Based on the resources we provide you as well as any additional research you have done, compare the four hashes and provide explanations in four different aspects: gas cost, capacity, proof generation efficiency, and proof size. It's ok if you cannot find reference for all four aspects, just do the best you can.


Let’s build a binary Merkle tree template in Circom and some relevant templates for leaf verification. We will use the Poseidon hash for this assignment.

Fork the week2 repo and initialize all submodules. Enter the Part1 directory and install all dependencies. In circuits/MerkleTree.circom, complete the code for the following templates (feel free to add any helper templates for intermediate components and it’s ok to reference existing repos as long as their licenses permit):

CheckRoot: Given all 2n already hashed leaves of an n-level tree, compute the Merkle root.

MerkleTreeInclusionProof: Given an already hashed leaf and all the elements along its path to the root, compute the corresponding root.

Run . scripts/compile-circuit.sh && node scripts/bump-solidity.js to compile the verifier contract for MerkleTreeInclusionProof of a 3-level tree.

We will now create a smart contract and use the circuits from above to verify a leaf inclusion on chain. In contracts/MerkleTree.sol, complete the code so that your contract will

initialize a blank (meaning all leaves are zeros) Merkle tree of 3 levels (8 leaves) in the constructor
clarification 1: assume the 0's are already hashed
clarification 2: the indexing convention of the hashes array is from bottom to top, left to right, of the tree

insertLeaf(): a function to insert a new already hashed leaf and update the relevant elements in the tree

verify(): a function that verifies the inclusion proof and checks that the output root from the proof is the same as the root on chain

Run npx hardhat test and attach a screenshot of all the tests passing in your PDF file

[bonus] In test/merkle-test.js, complete the code to verify the second leaf with the inclusion proof as well.

[bonus] Create a front-end UI that interacts with the above smart contract so that all of the functions can be called in the browser. The proof generation should also happen in the browser (Hint: WASM 👀).

### Part 2 Tornado Cash

How is Tornado Cash Nova different from Tornado Cash Classic? What are the key upgrades/improvements and what changes in the technical design make these possible?

What is the role of the relayers in the Tornado Cash protocols? Why are relayers needed?

In the Part2 directory of this week’s repo you will find a submodule that consists of a forked tornado-nova repo. Follow the README for instructions to install all dependencies and build via yarn.

Run yarn test and attach a screenshot of all the tests passing to your PDF file. 

In test/custom.test.js, write a test that: Alice deposits 0.1 ETH in L1 -> Alice withdraws 0.08 ETH in L2 -> assert recipient, omniBridge, and tornadoPool balances are correct.

In the same file, write a test that: Alice deposits 0.13 ETH in L1 -> Alice sends 0.06 ETH to Bob in L2 -> Bob withdraws all his funds in L2 -> Alice withdraws all her remaining funds in L1 -> assert all relevant balances are correct.

Copy your modified custom.test.js into week2/custom.test.modified.js for submission, so you don’t have to commit the submodule.

[bonus] Try out Tornado Classic on Goerli testnet and attach screenshots at deposit and withdrawal in the PDF file.

### Part 3 Semaphore

What is Semaphore? Explain in 4-8 sentences how it works.

How does Semaphore prevent double signing (or double withdrawal in the case of mixers)? Explain the mechanism in 4-8 sentences.

A lot of applications have already been built based on derivations from Semaphore, such as for voting (e.g. AnonyVote), survey or opinion (e.g. Ninja Survey, zkAsk), and authentication (e.g. InterRep, Continuum, zkPayroll). Can you suggest two more ideas for ZK applications that can be built upon Semaphore?