---
description: Liquidity availability is at the core of a secure protocol
---

# Liquidity Monitoring

### Liquidity and Protocol Solvency

The solvency of a borrowing and lending protocol hinges on the ability with which it can perform liquidations, and with which it can price assets in a fair-market manner. While the latter hinges heavily on the [security of the oracles](oracle-security.md), the former is heavily dependent on a variety of factors:

* The willingness of external actors to constantly monitor open positions, and liquidate as they go under water
* The ability to perform such liquidations, either with capital of their own, or with flash loans

At Midas Capital, our liquidation system is currently permissionless, and any actor is incentivised to take part in it and potentially profit from the _liquidation incentive_ granted to liquidators.&#x20;

However, due to the nature of Midas Capital and our inherent focus assets that are commonly not supported in other protocols, we must take extra steps to guarantee the liquidate-ability of each and every position. This is because some of the supported assets do not have deeply liquid markets, or if they do, they are not centralised around a single AMM.&#x20;

### Liquidity Monitoring at Midas Capital

While our liquidation system is flexible enough to be able to use a variety of different liquidity pools as sources for liquidations, it is important that such liquidity pools would be able to withstand any liquidation event. In particular, the aggregated liquidity of all the pools for a specific asset should be higher than the total borrowable value of such asset, and the largest liquidity pool should have enough depth to withstand a trade of the largest borrow position with minimal slippage. This usually means a [full-range liquidity](https://support.uniswap.org/hc/en-us/articles/7423608592781-Can-I-provide-liquidity-over-the-full-range-on-V3-) of 2-5 times larger than the largest possible borrowable position.

To ensure these requirements are met, we at Midas Capital developed a custom liquidity monitoring solution with the goal of mitigating the situation in which protocol solvency could be at-risk. The methodology by which such system operates is by preventing market operations on markets for which on-chain liquidity is not enough to perform liquidations or sustain an oracle attack.

### Approach

For small capitalisation tokens for which the price oracle depends on such liquidity, a sudden drop in liquidity should pause all market operations in pools that support that token

We assume that the initial liquidity is enough for sustaining liquidations and a manipulation-resistant price oracle. This must be ensured by due diligence performed at the time we support an asset

### **Actions**

**Liquidity drainage**

In the event of a large drop in liquidity in any of the liquidity sources, pause market operations for the asset in question and the borrowable assets in the pool with such asset. In particular, this will have the following effects on a pool

* Prevent any further borrowing of any assets
* Prevent any further minting of new collateral for the asset in question

This will however still allow users to repay their debts and withdraw liquidity from the pool

**Detected Dangerous Liquidity Concentration**&#x20;

Liquidity concentration is a risk vector for a liquidity pool. If the liquidity is concentrated into very few wallets, the changes of such liquidity being removed immediately is higher than if spread across multiple small holders.&#x20;

Our monitors will issue alerts if a critical level of concentration is detected. Namely, it will issue an alert if the top holder of the liquidity pool holds enough liquidity that, if removed, it would cause the available liquidity to drop below our specified thresholds.&#x20;

In many cases, pool owners and partner projects are the ones providing large part of the liquidity. In such cases, the incentives of maintaining such liquidity are aligned between Midas and the holder of liquidity, so risks are mitigated.  If you are a pool owner or partner project, [get in touch with us](broken-reference) to whitelist the address holding the liquidity, so that our monitors are ensured about&#x20;

### Currently Monitored Pools

We maintain an up-to-date list of currently monitored pools for internal usage. You can find it in the following link:

* [Monitored Pools](https://spiky-enemy-a6e.notion.site/68bfcae0448e45eab646276c13d87b05?v=9b46a25ec40140309cb39c7914ec7ba0)

If you'd like to receive alerts, or have a specific pool monitored, please [get in touch with us](broken-reference).

