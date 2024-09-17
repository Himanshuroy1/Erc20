# ERC20 Token

This project demonstrates how to create an ERC20 token and deploy it using Remix, an online Solidity IDE.

## Overview

The contract is written in Solidity and implements a simple ERC20 token with basic functionalities such as minting, burning, and transferring tokens. It is based on OpenZeppelin's ERC20 and Ownable libraries, making it both secure and easy to manage by an owner.

## Features

- **Minting**: The owner can mint new tokens to a specified address.
- **Burning**: Any token holder can burn a portion of their tokens.
- **Transferring**: The contract allows for transferring tokens between addresses, with a check to ensure sufficient balance.

## Setup Instructions

### Running the Program

To deploy and interact with this contract, you can use Remix, which is a browser-based IDE for Solidity. Follow the steps below to get started:

1. **Open Remix**: Go to [Remix](https://remix.ethereum.org/).
2. **Create a New File**: Click the "+" icon in the left-hand sidebar and create a new file. Save it with a `.sol` extension (e.g., `MyToken.sol`).
3. **Copy the Code**: Paste the following code into your new file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract ERC20Token is ERC20, Ownable {
    constructor() ERC20("Major", "GT") Ownable(msg.sender) {
        _mint(msg.sender, 10 * 100 ** decimals());
    }

    function mint(address recipient, uint256 amount) external onlyOwner {
        _mint(recipient, amount);
    }

    function burn(uint256 amount) external {
        _burn(msg.sender, amount);
    }

    function transfer(address from, address to, uint256 amount) public returns (bool) {
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");
        _transfer(from, to, amount);
        return true;
    }
}
```

### Compiling the Contract

1. Click on the "Solidity Compiler" tab in the sidebar.
2. Select the compiler version `0.8.20` from the dropdown.
3. Click the "Compile MyToken.sol" button.

### Deploying the Contract

1. Go to the "Deploy & Run Transactions" tab.
2. Select the contract you wish to deploy.
3. Click the "Deploy" button.

### Interacting with the Contract

After deploying, you can interact with the contract's functions:

- **Mint**: Use the `mint` function to add tokens to a specified address. Enter the recipient's address and the token amount, then click "transact."
- **Burn**: Use the `burn` function to reduce the total supply by burning tokens from your own balance. Enter the token amount and click "transact."
- **Transfer**: Use the `transfer` function to send tokens between two addresses. Enter the sender’s address, the recipient’s address, and the amount, then click "transact."

## License

This contract is licensed under the MIT License.

## Author

Himanshu Roy
