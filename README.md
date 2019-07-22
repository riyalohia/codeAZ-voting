# Open Vote Network


What is the Open Vote Network?
=========================


The Open Vote Network (OV-net) is a 2-round decentralized voting protocol with the following attractive features

* All communication is public - no secret channels between voters are required.
* The voter's privacy protection is maximum - only a full collusion that involves all other voters in the election can uncover the voter's secret vote.
* The system is dispute-free - everybody can check whether all voters act according to the protocol, hence ensuring the the result is publicly verifiable.

This program presents an efficient realization of this protocol over the Ethereum network.


Why Ethereum?
==============

Ethereum is a platform for Smart Contracts that provides the following:

* A public communication channel (i.e. its peer to peer network).
* All communication is authenticated (i.e. transactions are signed by the voter's Ethereum address)
* An immutable public ledger to store the voting information (i.e. eligibility white list, voting keys and votes).
* Economic majority must reach consensus on a program's execution.

The above allows anyone to verify the execution of the program, and that the protocol is executed correctly.

How does it work?
================

SETUP

- Election Admin is responsible for sending Ethereum a white list of eligible voters.

SIGNUP

- Voters submit their voting key, and a zero knowledge proof to prove knowledge of the voting key's secret.
- Ethereum verifies the correctness of the zero knowledge proof and stores the voting key.

VOTE

- Voters submit their ElGamal encrypted vote, and a 1 out of 2 zero knowledge proof that the vote is either 1 or 0. (i.e. yes or no).
- Ethereum verifies the 1 out of 2 zero knowledge proof and stores the vote.


SETUP
=====================================

You need to run 'Geth' in the background:

1. geth <OPTIONAL: --dev/testnet> --rpc --rpcapi="db,eth,net,web3,personal" --rpcport "8545" --rpcaddr "127.0.0.1" --rpccorsdomain "*" console

Example: ./geth --dev --rpc --ipcpath "~/Library/Ethereum/geth.ipc" --rpcapi="db,eth,net,web3,personal" --rpcport "8545" --rpcaddr "127.0.0.1" --rpccorsdomain "*" console
 
2. Compile the .SOL, and send it to the Ethereum Network.

3. Update vote.html, admin.html with the correct abi/contract address.

4. Voters open vote.html, and the Election Admin opens admin.html

5. Each voter requires a voter.txt document that contains the following:
 * x - the private key for the voter's voting key,
 * xG - the voter's voting public key,
 * v - the random nonce for a single ZKP,
 * w,r,d - the random nonces for the 1 out of 2 ZKP.
 * All values should be seperated by commas (i.e. ",") in a .txt document.

6. Voters can register and cast their vote.

An example 'voter.txt' has been included, and a Java Program 'votingcodes.jar' is included that can compute these numbers for the voter.