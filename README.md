# soliditymodifier
Solidity Modifier 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract PausableToke {
    address public owner;
    bool public paused;
    mapping(address => uint) public balances;

    constructor() {
        owner = msg.sender;
        paused = false;
        balances[owner] =1000;
    }

    modifier  onlyOwner() {
        require(msg.sender == owner, "Only owner can perform this action" );
        _;

    }

    modifier notPaused() {
        require(paused == false, "THE CONTRACT IS PAUSED");
        _;
    }

    function pause() public onlyOwner {
         paused = true;

    }

    function unpause() public onlyOwner {
        paused = false;

    }

    function transfer(address to, uint amount) public notPaused {
        require(balances[msg.sender] >= amount, "Insufficient balance");

        balances[msg.sender] -= amount;
        balances[to] += amount;

    }
            
         
}
