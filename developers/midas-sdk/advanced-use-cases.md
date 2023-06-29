---
description: >-
  Managing, deploying, and customising a specific pool are advanced use-cases
  that offer the full capability of creating money markets with parameters of
  their choice, at their own will
---

# Advanced Use-Cases

### Deploying A Pool\*

Programmatic pool creation is offered as an alternative to the UI flow we have implemented at [https://app.midascapital.xyz/\[chainId\]/create-pool](https://app.midascapital.xyz/56/create-pool)

### `deployPool`

**Arguments:**

* `poolName: string`: canonical pool name. Can be edited by the pool's owner at a later point
* `enforceWhitelist: boolean`: whether to limit pool interactions to a set of whitelisted addresses
* `closeFactor: BigNumber`: the pool's Close Factor. See [Compound Finance docs](https://compound.finance/docs/comptroller#close-factor) for more information &#x20;
* `liquidationIncentive: BigNumber`: incentive given to the liquidators as profit for liquidating an unhealthy loan. [Compound Finance docs](https://compound.finance/docs/comptroller#liquidation-incentive)
* `priceOracle: string`: contract address of the price oracle to be used
* `priceOracleConf: OracleConf`: currently unused
* `options: { from: string }`:  from address from where to make the call
* `whitelist: string[]`:An array of whitelisted addresses

**Returns:**

* `Promise<[string, string, string, number?]>`: array of pool data, namely:&#x20;
  * the pool's address (also referred to as the pool's Comptroller address)
  * the Implementation Address: this is the  Comptroller's _implementation_ address. Every new pool will basically deploy a new Comptroller, the implementation of which is deployed once by Midas Capital, and is subject to upgrading
  * Price Oracle address
  * Pool ID&#x20;

**\*NOTE:** permissionless pool creation is currently unsupported -- as we are still in public beta, we are limiting the pool creation to only the Midas Team and selected partners. [Get in contact with us](https://twitter.com/MidasCapitalxyz) if you'd like to get whitelisted for such functionality

## Managing A Pool's Assets

One of the core tenants of the Midas protocol is the ability for pool operators to add support for any arbitrary asset\* to their pools. This can be done via the ui at [https://app.midascapital.xyz/\[chainId\]/pool/\[poolId\]/edit](https://app.midascapital.xyz/56/pool/1/edit) , but that is also achievable programmatically. Whether you're interested in creating a custom pool management UI for yourself, or enable other users to manage your pool, these functions should allow you to add and remove assets from the ones supported by the pool

### `deployAsset`

**Arguments:**

* `irmConf: InterestRateModelConf`: configuration parameters for the asset's Interest Rate Model
* `config: MarketConfig`
* `options: any`&#x20;



**\*NOTE:** arbitrary assets are supported only insofar as these assets have a valid price oracle for them. Currently, Midas Capital controls which oracles are deployed. We strive however to support our partners in adding assets they wish to the set of assets that we can currently support.  [Get in contact with us](https://twitter.com/MidasCapitalxyz) if you'd like us to support more assets!

## Running a Liquidity Mining Campaign

Every pool can be customised to be the source of a liquidity mining campaign. This provides pool operators a mechanism to incentivise borrows or lends of specific assets they have interest in making more widely available, as well as increasing TVL in their pool.&#x20;

At its core, a liquidity mining campaign is based on a set of contracts named the `Flywheel Contracts` initially developed by the folks from Fei Protocol, now part of the [Tribe DAO](https://docs.tribedao.xyz/docs/protocol/Overview). These sets of contracts can be conceived as a generalised token incentives infrastructure that enables directing tokens to users based on specific protocol interactions. You can read more about it [here](https://github.com/fei-protocol/flywheel-v2).

#### Step 1: Deploy Flywheel Core & Flywheel Static Rewards

First, we deploy the basic infrastructure

```typescript
import { ethers } from 'ethers';

// An ether's signer
const { deployer } = await ethers.getNamedSigners();

// E.g. WBNB as reward token for the LM campagin
const rewardTokenAddress = "0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c"

// Deploy Flywheel Core
const fwCore = await sdk.deployFlywheelCore(rewardTokenAddress, {
    from: deployer.address,
});

// Deploy Flywheel Static Rewards
const fwStaticRewards = await sdk.deployFlywheelStaticRewards(fwCore.address, {
  from: deployer.address,
});

// Setup FuseFlywheelCore with FlywheelStaticRewards
const tx = await sdk.setFlywheelRewards(fwCore.address, fwStaticRewards.address, {
  from: deployer.address,
});

await tx.wait()
```

#### Step 2: Add the Flywheel to the pool

Then, we just need to add the newly deployed flywheel to the pool

```typescript
// the pool's address
const comptrollerAddress = "0x...."

const tx = await sdk.addFlywheelCoreToComptroller(fwCore.address, comptrollerAddress, {
  from: deployer.address,
});
await tx.wait();
```

#### Step 3: Set up rewards for specific market and set its emission schedule

```typescript
// the market for which the LM campaign is enabled
const cTokenAddress = "0x..."

await sdk.addMarketForRewardsToFlywheelCore(
  fwCore.address, 
  cTokenAddress, 
  { from: deployer.address }
);

// Set the rewards duration and emission speed
await sdk.setStaticRewardInfo(
  fwStaticRewards.address,
  market.address,
  {
    rewardsEndTimestamp: 0,
    rewardsPerSecond,
  },
  { from: deployer.address }
);
```

#### Step 4: Fund the Flywheel with the tokens you'd like to emit

```typescript
import { ethers, Contract } from "ethers";
import { ERC20Abi } from "@midas-capital/sdk";


const rewardTokenContract = new Contract(
    rewardTokenAddress,
    ERC20Abi,
    deployer.address
)
await rewardTokenContract.transfer(
    fwStaticRewards.address, 
    ethers.utils.parseUnits("100", 18), 
    { from: deployer.address }
);

```

That's it! Now every time a user interacts with the specified market, the user will automatically accrue LM rewards.&#x20;

A full-fledged run-down to how these are used can also be found in our [tests for the SDK](https://github.com/Midas-Protocol/monorepo/blob/development/packages/sdk/tests/unit/FlywheelModule.spec.ts#L2).

## Querying Flywheels for Accrued Rewards

Running the liquidity mining campaign assumes also that pool operators can let users check the status of their rewards, how much has been accrued, and how much is claimable.&#x20;

This is also the case for markets for which a an [ERC-4626 strategy](../../guides/yield-bearing-vaults-erc-4626.md) exists. Basically, the Flywheel contracts and the Flywheel SDK module are your one-stop-shop for letting users introspect, claim, and interact with any yield-bearing operation.&#x20;

### `getFlywheelMarketRewardsByPoolWithAPR`

**Arguments:**

* `pool: string`: pool address (Comptroller) for which to query the rewards
* `options: { from: string }`: from address for which to query the rewards

**Returns:**

* `Promise<Array<`[`FlywheelMarketRewardsInfo`](api-reference-typing-and-interfaces.md#flywheelmarketrewardsinfo)`>>`





