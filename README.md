# Coffee-Vending-machine
//SPDX-License-Identifier:MIT

pragma solidity ^0.8.0;

contract vendingMachine{
    address public owner;
    
    mapping(address => uint) public coffeeBalances;
    
    constructor(){
        owner = msg.sender;
        
        coffeeBalances[address(this)] = 100;
}

function getBalance() public view returns (uint) {

return coffeeBalances[address(this)];

}

function restock(uint amount) public {

require(msg.sender == owner, "Only owner able to restock the coffee");

coffeeBalances[address(this)]+= amount;

}

function purchase(uint amount) public payable{

require(msg.value >= amount * 0.4 ether, "You've to pay atleast 1 ether for one coffee");

require(coffeeBalances[address(this)] >= amount, "sorry,Not enough coffee");

coffeeBalances[address(this)] -= amount;

coffeeBalances[address(msg.sender)] += amount;

}

}
