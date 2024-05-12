# require-assert-and-revert-

pragma solidity ^0.8.0;

contract MyContract {
  
    mapping (address => uint) public balances;

    event BalanceUpdated(address indexed user, uint newBalance);

    function deposit(uint amount) public {
        require(amount > 0, "Amount must be greater than 0");

        uint currentBalance = balances[msg.sender];

        balances[msg.sender] = currentBalance + amount;

        emit BalanceUpdated(msg.sender, balances[msg.sender]);
    }

    function withdraw(uint amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");

        uint currentBalance = balances[msg.sender];

        balances[msg.sender] = currentBalance - amount;

        emit BalanceUpdated(msg.sender, balances[msg.sender]);
    }

    function checkBalance() public {
        assert(balances[msg.sender] > 0);

        revert("User's balance is 0 or less");
    }
}
