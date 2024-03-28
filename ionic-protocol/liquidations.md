# Liquidations

If the collateral's value falls below the borrowed amount, the borrower's position is subject to liquidation. The borrow limit sets the risk threshold, and liquidation is triggered when this ratio surpasses the maximum Loan-to-Value (LTV) limit, which is 70%.&#x20;

If the loan value surpasses 70% of the collateral's value, a partial liquidation is initiated. In this scenario, liquidator bots receives a 15% liquidation incentive. They will liquidate up to 50% of the borrower's collateral. After deducting the liquidation incentive, the remaining amount is returned to the borrower, thereby restoring the borrower's position health to a stable level.\
\
**NOTE:** as soon as the borrowing occurs, the interest rate is starting to accumulate, it is inadvisable to borrow maximum collateral limit.
