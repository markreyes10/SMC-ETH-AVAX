# SMC-ETH-AVAX - SMART CONTRACT MANAGEMENT ASSESSMENT
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
# Description
The ReyesLoanManager contract is a Solidity smart contract designed to manage loan balances. It has specific functionalities that allow the contract owner to interact with the loan balance, either by repaying loans or borrowing additional funds. 
contract ReyesLoanManager {
    address public owner;
    mapping(address => uint256) public loanBalances; 
    
# Getting Started
constractor that shows the contract owner and initializes the initial loan balance upon contract deployment. 
    // Constructor: Set contract owner and initial loan balance
    constructor() {
        owner = msg.sender;
        loanBalances[address(this)] = 50000;
    }
    
# # Executing the program 
The contract provides functionalities for the owner to manage the loan balance, including repaying and borrowing.
- The payBackLoan function allows the contract owner to repay a portion of the loan. 
    // Function to reduce contract's loan balance
    function payBackLoan(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can pay back the loan");
        require(loanBalances[address(this)] >= amount, "Not enough loan balance");
        loanBalances[address(this)] -= amount;
    }
This allows the contract owner to borrow additional funds. They need to send the correct amount to increase the loan balance in the contract.
- The checkLoanBalance function allows anyone to view the current loan balance of the contract. 
    // Function to check contract's loan balance
    function checkLoanBalance() public view returns (uint256) {
        return loanBalances[address(this)];
    }
The borrow function allows the contract owner to increase the loan balance.
- This function includes an ownership check to ensure that only the owner can borrow additional funds.
    // Function to increase contract's loan balance
    function borrow(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can borrow from the contract");
        loanBalances[address(this)] += amount;
    }
}
