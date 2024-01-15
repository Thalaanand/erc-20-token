# MyToken 

## Overview

This Solidity smart contract represents a basic ERC-20 token named "MyToken" with the symbol "MTK." The contract extends the functionalities provided by the OpenZeppelin ERC20 and Ownable contracts.

## License

This contract is licensed under the MIT License. Please refer to the SPDX-License-Identifier in the source code for more details.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
```

## Features

### ERC-20 Standard

The contract follows the ERC-20 standard, allowing for seamless integration with various decentralized applications, exchanges, and other contracts that support this standard.

### Ownership

The token contract is Ownable, meaning it has an owner (initially set to the deployer's address) who has special privileges, such as minting new tokens.

### Minting

Only the owner can mint new tokens using the `mint` function. The `onlyOwnerCanMint` modifier ensures that only the owner can perform this action. The `mint` function requires a valid recipient address (`vendee`) and a positive minting stipend.

```solidity
function mint(address vendee, uint256 stipend) external onlyOwnerCanMint {
    require(stipend > 0, "Non-positive stipend");
    _mint(vendee, stipend);
}
```

### Burning

Token holders can burn their own tokens using the `burn` function. The function requires a positive and valid burn stipend, ensuring that the amount to burn is within the sender's balance.

```solidity
function burn(uint256 stipend) external {
    require(stipend > 0 && stipend <= balanceOf(_msgSender()), "Invalid burn tokens");
    _burn(_msgSender(), stipend);
}
```

### Transfer

The `transfer` function allows token holders to transfer tokens to another address. Additional checks ensure the validity of the transaction by requiring a valid recipient address (`vendee`), a positive transfer stipend, and a sufficient balance.

```solidity
function transfer(address vendee, uint256 stipend) public override returns (bool) {
    require(vendee != address(0) && stipend > 0 && stipend <= balanceOf(_msgSender()), "Invalid transfer");
    _transfer(_msgSender(), vendee, stipend);
    return true;
}
```

## Usage

1. Deploy the contract to the Ethereum blockchain.
2. The deployer becomes the initial owner of the contract.
3. The owner can mint new tokens using the `mint` function.
4. Token holders can burn their tokens using the `burn` function.
5. Tokens can be transferred using the `transfer` function.

## Author

thalaanand959170@gmail.com

