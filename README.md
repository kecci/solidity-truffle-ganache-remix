# Solidity Ganache VM Simulation + MetaMask

Chapter 2: Step-by-step install simulator for VM ethereum blockchain with Ganache and MetaMask. Then implement Smart Contract Solidity to Ganache.

## The Chapter
- Chapter 1: [Solidity Remix Basic Syntax](https://github.com/kecci/solidity-remix-basic)
- Chapter 2: [Simulation VM with Ganache and MetaMask for Solidity Smart Contract](https://github.com/kecci/solidity-truffle-ganache-remix) (you in here)
- Chapter 3: [Building Simple Decentralized Application with React and Truffle Box](https://github.com/kecci/solidity-react-truffle-box)

## Table of Contents
- [Solidity Ganache VM Simulation + MetaMask](#solidity-ganache-vm-simulation--metamask)
  - [The Chapter](#the-chapter)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Metamask](#metamask)
    - [Download, Install and Register](#download-install-and-register)
    - [Remix connect to Metamask](#remix-connect-to-metamask)
  - [Ganache](#ganache)
    - [Download \& Install](#download--install)
    - [Run Ganache](#run-ganache)
    - [Ganache connect to Metamask](#ganache-connect-to-metamask)
    - [Import Ganache Account to Metamask](#import-ganache-account-to-metamask)
    - [Send ETH between Account](#send-eth-between-account)
  - [Smart Contract Remix to Ganache](#smart-contract-remix-to-ganache)
  - [Next](#next)


## Introduction
Before we running the VM of Blockchain with ganache, we need to install metamask for our browser wallet.

## Metamask
A crypto wallet & gateway to blockchain apps.

### Download, Install and Register
Download: https://metamask.io/download/

### Remix connect to Metamask
To run Remix, we can following remix basic before: https://github.com/kecci/solidity-remix-basic

Now, we want to connect to the remix with metamask:
1. Open the remix our workspace, then compile one of the contract
2. Then go to deployment section, and choose `Injected Provider - Metamask` ![img](assets/remix-environment.png)
3. It will be show pop up connecting Remix to Metamask. ![img](assets/remix-connect-metamask.png)
4. After we submit, the `Account` and the `Wallet` would be have same address ![img](assets/remix-connected-account.png) ![img](assets/remix-connected-metamask.png)

For now, we just want to know how to connect remix to Metamask. 

After this, we next step to `Import` the account from Local VM Ganache.

## Ganache
Personal Ethereum Blockchain. (Local VM).

### Download & Install
Download: https://trufflesuite.com/ganache/

### Run Ganache
We can following these steps:
1. Open ganache, choose `Quickstart`. ![img](assets/ganache-launch.png)
2. We can see 10 address account simulator for each 100 eth. ![img](assets/ganache-account.png)
3. If we click on :key: `Key Button` We can see Account Information about the `Account Address` and `Private Key`. ![img](assets/ganache-account-info.png)

### Ganache connect to Metamask

After we running the Ganache. We can connect the network to the metamask.

Following these steps:
1. Open the Metamask. And Click on dropdown Network. ![img](assets/metamask-networks.png)
2. Choose `Add Network` and will redirect to these settings. ![img](assets/metamask-network-config.png)
3. Choose `Add a network manually` and will open these form network. ![img](assets/metamask-add-network-manually.png)
4. Input the network settings for `Ganache`, you can follow these input. ![img](assets/metamask-add-network-ganache.png)
   1.  Network Name: `Ganache`
   2.  New RPC URL: `HTTP://127.0.0.1:7545`
   3.  Chain ID: `1337`
   4.  Currency Symbol: `ETH`
5. Save, and we can see the Network Ganache already added. ![img](assets/metamask-network-ganache.png)

### Import Ganache Account to Metamask
We want to import the Ganache Account to metamask, we can follow these steps:
1. Open the account section, and choose `Import Account`. ![img](assets/metamask-import-account.png)
2. It will show the form import account. ![img](assets/metamask-form-account.png)
3. Copy the `Private Key` on Ganache before, then copy it to the metamask private key form. ![img](assets/ganache-account-info.png)
4. After that, click `Import` button. We will see the `Account Address` and `Balance` are same like as in `Ganache Account`. ![img](assets/metamask-ganache-account-imported.png) We can adding multiple accounts from Ganache to Metamask.

### Send ETH between Account
After We have 2 imported account. We can simulate to send ETH between account.

Follow these steps:
1. In metamask, Click on `Send`. Then it will redirect to form send. ![img](assets/metamask-send.png)
2. Fill the inputs with the different account address. It will be like this. ![img](assets/metamask-send-to-account-3.png)
3. Then we set the `Amount`, and click send. For example 5 ETH. It will redirect to `Confirmation Page`. ![img](assets/metamask-send-confirmation.png)
4. After we submit `Confirm`. We will redirect to `Transaction Queue Section`. ![img](assets/metamask-transaction-queue.png) 
5. After waiting for the pending, the transaction will be updated to History Section. ![img](assets/metamask-transaction-history.png)
6. Congratulations, we have successfully send the coin ! You can see also in Ganache Balance are updated. ![img](assets/ganache-after-transaction.png)

## Smart Contract Remix to Ganache

First, we need to create the smart contract.
```solidity
pragma solidity >=0.7.0 <0.9.0;

contract ProofOfExistence {
    mapping (bytes32 => bool) private proofs;

    function storeProof(bytes32 proof) public {
        proofs[proof] = true;
    }

    function proofFor(string memory document) private pure returns (bytes32) {
        return sha256(bytes(document));
    }

    function notarize(string memory document) public {
        storeProof(proofFor(document));
    }

    function checkDocument(string memory document) public view returns (bool) {
        return proofs[proofFor(document)];
    }
}
```

Step to deploy the contract:
1. Run the `Ganache` and choose `Quick Start`. Then we see the accounts ![img](assets/ganache-account.png)
2. Open Remix Browser, and select the localhost. ![img](assets/remix-local.png)
3. In Remix, open tab Deploy then choose Environment `External HTTP Provider`. ![img](assets/remix-external-http-provider.png)
4. Update the url & port to follow the Ganache `RPC Server`. Which in this case is `http://127.0.0.1:7545` ![img](assets/ganache-rpc-server.png)
5. After connected, we've got the same account in `remix account` and `ganache account`. ![img](assets/remix-account-same.png) ![img](assets/ganache-account-same.png)
6. In Remix, we `Deploy` the smart contract to some account. And we can see the contract. ![img](assets/remix-deployed.png)
7. In Ganache, we can see our contract in `Blocks` tab: ![img](assets/ganache-deployed-blocks.png) And in the `Transactions` tab: ![img](assets/ganache-deployed-transactions.png)

After deployed, Step to transaction:
1. Create a transaction, Call `notarize` with input `"Hello"`: ![img](assets/remix-transaction-notarize.png) We can see the transaction hash and the detail.
2. Then we can see in ganache transaction has been called, and the transaction hash is same like above. ![img](assets/ganache-transaction-notarize.png)
3. After that, we want to make sure that the transaction are legit. We can call the `checkDocument` with `"Hello"`: ![img](assets/remix-transaction-checkDocument.png) The response are valid true and the details are same like in Ganache transaction. **When only checking the transaction, there is no adding block / transaction**.

> Notes:
> - In create new transactions, it will be adding new blocks.
> - But in check the transaction, it won't be adding any blocks.

[Connecting Smart Contract in Remix to Ganache](https://www.youtube.com/watch?v=fRl2UA4S6dE&list=PLH1gH0TmFBBhvZi4kEqU6kCjyv_y8qBae&index=34)

## Next 
After we know the simulation of blockchain with Ganache and the Connecting Solidity Smart Contract. Next chapter is: [Building Simple Decentralized Application with React and Truffle Box](https://github.com/kecci/solidity-react-truffle-box)
