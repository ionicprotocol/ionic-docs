---
description: >-
  Liquidating positions is a core aspect of any borrowing and lending protocol.
  We offer functionality to fetch potential liquidations, as we as to actually
  run the liquidations.
---

# Liquidations

While we run our own bots for ensuring that liquidations occur smoothly, users are also incentivised to the same, as every liquidation might be a healthy source of profit, since each liquidation comes with a [liquidation incentive](https://compound.finance/docs/comptroller#liquidation-incentive).&#x20;

The source code for the liquidation bots we run is fully open-sourced, and it leverages heavily the SDK. Users are welcomed to fork it and run their own liquidation bots.

Check it out in our [monorepo](https://github.com/Midas-Protocol/monorepo/tree/development/packages/bots/fuse-liquidator-bot).

## Gathering Liquidations

#### `getPotentialLiquidations`

**Arguments:**

* `signer: ethers.Wallet`: a wallet from which to run the liquidations
* `supportedComptrollers: Array = []`: a list of supported pool addresses. If empty, all pools will be checked
* `maxHealthFactor: BigNumber = utils.parseEther("1")`: filter positions by their health factors
* `configOverrides?:` [`ChainLiquidationConfig`](api-reference-typing-and-interfaces.md#chainliquidationconfig): configuration for the supported input and output currencies for the liquidation and other parameters

**Returns:**

* `Promise<Array<`[`LiquidatablePool`](api-reference-typing-and-interfaces.md#liquidatablepool)`>>`

### `liquidatePositions`

**Arguments:**

* `positions: Array<`[`LiquidatablePool`](api-reference-typing-and-interfaces.md#liquidatablepool)`>`

**Returns:**

* `null`
