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
We use remix to compile the smart contract and deploy it on ganache network.
With it done we can use this contract in javaScript code accessing it throughout web3.js.

## Html page
A page that shows an input and a button to send the message to the blockchain.

## Script
Get the smart contract ABI and contract address.
Done it, is possible access the methods of smart contracts and use it on the code.

### Code explanation

First, I want to explain what ABI is. The worldwide computer Ethereum has a virtual machine - EVM.
Thus, for the contract to be executed in the EVM, it is necessary to compile it to generate the bytecode.
Therefore, bytecode is the way in which the virtual machine can understand and execute a smart contract.

After the contract is already on the blockchain, other accounts need to use the methods of this contract.
That's where ABI comes from. It is generated when the contract is created to allow other accounts to understand the contract object and use it.
Therefore, the ABI is a significant JSON that allows the account to hash some function of this contract and generate the bytecode to be executed by the EVM.

Ok. So what we do on the code. First we need to get the instance of Ganache network.
For that we use the web3js library.
```
var web3 = new Web3(new Web3.providers.HttpProvider('http://127.0.0.1:7545'));                   
```

After we'll use the web3 object to create a instance of the smart contract.
For that we need two things:
- The contract ABI.
- The contract address.
```
var myContract = new web3.eth.Contract([
    {
        "constant": false,
        "inputs": [
            {
                "name": "x",
                "type": "string"
            }
        ],
        "name": "setMessage",
        "outputs": [],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "getMessage",
        "outputs": [
            {
                "name": "",
                "type": "string"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    }
],'0x7Fd8541D86870CA37F62b4B55eFcb85Ce61B9d0C');            
```

Thus, ABI allows javaScript to understand the contract and use its methods and variables.
This way, when the html button is clicked, the setMessage method will be called and then we can see
the string set with the getMessage method.
```    
$("#setMessageButton").click(function () {
    message = $("#userInput").val()
    myContract.methods.setMessage(message)
    .send({from: '0xf20c1a6BfEc7F2D617e6e5e4c027BAF6780d4D98'})
    .then(result => {
        console.log(result);
        myContract.methods.getMessage()
            .call()
            .then(console.log);        
    });                        
});
```

# Project result

![image](https://user-images.githubusercontent.com/73957838/113078192-fa9c1b80-91a8-11eb-996f-2ff6759d82b8.png)

So what happens here? You can see that if you type a message and click the button, you will see that message on the console.
Another thing that you can notice is the transaction that was created. Note that it was created on the ganache network. So it shows that
we achieved the objective of the project.

