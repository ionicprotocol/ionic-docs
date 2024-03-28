---
description: Liquidity availability is at the core of a secure protocol.
---

# Liquidity Monitoring

### Liquidity and Protocol Solvency

The solvency of a borrowing and lending protocol hinges on the ability with which it can perform liquidations, and with which it can price assets in a fair-market manner. While the latter hinges heavily on the [security of the oracles](oracle-security.md), the former is heavily dependent on a variety of factors:

* The willingness of external actors to constantly monitor open positions, and liquidate as they go under water
* The ability to perform such liquidations, either with capital of their own, or with flash loans

At Ionic, our liquidation system is currently permissionless, and any actor is incentivised to take part in it and potentially profit from the _liquidation incentive_ granted to liquidators.

We must guarantee the liquidate-ability of each and every position.&#x20;

### Liquidity Monitoring at Ionic

While our liquidation system is flexible enough to be able to use a variety of different liquidity pools as sources for liquidations, it is important that such liquidity pools would be able to withstand any liquidation event. In particular, the aggregated liquidity of all the pools for a specific asset should be higher than the total borrowable value of such asset, and the largest liquidity pool should have enough depth to withstand a trade of the largest borrow position with minimal slippage. This usually means a [full-range liquidity](https://support.uniswap.org/hc/en-us/articles/7423608592781-Can-I-provide-liquidity-over-the-full-range-on-V3-) of 2-5 times larger than the largest possible borrowable position.

To ensure these requirements are met, we at Ionic developed a custom liquidity monitoring solution with the goal of mitigating the situation in which protocol solvency could be at-risk. The methodology by which such system operates is by preventing market operations on markets for which on-chain liquidity is not enough to perform liquidations or sustain an oracle attack.

### **Actions**

**Liquidity drainage**

In the event of a large drop in liquidity in any of the liquidity sources, pause market operations for the asset in question and the borrowable assets in the protocol with such asset. In particular, this will have the following effects on the protocol

* Prevent any further borrowing of any assets
* Prevent any further minting of new collateral for the asset in question

This will however still allow users to repay their debts and withdraw liquidity from the pool

**Detected Dangerous Liquidity Concentration**

Liquidity concentration is a risk vector for a liquidity pool. If the liquidity is concentrated into very few wallets, the changes of such liquidity being removed immediately is higher than if spread across multiple small holders.

Our monitors will issue alerts if a critical level of concentration is detected. Namely, it will issue an alert if the top holder of the liquidity pool holds enough liquidity that, if removed, it would cause the available liquidity to drop below our specified thresholds.
