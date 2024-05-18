FunctionsAndErrors Solidity Contract

This is a simple Solidity contract named `FunctionsAndErrors` that allows an owner to deposit and withdraw Ether, check the balance, and manage age verification.

Contract Overview

Owner: The address that deploys the contract becomes the owner.
Balance: Tracks the Ether balance of the contract.
Age: Stores the age of the owner or user and includes a check for whether the age indicates adulthood (18 years or older).

 Functions

deposit(): Allows anyone to deposit Ether into the contract. The deposit amount must be greater than 0.
withdraw(uint256 amount): Allows only the owner to withdraw a specified amount of Ether from the contract. The amount must be greater than 0 and cannot exceed the contract's balance.
checkBalance(): Allows only the owner to check the contract's balance.
isAdult(): Returns `true` if the age is 18 or older, otherwise `false`.
setAge(uint256 _age): Allows only the owner to set a new age, which must be greater than 0.

Errors and Assertions

The contract includes `require` statements to ensure conditions are met before proceeding with function execution.
The `withdraw` function includes an `assert` to ensure the withdrawal amount does not exceed the balance.
The `withdraw` function reverts with a custom message, simulating an error after the balance deduction.

Deployment and Usage

rerequisites
Remix IDE: An online Solidity IDE available at [Remix IDE](https://remix.ethereum.org/).

Steps to Deploy

1. Open Remix IDE:
    Navigate to [Remix IDE](https://remix.ethereum.org/).

2. Create a New File:
    Click on the `+` icon to create a new file.
    Name the file `FunctionsAndErrors.sol`.

3. Copy and Paste the Contract Code:
    Copy the following Solidity contract code and paste it into the newly created file:

solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract FunctionsAndErrors {
    address public owner;
    uint256 public balance = 50;
    uint256 public age;

    constructor(uint256 _age) {
        require(_age > 0, "Age must be greater than 0");
        owner = msg.sender;
        age = _age;
    }

    function deposit() public payable {
        require(msg.value > 0, "Deposit amount should be greater than 0");
        balance += msg.value;
    }

    function withdraw(uint256 amount) public {
        assert(amount <= balance);
        require(msg.sender == owner, "Only the contract owner can withdraw");
        require(amount > 0, "Withdrawal amount should be greater than 0");
        balance -= amount;
        revert("Withdrawal successful, but custom error message");
    }

    function checkBalance() public view returns (uint256) {
        require(msg.sender == owner, "Only the contract owner can check the balance");
        return balance;
    }

    function isAdult() public view returns (bool) {
        return age >= 18;
    }

    function setAge(uint256 _age) public {
        require(msg.sender == owner, "Only the contract owner can set the age");
        require(_age > 0, "Age must be greater than 0");
        age = _age;
    }
}

Author 
Metacrafter ralph
