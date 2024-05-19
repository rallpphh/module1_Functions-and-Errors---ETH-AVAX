# My Monthly Allowances Solidity Contract
This Solidity contract, named My_Monthly_Allowances, is designed to manage a monthly allowance for an address. The contract allows the owner to add allowances, record daily expenses, and update the monthly allowance.

# Contract Overview
Wallet: The address that deploys the contract becomes the wallet address (owner).

Monthly Allowance: Tracks the monthly allowance amount which can be updated by the owner.

# Functions
addAllowance(uint256 _value): Allows the owner to add to the monthly allowance. The added value must be greater than 1000 and not exceed the current monthly allowance.

DailyExpenses(uint256 _value): Records daily expenses deducted from the monthly allowance. The expense value must be greater than 100 and not exceed the current monthly allowance.

updateMonthlyAllowance(uint256 newAllowance): Allows only the owner to update the monthly allowance to a new value.

# Errors and Assertions
The contract includes require statements to ensure that conditions are met before proceeding with function execution:

addAllowance requires the value to be greater than 1000 and asserts it does not exceed the monthly allowance.
DailyExpenses requires the expense value to be greater than 100 and asserts it does not exceed the monthly allowance.
Deployment and Usage
Prerequisites
Remix IDE: An online Solidity IDE available at Remix IDE.
Steps to Deploy
Open Remix IDE:

Navigate to Remix IDE.
Create a New File:

Click on the + icon to create a new file.
Name the file My_Monthly_Allowances.sol.
Copy and Paste the Contract Code:

Copy the following Solidity contract code and paste it into the newly created file:
solidity
Copy code
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract My_Monthly_Allowances {
    address public wallet;
    uint256 public monthlyAllowance = 5000; // initial monthly allowance

    constructor() {
        wallet = msg.sender;
    }

    function addallowance(uint256 _value) public payable {
        assert(_value <= monthlyAllowance);
        require(_value > 1000, "Add Allowance value should be greater than 1000");
        monthlyAllowance <= 1000;
    }

    function DailyExpenses(uint256 _value) public {
        assert(_value <= monthlyAllowance);
        require(_value > 100, "Daily Expenses value should be greater than 100");
        monthlyAllowance -= _value;
    }

    function updateMonthlyAllowance(uint256 newAllowance) public {
        require(msg.sender == wallet, "Only the contract owner can update the monthly allowance");
        monthlyAllowance = newAllowance;
    }
}
# Author
Metacrafter ralph
