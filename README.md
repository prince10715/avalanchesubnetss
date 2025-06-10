DeFi Kingdom Clone on Avalanche EVM Subnet
This project demonstrates how to set up and deploy a DeFi Kingdom clone on a custom EVM subnet within the Avalanche network. You will learn to create your own decentralized game featuring native currency, smart contracts for battling, exploring, and trading, all integrated with Metamask.

Prerequisites
Metamask browser extension
Avalanche CLI
Solidity development environment (e.g., Remix)
Steps
1. Set Up Your EVM Subnet
Follow the Avalanche documentation to create a custom EVM subnet.
Refer to our guide for specific configuration steps to set up your subnet tailored for the game.
2. Define Your Native Currency
Create a native in-game currency for your DeFi Kingdom clone by deploying an ERC20 token.
Customize parameters like total supply, token name, and symbol according to your game’s requirements.
3. Connect to Metamask
Link your EVM subnet to Metamask by adding the custom RPC endpoint and Chain ID.
Follow the steps in our guide to correctly configure Metamask for your subnet.
4. Deploy the Game's Building Blocks
a. ERC20 Token Contract
Deploy an ERC20 token contract using Solidity. Below is a basic implementation to get you started:
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ERC20 {
    uint public totalSupply;
    mapping(address => uint) public balanceOf;
    mapping(address => mapping(address => uint)) public allowance;
    string public name = "Solidity by Example";
    string public symbol = "SOLBYEX";
    uint8 public decimals = 18;

		event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);

    function transfer(address recipient, uint amount) external returns (bool) {
        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint amount) external returns (bool) {
        allowance[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool) {
        allowance[sender][msg.sender] -= amount;
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }

    function mint(uint amount) external {
        balanceOf[msg.sender] += amount;
        totalSupply += amount;
        emit Transfer(address(0), msg.sender, amount);
    }

    function burn(uint amount) external {
        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;
        emit Transfer(msg.sender, address(0), amount);
    }
}
b. Vault Contract
Deploy a Vault contract that handles in-game deposits and withdrawals:

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

interface IERC20 {
    function totalSupply() external view returns (uint);

    function balanceOf(address account) external view returns (uint);

    function transfer(address recipient, uint amount) external returns (bool);

    function allowance(address owner, address spender) external view returns (uint);

    function approve(address spender, uint amount) external returns (bool);

    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);
}

contract Vault {
    IERC20 public immutable token;

    uint public totalSupply;
    mapping(address => uint) public balanceOf;

    constructor(address _token) {
        token = IERC20(_token);
    }

    function _mint(address _to, uint _shares) private {
        totalSupply += _shares;
        balanceOf[_to] += _shares;
    }

    function _burn(address _from, uint _shares) private {
        totalSupply -= _shares;
        balanceOf[_from] -= _shares;
    }

    function deposit(uint _amount) external {
        /*
        a = amount
        B = balance of token before deposit
        T = total supply
        s = shares to mint

        (T + s) / T = (a + B) / B 

        s = aT / B
        */
        uint shares;
        if (totalSupply == 0) {
            shares = _amount;
        } else {
            shares = (_amount * totalSupply) / token.balanceOf(address(this));
        }

        _mint(msg.sender, shares);
        token.transferFrom(msg.sender, address(this), _amount);
    }

    function withdraw(uint _shares) external {
        /*
        a = amount
        B = balance of token before withdraw
        T = total supply
        s = shares to burn

        (T - s) / T = (B - a) / B 

        a = sB / T
        */
        uint amount = (_shares * token.balanceOf(address(this))) / totalSupply;
        _burn(msg.sender, _shares);
        token.transfer(msg.sender, amount);
    }
}


DeFi Kingdom Clone on Avalanche EVM Subnet
This project demonstrates how to set up and deploy a DeFi Kingdom clone on a custom EVM subnet within the Avalanche network. You will learn to create your own decentralized game featuring native currency, smart contracts for battling, exploring, and trading, all integrated with Metamask.

Prerequisites
Metamask browser extension
Avalanche CLI
Solidity development environment (e.g., Remix)
Steps
1. Set Up Your EVM Subnet
Follow the Avalanche documentation to create a custom EVM subnet.
Refer to our guide for specific configuration steps to set up your subnet tailored for the game.
2. Define Your Native Currency
Create a native in-game currency for your DeFi Kingdom clone by deploying an ERC20 token.
Customize parameters like total supply, token name, and symbol according to your game’s requirements.
3. Connect to Metamask
Link your EVM subnet to Metamask by adding the custom RPC endpoint and Chain ID.
Follow the steps in our guide to correctly configure Metamask for your subnet.
4. Deploy the Game's Building Blocks
a. ERC20 Token Contract
Deploy an ERC20 token contract using Solidity. Below is a basic implementation to get you started:


b. Vault Contract
Deploy a Vault contract that handles in-game deposits and withdrawals:


License
This project is licensed under the MIT License. See the LICENSE file for further details.
#author 
Name:Prince Kumar
Gmail:kumarprincerajput124@gmail.com
[GitHub – princekumar](https://github.com/prince10715)

