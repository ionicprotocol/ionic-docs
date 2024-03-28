---
description: Overview of the core pieces of Ionic's Infrastructure
---

# Oracles

### What is an oracle?

```
Blockchain oracles are entities that connect blockchains to external systems, thereby enabling smart contracts to execute based upon inputs and outputs from the real world.[1]
```

Within the context of borrowing and lending, oracles are an essential part of the infrastructure. In particular, Oracles are needed to correctly _price_ an asset, as asset prices are not directly available on the blockchain.

Ionic utilizes the decentralized [RedStone](https://redstone.finance/) and [Pyth oracles](https://pyth.network/) as a primary source of untamperable and up-to-date token price data to smart contracts on Mode Network.

### Oracle Types

* Oracle Providers: oracles that are based on 2+ sources (such as RedStone price feeds), these are price feeds given by aggregators that generally query a disparate set of data sources to arrive at a price feed
* UniswapV2 oracles: as long as they pass a specific liquidity threshold (defined per-asset, based on total available on-chain liquidity of that asset), and implement a time-weighted moving average of at least the last 10 observations
* UniswapV3 oracles: as long as their cost of attack exceeds the total available pool liquidity by a factor of 2
* Combined price feeds: for exotic tokens, such as LP tokens, fair pricing models exist and have been extensively validated. As long as price feeds for the underlying assets of such LPs are secure, LP tokens from a variety of different sources can be safely calculated. This does mean however that the manipulation risk is combined each asset’s manipulability. We take this into account when evaluating such oracles.
