# Advanced Features

## Liquidity Mining

### Direct Pool Incentives

Pool Creators can incentivize the pool by running liquidity mining campaigns to distribute rewards to Depositors or Borrowers in the pool. Custom flywheels can be set up enabling Pool Creators to set duration of the liquidity mining campaign and the distribution speed of any liquidity mining rewards.

### Pass Through Incentives from Yield-Bearing Collateral

The Midas platform allows for yield-bearing assets such as AMM LP tokens and yield aggregator vault tokens as collateral. Many of these yield-bearing earn part of their yield from liquidity mining incentives. When depositing yield-bearing assets into Midas pools, the Midas platform will stake these assets into their respective yield-bearing staking contracts so users can continue to earn these farming rewards while using their assets as collateral.

## Alerting

### Oracle Monitoring

Midas uses a wide variety of oracles to be able to deliver the customizability and wide range of available assets in our pools. All our oracles are chosen deliberately and only in used in production, if they can be designed in a flash loan resistant way.

To make sure all our oracles function flawlessly at all times, we have developed a set of monitors with these features:

* Monitors the heartbeat of all oracles, to check if any went stale
* Monitors if the price of an oracle changes by an unnatural percentage within a time period These monitors will be integrated into a circuit breaker system that automatically shuts down borrowing inside a pool, if certain conditions are triggered.

### Liquidity Monitoring

Liquidity is one of the most important metrics for assessing the usability of an asset as collateral on Midas. Liquidity can be quickly changing in a volatile market environment and needs to be constantly monitored to keep pool parameters in a safe range.

Midas has developed a set of off chain liquidity monitors with the following features:

* Monitors on chain liquidity for all popular DEXes (Uni V2/V3, Curve, Balancer, etc.)
* Monitors TVL of DEX LPs
* Monitors liquidity imbalances in Curve LPs
* Monitors liquidity distribution of LPs in a pool

These monitors can be easily integrated with automated system that can trigger certain actions within pools, as well as an altering system, that informs pool creators or users of sudden changes in liquidity.
