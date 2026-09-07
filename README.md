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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract VaultTwo {
    address public owner;
    uint256 public total;

    event Deposited(address indexed from, uint256 amount);
    event Withdrawn(uint256 amount);

    constructor() {
        owner = msg.sender;
    }

    function deposit() external payable {
        require(msg.value > 0, "Must send ETH");
        total += msg.value;
        emit Deposited(msg.sender, msg.value);
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");
        uint256 amount = address(this).balance;
        total = 0;
        (bool success, ) = owner.call{value: amount}("");
        require(success, "Transfer failed");
        emit Withdrawn(amount);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SparkThree {
    mapping(address => uint256) public sparks;
    mapping(address => uint256) public lastSpark;

    event Sparked(address indexed user, uint256 level);

    function spark() external {
        if (block.timestamp <= lastSpark[msg.sender] + 5 minutes) {
            sparks[msg.sender] += 1;
        } else {
            sparks[msg.sender] = 1;
        }
        lastSpark[msg.sender] = block.timestamp;
        emit Sparked(msg.sender, sparks[msg.sender]);
    }

    function getSparks(address user) external view returns (uint256) {
        return sparks[user];
    }
}
