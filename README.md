// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EmberTwo {
    mapping(address => uint256) public embers;
    mapping(address => uint256) public lastEmber;

    event EmberLit(address indexed user, uint256 level);

    function light() external {
        if (block.timestamp <= lastEmber[msg.sender] + 6 minutes) {
            embers[msg.sender] += 1;
        } else {
            embers[msg.sender] = 1;
        }
        lastEmber[msg.sender] = block.timestamp;
        emit EmberLit(msg.sender, embers[msg.sender]);
    }

    function getEmbers(address user) external view returns (uint256) {
        return embers[user];
    }
}
