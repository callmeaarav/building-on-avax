# StockRewardToken Smart Contract

## Overview

The `StockRewardToken` is an ERC20 token smart contract that allows users to mint, transfer, burn, and redeem tokens for specific stock rewards. The contract supports three types of stocks: TCS, Infosys, and Wipro. Users can redeem tokens for these stock types, and the contract keeps track of the last redeemed stock for each user.

## Contract Details

- **Token Name:** Stock Reward Token
- **Token Symbol:** SRT

## Functions

### Public and External Functions

1. **constructor(address initialOwner)**
   - Initializes the contract with the given owner and sets the initial stock costs.

2. **mintTokens(address recipient, uint256 amount) external onlyOwner**
   - Mints new tokens and assigns them to the specified recipient.
   - Only the contract owner can call this function.

3. **transferTokens(address recipient, uint256 amount) external**
   - Transfers tokens from the sender's account to the recipient's account.
   - Requires that the sender has a sufficient token balance.

4. **burnTokens(uint256 amount) external**
   - Burns a specified amount of tokens from the sender's account.
   - Requires that the sender has a sufficient token balance.

5. **redeemStockByName(string calldata stockName) external**
   - Allows a user to redeem tokens for a specified stock type.
   - Burns the required amount of tokens from the user's account.
   - Records the redeemed stock type and name for the user.
   - Emits a `Redeemed` event with the user address, stock name, and cost.

6. **redeemedStock() external view returns (string memory)**
   - Returns the name of the last redeemed stock for the caller.

### View Functions

1. **getMyTokenBalance() external view returns (uint256)**
   - Returns the token balance of the caller.

2. **getLastRedeemedStock() external view returns (StockType)**
   - Returns the `StockType` enum of the last redeemed stock for the caller.

### Internal Functions

1. **initializeStockCosts() internal**
   - Sets the initial costs for the three stock types: TCS, Infosys, and Wipro.

2. **getStockTypeByName(string calldata stockName) internal pure returns (StockType)**
   - Converts a stock name string to the corresponding `StockType` enum.
   - Reverts if the stock name is invalid.

3. **compareStrings(string memory a, string memory b) internal pure returns (bool)**
   - Compares two strings for equality using their keccak256 hashes.

### Events

- **Redeemed(address indexed user, string stockName, uint256 cost)**
  - Emitted when a user redeems tokens for a stock type.
  - Contains the user address, stock name, and cost.

## Usage

### Minting Tokens

To mint tokens, the owner can call:

```solidity
mintTokens(address recipient, uint256 amount)
```

### Transferring Tokens

Users can transfer tokens to another address by calling:

```solidity
transferTokens(address recipient, uint256 amount)
```

### Burning Tokens

Users can burn their tokens by calling:

```solidity
burnTokens(uint256 amount)
```

### Redeeming Tokens for Stocks

Users can redeem tokens for a specific stock by calling:

```solidity
redeemStockByName(string calldata stockName)
```

### Getting Token Balance

Users can get their token balance by calling:

```solidity
getMyTokenBalance()
```

### Getting Last Redeemed Stock

Users can get the last stock they redeemed by calling:

```solidity
getLastRedeemedStock()
```

### Getting Redeemed Stock Name

Users can get the name of the last stock they redeemed by calling:

```solidity
redeemedStock()
```

## Deployment

Deploy the contract with the owner's address as the parameter:

```solidity
StockRewardToken(address initialOwner)
```

## License

This project is licensed under the MIT License.

