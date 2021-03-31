# Project goals

- Connect the functions of your blockchain to a front end that users can interact with.
- Fix some of the issues that come up needed to make this DApp live.
- Deploy your DApp to the test network and view the results

# Tools and libraries

## Ganache

Create a local blockchain network for us. It allow us to make tests.

## Remix

Used to deploy a smart contract in the choosed blockchain network. At this case, we'll connect on the ganache network throughout web3.

## Web3 library

Allow the developer manage and interact with the blockchain network.

# Project explanation

## Our smart contract
It's a sample code that have two methods:
- setMessage that storage some string on memory.
- getMessage that shows the string storaged.

Solidity code - myMessage.sol
```
pragma solidity ^0.4.24;

contract Message {
    string myMessage;

    function setMessage(string x) public {
        myMessage = x;
    }

    function getMessage() public view returns (string) {
        return myMessage;
    }
}
```

## How to deploy
We use remix to make the smart contract deploy on ganache.
With it done we can use this contract in javaScript code accessing it throughout web3.js.

## Html page
A page that shows an input and a button to send the message to the blockchain.

## Script
Get the smart contract ABI and contract address.
Done it, is possible access the methods of smart contracts and use it on the code.

# Project result


