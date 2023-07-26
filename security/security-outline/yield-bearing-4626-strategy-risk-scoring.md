# Yield Bearing 4626 Strategy Risk Scoring

## Introduction

ERC-4626 was created to allow DeFi protocol developers to use a standard when creating yield strategies across multi-asset, multi-chain configurations. However, there are inherent risks to using Vaults that users should be aware of, including but not limited to:

* Use of plugins could result in Ionic pool risk, along with underlying protocol risk
* Impermanent loss due to the pool’s token price volatility
* Liquidity issues in riskier token pairs

We've implemented a risk scoring framework for 4626 strategies aimed at giving users a better understanding of the risks associated with their usage.

A 4626 strategy will have assigned a particular score in the rage 0-10, based on the following aspects, each having a specific weight towards the score.

While the specifications are defined here, the implementation is completely open sourced in our monorepo, in the `security package`

Many thanks to the folks at Beefy Finance for the inspiration on the specification hereby used, as ours is heavily inspired by theirs.

* [Ionic Risks (20%)](yield-bearing-4626-strategy-risk-scoring.md#category-ionic-risks)
  * [Complexity](yield-bearing-4626-strategy-risk-scoring.md#subcategory-complexity)
  * [Time in the Market](yield-bearing-4626-strategy-risk-scoring.md#subcategory-time-in-market)
* [Asset Risks (20%)](yield-bearing-4626-strategy-risk-scoring.md#category-asset-risks)
  * [Impermanent Loss](yield-bearing-4626-strategy-risk-scoring.md#subcategory-impermanent-loss)
  * [Liquidity](yield-bearing-4626-strategy-risk-scoring.md#subcategory-liquidity)
  * [Market Cap](yield-bearing-4626-strategy-risk-scoring.md#subcategory-market-cap)
* [Platform Risks (60%)](yield-bearing-4626-strategy-risk-scoring.md#category-platform-risks)
  * [Reputation](yield-bearing-4626-strategy-risk-scoring.md#subcategory-reputation)
  * [Security](yield-bearing-4626-strategy-risk-scoring.md#subcategory-security)

## Category: Ionic Risks

These are risks related to the Ionic platform itself. These could be risks added by the complexity of the vault strategy, if it's an experimental deployment, if it's been audited by others, etc. Twenty percent of the safety score is determined by this category.

### Subcategory: Complexity

Tracks the complexity of the 4626 strategy

#### **COMPLEXITY\_LOW**

* Title: Low complexity strategy
* Explanation: Low complexity strategies have few, if any, moving parts and their code is easy to read and debug. There is a direct correlation between code complexity and implicit risk. A simple strategy effectively mitigates implementation risks.
* Qualification Criteria: A low complexity strategy should interact with just one audited and well-known smart contract e.g. MasterChef. The strategy serves as a façade for this smart contract, forwarding deposit, harvest and withdrawal calls using a single line of code.

#### COMPLEXITY\_MID

* Title: Ionic strategy is of medium complexity
* Explanation: Medium complexity strategies interact with two or more audited and well-known smart contracts. Its code is still easy to read, test and debug. It mitigates most implementation risks by keeping things simple, however the interactions between 2 or more systems add a layer of complexity.
* Qualification Criteria: A medium complexity strategy interacts with 2 or more well-known smart contracts. This strategy automates the execution of a series of steps with no forking paths. Every time deposit(), harvest() and withdraw() is called, the same execution path is followed.

#### COMPLEXITY\_HIGH

* Title: Ionic strategy is complex
* Explanation: High complexity strategies interact with one or more well-known smart contracts. These advanced strategies present branching paths of execution. In some cases multiple smart contracts are required to implement the full strategy.
* Qualification Criteria: A high level complexity strategy can be identified by one or more of the following factors: high cyclomatic complexity, interactions between two or more third-party platforms, implementation split between multiple smart contracts.

### Subcategory: Time in Market

Tracks how long has this strategy been running without any major issues.

#### BATTLE\_TESTED

* Title: Ionic strategy is battle tested
* Explanation: The more time a particular strategy is running, the more likely that any potential bugs it had have been found, and fixed. This strategy has been exposed to attacks and usage for some time already, with little to no changes. This makes it sturdier.
* Qualification Criteria:
  * 10+ strategies sharing the same code deployed
  * 3 months working as expected without upgrades

#### NEW\_STRAT

* Title: Strategy has been running for less than a month
* Explanation: The more time a particular strategy is running, the more likely that any potential bugs it has have been found, and fixed. This strategy is a modification or iteration of a previous strategy. It hasn't been battle tested as much as others.

#### EXPERIMENTAL\_STRAT

* Title: The strategy has some features which are new
* Explanation: The more time a particular strategy is running, the more likely that any potential bugs it had have been found, and fixed. This strategy is brand new and has at least one experimental feature. Use it carefully at your own discretion.

## Category: Asset Risks

Risks relating to the asset or assets handled by the vault. Entering into a vault with BTC has a different set of risks than entering into a vault with a newer and smaller coin. Twenty percent of the score is determined by this category.

### Subcategory: Impermanent Loss

Tracks the risk of impermanent loss within the vault

#### IL\_NONE

* Title: Very low or zero projected IL
* Explanation: The asset in this vault has very little or even no expected impermanent loss. This might be because you are staking a single asset, or because the assets in the LP are tightly correlated like USDC-USDT or WBTC-renBTC.
* Qualification Criteria: Single asset vaults and vaults that manage stablecoins with a peg that isn't experimental: USDT, USDC, DAI, sUSD, etc.

#### IL\_LOW

* Title: Low projected IL
* Explanation: When you are providing liquidity into a token pair, for example ETH-BNB, there is a risk that those assets decouple in price. BNB could drop considerably in relation to ETH. You would lose some funds as a result, compared to just holding ETH and BNB on their own. The assets in this vault have some risks of impermanent loss.
* Qualification Criteria: Vaults that handle what are normally referred as “Pool 1” LPs would fit here: ETH-USDC, MATIC-AAVE, etc. Governance tokens for smaller projects are normally known as “Pool 2” and thereby excluded.

#### IL\_HIGH

* Title: High projected IL
* Explanation: When you are providing liquidity into a token pair, for example ETH-BNB, there is a risk that those assets decouple in price. BNB could drop considerably in relation to ETH. You would lose some funds as a result, compared to just holding ETH and BNB on their own. The assets in this vault have a high or very high risk of impermanent loss.
* Qualification Criteria: Vaults that handle “Pool 2” LPs go here. These LP normally include the governance token of the farm itself.

### Subcategory: Liquidity

Tracks how difficult it is to buy/sell the vault's token.

#### LIQ\_HIGH

* Title: High trade liquidity
* Explanation: How liquid an asset is affects how risky it is to hold it. Liquid assets are traded in many places and with good volume. The asset held by this vault has high liquidity. This means that you can exchange your earnings easily in plenty of places.

#### LIQ\_LOW

* Title: Low trade liquidity
* Explanation: How liquid an asset is affects how risky it is to hold it. Liquid assets are traded in many places and with good volume. The asset held by this vault has low liquidity. This means that it isn't as easy to swap and you might incur high slippage when doing so.

### Subcategory: Market Cap

Total value of all the coins in circulation. Indirectly tracks how volatile the vault's underlying asset is.

#### MCAP\_LARGE

* Title: High market cap, low volatility asset
* Explanation: The market capitalization of the crypto asset directly affects how risky it is to hold it. Usually a small market cap implies high volatility and low liquidity. The asset held by this vault has a large market cap. This means it's potentially a highly safe asset to hold. The asset has a high potential to stick around and grow over time.
* Qualification Criteria: Top 50 MC by Gecko/CMC

#### MCAP\_MEDIUM

* Title: Medium market cap, medium volatility asset
* Explanation: The market capitalization of the crypto asset directly affects how risky it is to hold it. Usually a small market cap implies high volatility and low liquidity. The asset held by this vault has a medium market cap. This means it's potentially a safe asset to hold. The asset has potential to stick around and grow over time.
* Qualification Criteria: Between 50 and 300 MC by Gecko/CMC

#### MCAP\_SMALL

* Title: Small market cap, high volatility asset
* Explanation: The market capitalization of the crypto asset directly affects how risky it is to hold it. Usually a small market cap implies high volatility and low liquidity. The asset held by this vault has a small market cap. This means it's potentially a risky asset to hold. The asset has low potential to stick around and grow over time.
* Qualification Criteria: Between 300 and 500 MC by Gecko/CMC

#### MCAP\_MICRO

* Title: Micro market cap, Extreme volatility asset
* Explanation: The market capitalization of the crypto asset directly affects how risky it is to hold it. Usually a small market cap implies high volatility and low liquidity. The asset held by this vault has a micro market cap. This means it's potentially a highly risky asset to hold. The asset has low potential to stick around.
* Qualification Criteria: +500 MC by Gecko/CMC

### Subcategory: Supply

Tracks risks related to the asset supply. Can it be altered by anyone? How centralised is it?

#### SUPPLY\_CENTRALIZED

* Title: Few very powerful whales
* Explanation: When the supply is concentrated in a few hands, they can greatly affect the price by selling. Whales can manipulate the price of the coin. The more people that have a vested interest over a coin, the better and more organic the price action is.
* Qualification Criteria: Less than 50 accounts hold more than 50% of the supply.

## Category: Platform Risks

Risks relating to the third party platforms used by the vault. How much track record they have, how solid the code is, are there any dangerous actions that an admin can take, etc. Sixty percent of the score is determined by this category.

### Subcategory: Reputation

Tries to give clues about the team and community's track record. How likely are they to rug for example.

#### PLATFORM\_ESTABLISHED

* Title: The platform has a known track record
* Explanation: When taking part in a farm, it can be helpful to know the amount of time that the platform has been around and the degree of its reputation. The longer the track record, the more investment the team and community have behind a project. This vault farms a project that has been around for many months.
* Qualification Criteria: The underlying farm has been around for at least 3 months.

#### PLATFORM\_NEW

* Title: Platform is new with little track record
* Explanation: When taking part in a farm, it can be helpful to know the amount of time that the platform has been around and the degree of its reputation. The longer the track record, the more investment the team and community have behind a project. This vault farms a new project, with less than a few months out in the open.
* Qualification Criteria: The underlying farm has been around for less than 3 months.

### Subcategory: Security

Tracks various smart contract good practices.

#### NO\_AUDIT

* Title: The platform has never been audited by third-party trusted auditors
* Explanation: Audits are reviews of code by a group of third party developers.

#### AUDIT

* Title: The platform has an audit from at least one trusted auditor
* Explanation: Audits are reviews of code by a group of third party developers.
* Qualification Criteria: One or more audits from an auditor that has some positive track record in the space.

#### CONTRACTS\_VERIFIED

* Title: All relevant contracts are publicly verified
* Explanation: Code running in a particular contract is not public by default. Block explorers let developers verify the code behind a particular contract. This is a good practice because it lets other developers audit that the code does what it’s supposed to. All the third party contracts that this vault uses are verified. This makes it less risky.

#### CONTRACTS\_UNVERIFIED

* Title: Some contracts are not verified
* Explanation: Code running in a particular contract is not public by default. Block explorers let developers verify the code behind a particular contract. This is a good practice because it lets other developers audit that the code does what it’s supposed to. Some of the third party contracts that this vault uses are not verified. This means that there are certain things that the Midas devs have not been able to inspect.

#### ADMIN\_WITH\_TIMELOCK

* Title: Dangerous functions are behind a timelock
* Explanation: Sometimes the contract owner or admin can execute certain functions that could put user funds in jeopardy. The best thing is to avoid these altogether. If they must be present, it’s important to keep them behind a timelock to give proper warning before using them. This contract has certain dangerous admin functions, but they are at least behind a meaningful Timelock.
* Qualification Criteria: There is at least one function present that could partially or completely rug user funds. The function must be behind a +6h timelock.

#### ADMIN\_WITHOUT\_TIMELOCK

* Title: Dangerous functions are without a timelock
* Explanation: Sometimes the contract owner or admin can execute certain functions that could put user funds in jeopardy. The best thing is to avoid these altogether. If they must be present, it’s important to keep them behind a timelock to give proper warning before using them. This contract has certain dangerous admin functions, and there is no time lock present. They can be executed at a moment's notice.
* Qualification Criteria: There is at least one function present that could partially or completely rug user funds. The function has no time lock protection.
