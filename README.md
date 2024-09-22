DeFi Kingdom Clone on Avalanche EVM Subnet
This project demonstrates the steps required to set up and deploy a DeFi Kingdom clone on a custom EVM subnet on the Avalanche network. Follow the steps outlined below to create your own decentralized game with native currency, smart contracts for battling, exploring, and trading, and integration with Metamask.

Prerequisites
Metamask browser extension
Avalanche CLI
Solidity development environment (e.g., Remix)
Steps
1. Set up your EVM subnet
Follow the Avalanche documentation to create a custom EVM subnet.
Use our guide for specific steps and configurations needed to set up your subnet.
2. Define your native currency
Set up your own native currency to be used as the in-game currency for your DeFi Kingdom clone.
Customize the parameters to suit your game's needs, such as total supply, name, and symbol.
3. Connect to Metamask
Connect your EVM Subnet to Metamask by following the steps laid out in our guide.
Add the custom RPC endpoint and chain ID to Metamask.
4. Deploy basic building blocks
a. ERC20 Token Contract
Deploy an ERC20 token contract using Solidity. Below is a basic implementation:

b. Vault Contract
Deploy a Vault contract to handle deposits and withdrawals:

License
This project is licensed under the MIT License. See the LICENSE file for details.
