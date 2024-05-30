SMC 

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ReyesLoanManager {
    address public owner;
    mapping(address => uint256) public loanBalances; 

constructor() {
        owner = msg.sender;
        loanBalances[address(this)] = 50000;
    }

 function payBackLoan(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can pay back the loan");
        require(loanBalances[address(this)] >= amount, "Not enough loan balance");
        loanBalances[address(this)] -= amount;
    }


  function checkLoanBalance() public view returns (uint256) {
        return loanBalances[address(this)];
    }

 function borrow(uint256 amount) public {
        require(msg.sender == owner, "Only the owner can borrow from the contract");
        loanBalances[address(this)] += amount;
    }
}
