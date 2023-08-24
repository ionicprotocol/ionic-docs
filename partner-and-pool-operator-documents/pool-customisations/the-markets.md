# The Markets

As a steward of your community, one of the main motivations behind using the Ionic will be the ability to have assets supported as collateral that other platforms do not support. Or if they do, they do so with a lesser capital efficiency or unappetising risk parameters.

As a pool operator, you’ll be able to design a pool form the ground up, starting from which markets your pool is composed of. See our section on [security](../../security/security-outline/) for an overview of what considerations need to be taken into account for an asset to be fully supported.

## Market Configuration

Customarily, a pool is composed is a set of two different asset types:

* Collateral assets (also known as _**protected**_ assets): the assets used to back up a loan, and cannot be borrowed
* Borrowable assets: usually in the form of blue-chip assets and stables, these are the assets that users borrow (though can also be used as collateral as well)

### Market Risk Factors

Each market has attached to it a set of customisable risk parameters. We do not expect every operator to have a deep knowledge of how such parameters should be set, and we’ll provide reasonable suggestions based on our team’s expertise as well as our risk-analysis frameworks.

#### Loan-to-Value (LTV)

The loan-to-value (LTV) ratio of an asset is a measure of the amount of financing that is provided for the asset compared to its value. It is calculated by dividing the amount of the loan by the value of the asset. For example, if a lender provides a loan of $100,000 to purchase an asset worth $200,000, the LTV ratio would be 50%.

#### **Supply Caps**

These are limits to how much of the collateral asset can be used in the money market. This parameter is designed to protect the pool against specific, long-tail volatile assets to damage the pool integrity.

For a variety of smaller capitalisation tokens with high fully-diluted valuations that are traded with thin liquidity, having the ability to supply an infinite amount of such token poses structural risks. Were the capitalisation of such token to vary significantly, it is likely that positions backed by such assets could no longer be liquidate-able, posing the risk of bad debt being incurred in the system.

#### Debt Ceilings

These are limits on the total borrow amount of a market that is collaterized by another specific asset in the pool. The cap is measured as an amount of the borrowed markets underlying tokens.

Similarly to Supply Caps, debt ceilings enable further granular risk management of certain collateral assets, by making sure that certain tail assets cannot be used to collateralise positions that are too large.

#### **Asset Blacklisting**

You can blacklist specific collateral assets from borrowing individual borrow assets in a pool. This decreases risk and reflexivity, enabling further isolation modes in pool.

For all intents and purposes, this is an extension of the Collateral Caps: It essentially sets a collateral cap to zero.

#### **Interest Rate Model**

The interest rate model is the graphical representation of the relationship between interest rates and the utilization of an asset in that market. It shows how the interest rate on a loan changes as the utilization of the loaned assets increases.

While most of the assets in a pool can be used with a standard interest model such as [Compound’s Jump Rate Model](https://ianm.com/posts/2020-12-20-understanding-compound-protocols-interest-rates), in many cases a pool might benefit from a specific asset to be borrowable with a tailored interest rate curve. See our [use-cases](../ionic-for-partners/) for some interesting case-studies of how our team developed a customised interest rate model for a specific asset.

#### Multiple Markets, Same Underlying

In the Compound model, each market is represented by a specific _underlying asset_: ETH, BTC, some Curve LP token, etc. These are assets that can be supplied or borrowed, and can have attached to them a plugin. Further, they can have a specific IRM and LTV.

This is however limiting! A specific Market can be configured in a variety of different manners, being more tailored to certain risk factors, and can also have different strategies attached to it. An example: a pool could offer a bare USDC market, that users can supply to or borrow from. However, Ionic also offer the possibility of integrating with Tier 1 pool, so that unused liquidity is deposited there, earning users extra yield. While Ionic could add such integration to all USDC markets, some pool operators might prefer having two separate markets, one with and one without the integration, so that users can choose whether to use a more complex market (and perhaps riskier). These separate markets can also have customisable IRMs, LTVs, etc., granting the pool operator further levels of customisations of their pool.

## Limitations & Security Considerations

As a permissioned protocol focused on security, the support for specific markets is subject to specific constraints. Let’s explore these.

1. Price Oracle availability A market needs to be able to price collateral and debt appropriately, in a reliable, censorship-free manner. This entails the existence of an on-chain feed for the price of such asset. Currently, Ionic supports natively the most extensive set of assets of any Money Market. It is very likely that yours is also supported:
   * Any Curve, Balancer, Uniswap V2-like, Wombat, and many other AMM LP tokens See our [oracle security docs](../../security/security-outline/oracle-security.md) for more information on how we develop, monitor, and circuit-break oracles to ensure their reliability.
   * Any asset that has any Uniswap V2 or V3 liquidity, via TWAPs or V3s internal price oracle
   * Any asset with a Chainlink, DIA, Flux, Pyth, Adrastia, or price feed
2. On-chain liquidity Protocol solvency is based on the ability to perform timely liquidations of collateral assets. Our team will perform strict liquidity analysis on the available liquidity pools for the desired assets, ensuring that every asset that is supported can be liquidated. See our [risk parameter setting docs](../../security/security-outline/) for more information on how these limits are calculated, and what precautions can be taken to ensure the protocol remains solvent, and our [monitoring docs](../../security/security-outline/liquidity-monitoring.md) for the tooling we have available to ensure on-chain liquidity profiles remain above desired security thresholds.

It is quite likely that most of the assets desired to be had in the pool will be natively supported by Ionic and will satisfy our security requirements. Where that not to be the case, we’ll get in touch with you to discuss how our engineering & BD team can develop a custom solution for your use-case, or put you in touch with the necessary stakeholders to get the requirements satisfied.

**NOTE:** The decision to support a pool at Ionic is ultimately subject to vetting by the Ionic team. Following a submission of a proposal for a pool, our team will identify its feasibility both in terms of engineering effort & risk analysis. Never hesitate to get in touch with us to discuss.
