Smart Contracts & Solidity: A Detailed Guide

1. What Are Smart Contracts?

A smart contract is a self-executing program stored on a blockchain that runs when predefined conditions are met. It automates transactions without intermediaries, ensuring trust, security, and transparency.

Key Characteristics:

✅ Trustless: No central authority needed.
✅ Immutable: Once deployed, the code cannot be altered.
✅ Transparent: Anyone can view the contract on a blockchain explorer.
✅ Automated Execution: Runs when conditions are met (e.g., sending ETH on payment).

Example Use Cases:

Token Transactions (ERC-20, ERC-721 NFTs)

Decentralized Finance (DeFi) (Lending, Staking, DEXs)

Decentralized Autonomous Organizations (DAOs)

Supply Chain Management

Voting Systems



---

2. What is Solidity?

Solidity is the programming language used to write Ethereum smart contracts. It is a statically typed, contract-oriented language similar to JavaScript and Python.

Why Solidity?

✅ Designed for Ethereum: Compatible with EVM (Ethereum Virtual Machine).
✅ Smart Contract Optimized: Features like modifiers, mappings, structs, and interfaces.
✅ Strong Developer Community: Open-source ecosystem with libraries like OpenZeppelin.


---

3. Solidity Basics

3.1 Solidity Structure

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0; // Compiler version

contract MyFirstContract {
    uint public myNumber; // State variable

    function setNumber(uint _num) public {
        myNumber = _num;
    }

    function getNumber() public view returns (uint) {
        return myNumber;
    }
}

Explanation:

pragma solidity ^0.8.0; → Defines compiler version.

contract MyFirstContract {} → Smart contract definition.

uint public myNumber; → State variable stored on the blockchain.

function setNumber(uint _num) public {} → Updates state.

function getNumber() public view returns (uint) {} → Reads state (view function).



---

4. Solidity Data Types


---

5. Smart Contract Features

5.1 Variables in Solidity

contract VariablesExample {
    uint public stateVar = 10; // State variable

    function localExample() public pure returns (uint) {
        uint localVar = 20; // Local variable
        return localVar;
    }
}

State Variables: Stored on blockchain (costs gas).

Local Variables: Exist only within a function (free).


5.2 Functions & Visibility Modifiers

contract FunctionExample {
    uint private myValue = 100;

    function setValue(uint _newValue) public {
        myValue = _newValue;
    }

    function getValue() public view returns (uint) {
        return myValue;
    }
}

5.3 Payable Functions (For Handling ETH)

contract PayableExample {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function sendEther() public payable {} // Accepts ETH

    function getBalance() public view returns (uint) {
        return address(this).balance;
    }

    function withdrawEther() public {
        require(msg.sender == owner, "Not owner");
        payable(owner).transfer(address(this).balance);
    }
}

payable → Allows contract to receive ETH.

require → Ensures only owner can withdraw.

transfer() → Sends ETH safely.



---

6. Solidity Advanced Concepts

6.1 Events (For Logging)

contract EventExample {
    event DataStored(address indexed user, uint value);

    function storeData(uint _value) public {
        emit DataStored(msg.sender, _value);
    }
}

emit → Logs data on the blockchain for external tracking.


6.2 Mappings (Key-Value Store)

contract MappingExample {
    mapping(address => uint) public balances;

    function setBalance(uint _amount) public {
        balances[msg.sender] = _amount;
    }
}

mapping(address => uint) → Stores balances per user.


6.3 Modifiers (Reusable Function Rules)

contract ModifierExample {
    address public owner;

    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function restrictedFunction() public onlyOwner {
        // Only owner can call this
    }
}

modifier onlyOwner → Restricts access to contract owner.

_ → Placeholder for function execution.


6.4 Self-Destruct (Destroying Contracts)

contract KillExample {
    address payable owner;

    constructor() {
        owner = payable(msg.sender);
    }

    function destroy() public {
        require(msg.sender == owner, "Not owner");
        selfdestruct(owner);
    }
}

selfdestruct(owner) → Deletes contract & sends funds to owner.



---

7. Solidity Security Best Practices

✅ Use require() to validate inputs
✅ Limit storage writes (gas efficiency)
✅ Avoid tx.origin for authentication (vulnerable to phishing)
✅ Use OpenZeppelin for standard contract templates
✅ Test with Hardhat/Foundry before deploying


---

8. Deploying Smart Contracts

Using Hardhat (Recommended)

npm install --save-dev hardhat
npx hardhat init

Write your contract in /contracts

Compile with: npx hardhat compile

Deploy using scripts in /scripts

Use testnets like Goerli, Sepolia, Mumbai


Using Remix (Quickest)

Go to Remix

Paste Solidity code & compile

Deploy using MetaMask



---

9. Real-World Smart Contract Examples

9.1 ERC-20 Token

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 1000000 * 10 ** decimals());
    }
}

Uses OpenZeppelin for standard token functions.


9.2 NFT (ERC-721)

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract MyNFT is ERC721 {
    constructor() ERC721("MyNFT", "MNFT") {}
}

Standard NFT contract for digital collectibles.



---

10. Next Steps: Learning & Practice

Practice Projects

✅ Simple Bank (Deposit & Withdraw ETH)
✅ Crowdfunding dApp
✅ DAO Governance Contract
✅ Decentralized Exchange (DEX)

Resources to Learn More

Solidity Docs: soliditylang.org

OpenZeppelin Library: openzeppelin.com

Ethereum Dev Portal: ethereum.org


Would you like help with a specific Solidity project? 🚀

