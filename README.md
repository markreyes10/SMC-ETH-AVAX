# SMC-ETH-AVAX
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ReyesLoanManager {
    address public owner;
    mapping(address => uint256) public loanBalances;
# constractor that shows the contract owner and initializes the initial loan balance upon contract deployment. 
    // Constructor: Set contract owner and initial loan balance
    constructor() {
        owner = msg.sender;
        loanBalances[address(this)] = 50000;
    }

# This allows the contract owner to repay a loan and they need to send the correct amount and ensure that there is enough loan balance in the contract before making a repayment.
    // Function to reduce contract's loan balance
    function payBackLoan(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can pay back the loan");
        require(loanBalances[address(this)] >= amount, "Not enough loan balance");
        loanBalances[address(this)] -= amount;
    }
# This allows the contract owner to borrow additional funds. They need to send the correct amount to increase the loan balance in the contract.

    // Function to check contract's loan balance
    function checkLoanBalance() public view returns (uint256) {
        return loanBalances[address(this)];
    }

    // Function to increase contract's loan balance
    function borrow(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can borrow from the contract");
        loanBalances[address(this)] += amount;
    }
}
