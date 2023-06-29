# The Yield

### The Problem: Yield vs Liquidity

What if instead of just being able to take loans on a specific token, users could also earn unparalleled yield on those tokens? Usually, users of DeFi find themselves having to choose how to allocate their capital in conflicting manners — taking a loan on an asset means locking it into a borrowing and lending pool and forgoing the ability to earn passive income on it (or at the very least, earning far less yield than some other more attractive yield opportunity). At the core of this issue is the inability to use capital in an efficient manner due to technical limitations of most money markets.

### The Solution: ERC4626 Yield-bearing Strategies

With Midas, this limitation vanishes: built with the novel [ERC4626 standard in mind](https://medium.com/midas-capital/an-introduction-to-the-erc-4626-tokenized-vault-standard-with-infographic-cd814c00201f), the money markets at Midas capital come with the native ability to pair any market with an arbitrary strategy, allowing completely re-imagined levels of capital efficiency and yield possibilities.

As a partner interested in offering your users novel financial instruments, this standard allows the combination of liquidity provision of assets without the need to forgo the ability to collateralise such assets.

#### **Example Use-Case: Improved AMM liquidity provision**

[Ellipsis Finance](https://ellipsis.finance/) is a curve-like protocol where users can provide liquidity to a variety of pools, receiving LP tokens back as a “receipt” of their liquidity. While these tokens already earn trading fees on their own, they can be staked in a variety of other yield aggregator platforms (Beefy Finance, Dot Dot Finance).

However, once in these platforms, they no longer become liquid: they can’t be used anywhere else. At Midas Capital, we built integrations with yield aggregators such that users can deposit their LP tokens on Midas, have them automatically staked into they yield aggregator platforms, while at the same time being able to borrow against them. You (and your users!) can have your cake and eat it (too).

### Developing ERC4626 Strategies At Midas Capital

At Midas Capital, we’ve built a set of strategies that target the most prominent yield aggregator platforms & protocols. Examples of these are:

* Beefy Finance
* DotDot Finance
* Wombex Finance
* AAVE V3
* Curve Gauges

And many others. While we’ve already built a healthy number of strategies, we also understand that each protocol might have specific requirements and strategies they'd like to use. Visit our [Premium Support](../slas-and-premium-support.md) for an overview of how you can work together with us to get custom integrations built for your use-case.&#x20;
