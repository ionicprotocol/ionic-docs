---
description: Borrowing crypto assets from Midas pools.
---

# Borrowing on Midas pools

**Step 1: Borrow Against Your Supplied Collateral**

Now that you have supplied assets, you have the opportunity to borrow assets in the same Midas pool. Users are constantly seen borrowing against their assets to gain leverage (borrowing stablecoins to buy more tokens) or borrowing to short an asset (selling an asset and buying it back at a later date), or even a chance to take out money against an appreciating asset that you do not wish to sell.

_Note: There is a significant amount of risk when borrowing assets, and you should do your own research and education before using this functionality_

1. Select the asset that you would like to borrow.
2. A new window will pop up on your screen displaying the current borrow APY and it will adjust based on the amount you type in.
3.  Now that the token has been selected and you have typed in your desired amount to borrow, click borrow and you are all done.

    _Note: this is a transaction that will cost gas._

**Step 2: Understanding Liquidation Health**

Cryptocurrency-based assets can be extremely volatile in price action, meaning your supplied amount can change rapidly (in USD value for example) which could cause the amount you can borrow to change abruptly based on price moments.

A _Liquidation_ is when your _Borrow Limit_ reaches its full capacity. Once this health bar (at the top of your dashboard) reaches 100%, your balances will be liquidated. This can come from collateral (supplied amount) dropping in value, or borrowed assets surging in value. When you get liquidated, a bot within the community will repay a percentage of your outstanding borrowed amount, as well as keeping a reward from your collateral based on the _liquidation incentive_ percentage found on each Midas pool's dashboard.

_Note: You should always do your own research regarding liquidations and find a safe haven for your health limit. When borrowing assets, you should consistently be checking the analytics monitor to avoid unforeseen liquidations._

_Note: You should be aware that sending your fToken (Midas Capital protocol ownership asset) to another wallet that is affiliated with a current borrowing position, you will be liquidated as the protocol does not see your collateral position anymore._

#### _**Example of an account that needs to be liquidated**_&#x20;

User A supplies $1m in ETH as collateral. $100k USDC borrowed and there is a $333k borrow limit based on the collateral factor of that specific pool.&#x20;

Now let’s say ETH collapses to 1/4th of its previous value. User A's collateral is now worth $250,000 and the borrow limit would be $83k USDC, but User A currently has $100k USDC borrowed. This account is under-collateralized and needs a liquidation to keep the pool solvent for the rest of the users.&#x20;

#### **Example of an account post liquidation**&#x20;

A liquidator bot will come in and repay some or all of your USDC debt (as much as necessary to bring the pool back to full solvency).&#x20;

For every $1 of your debt they repay, they get to take $1.12 of your collateral. This $0.12 bonus is defined as the liquidator incentive and is used to ensure the pool stays healthy. This amount is chosen by the pool creator and can be viewed on the details page of each Midas pool.

The liquidation mechanic is necessary to prevent the pool from going underwater, however, **most users will want to avoid being liquidated if possible.**\


{% hint style="info" %}
**Good to know:** your product docs aren't just a reference of all your features! use them to encourage folks to perform certain actions and discover the value in your product.
{% endhint %}
