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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TapThree {
    address[] public tappers;
    uint256[] public timestamps;

    event Tapped(address indexed user, uint256 timestamp, uint256 index);

    function tap() external {
        tappers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Tapped(msg.sender, block.timestamp, tappers.length - 1);
    }

    function getTap(uint256 index) external view returns (address, uint256) {
        require(index < tappers.length, "Invalid index");
        return (tappers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return tappers.length;
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PermitThree {
    address public owner;
    mapping(address => bool) public hasPermit;

    event PermitGranted(address indexed user);
    event PermitRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasPermit[msg.sender] = true;
    }

    function grantPermit(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPermit[user] = true;
        emit PermitGranted(user);
    }

    function revokePermit(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPermit[user] = false;
        emit PermitRevoked(user);
    }

    function checkPermit(address user) external view returns (bool) {
        return hasPermit[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LockerThree {
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

contract SignalThree {
    address[] public signalers;
    uint256[] public timestamps;

    event Signaled(address indexed user, uint256 timestamp, uint256 index);

    function signal() external {
        signalers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Signaled(msg.sender, block.timestamp, signalers.length - 1);
    }

    function getSignal(uint256 index) external view returns (address, uint256) {
        require(index < signalers.length, "Invalid index");
        return (signalers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return signalers.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PassThree {
    address public owner;
    mapping(address => bool) public hasPass;

    event PassGranted(address indexed user);
    event PassRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasPass[msg.sender] = true;
    }

    function grantPass(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPass[user] = true;
        emit PassGranted(user);
    }

    function revokePass(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPass[user] = false;
        emit PassRevoked(user);
    }

    function checkPass(address user) external view returns (bool) {
        return hasPass[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PocketThree {
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

contract AuraThree {
    mapping(address => uint256) public auras;
    mapping(address => uint256) public lastAura;

    event AuraGained(address indexed user, uint256 level);

    function gain() external {
        if (block.timestamp <= lastAura[msg.sender] + 8 minutes) {
            auras[msg.sender] += 1;
        } else {
            auras[msg.sender] = 1;
        }
        lastAura[msg.sender] = block.timestamp;
        emit AuraGained(msg.sender, auras[msg.sender]);
    }

    function getAuras(address user) external view returns (uint256) {
        return auras[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ClickThree {
    address[] public clickers;
    uint256[] public timestamps;

    event Clicked(address indexed user, uint256 timestamp, uint256 index);

    function click() external {
        clickers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Clicked(msg.sender, block.timestamp, clickers.length - 1);
    }

    function getClick(uint256 index) external view returns (address, uint256) {
        require(index < clickers.length, "Invalid index");
        return (clickers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return clickers.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract AccessFour {
    address public owner;
    mapping(address => bool) public hasAccess;

    event AccessGranted(address indexed user);
    event AccessRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasAccess[msg.sender] = true;
    }

    function grantAccess(address user) external {
        require(msg.sender == owner, "Not owner");
        hasAccess[user] = true;
        emit AccessGranted(user);
    }

    function revokeAccess(address user) external {
        require(msg.sender == owner, "Not owner");
        hasAccess[user] = false;
        emit AccessRevoked(user);
    }

    function checkAccess(address user) external view returns (bool) {
        return hasAccess[user];
    }
}
