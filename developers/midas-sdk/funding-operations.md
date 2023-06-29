---
description: >-
  These are the core actions that enable users to actually use their funds
  within the protocol.
---

# Funding Operations

Enabling programmatic control of these operations offers a powerful shorthand to developers interested in integrating with Midas Capital.&#x20;

The functions here shown enable the typical interactions with a Money Market:

* Depositing collateral to a pool
* Borrow funds against the deposited collateral
* Repay the borrowed funds
* Withdraw collateral from a pool

With these, protocol developers can seamlessly add a Borrow and Lending page to their web applications, and have a very concise interface with which they can enable users to perform the major operations against a lending & borrowing pool

### `supply`

Supply assets to a pool, with the option of enabling them to be used as collateral

**Arguments**:

* `cTokenAddress: string`: the address of the `cToken` to be supplied
* `underlyingTokenAddress: string`: the address of the underling token of the `cToken` to be borrowed
* `comptrollerAddress: string`: the comptroller e.g., the pool's address
* `enableAsCollateral: boolean`: whether the deposited underlying should be enabled to be used as collateral
* `amount: BigNumber`: amount in `BigNumber` format
* `options: { from: string }`: address from which to perform the funding

**Returns**:

* `{tx: ContractTransaction, errorCode: number | null}`

### `borrow`

After having deposited into a pool and marked an asset as enabled for collateralization, you may perform a borrow against that asset

**Arguments**:

* `cTokenAddress: string`: the address of the `cToken` to be borrowed
* `amount: BigNumber`: amount to be borrowed in `BigNumber` format
* `options: { from: string }`: address from which to perform the borrowing

**Returns**:

* `{tx: ContractTransaction, errorCode: number | null}`

### `repay`

Repay a borrow action, with the option of repaying the full amount instead of specifying an amount.

**Arguments**:

* `cTokenAddress: string`: the address of the `cToken` to be repaied
* `underlyingTokenAddress: string`: the address of the underling token of the `cToken` to be repaid
* `isRepayingMax: boolean`: whether the maximum amount is being tried to be repaid
* `amount: BigNumber`: amount to be repaid in `BigNumber` format
* `options: { from: string }`: address from which to perform the repayment

**Returns**:

* `{tx: ContractTransaction, errorCode: number | null}`

### `withdraw`

Withdraw deposited funds from the pool. This redeems the underlying tokens deposited from the cTokens that belong to your account, and are currently not being used to collateralised a loan.

**Arguments**:

* `cTokenAddress: string`: the address of the `cToken` to be withdrawn
* `amount: BigNumber`: amount to be withdrawn in `BigNumber` format
* `options: { from: string }`: address from which to perform the withdrawal

**Returns**:

* `{tx: ContractTransaction, errorCode: number | null}`
