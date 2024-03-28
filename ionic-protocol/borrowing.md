# Borrowing

To initiate a loan, borrowers must supply and enable asset as collaterall. This allows them to borrow in proportion to the value of their assets. \
\
**Important:** You cannot borrow the collateral asset (ie supply USDC and borrow USDC), this also goes for supplying and enabling several collateral assets (ie if you supply WETH, USDC, USDT and borrow USDC -> USDC will not be counted as collateral).\
\
**NOTE:** Max borrow button shows maximum amount you can borrow with the given collateral, however proceeding with max borrow will lead to liquidation.

### Liquidations&#x20;

If the collateral's value falls below the borrowed amount, the borrower's position is subject to liquidation. The borrow limit sets the risk threshold, and liquidation is triggered when this ratio surpasses the maximum Loan-to-Value (LTV) limit.&#x20;

However, if the loan value surpasses 70% of the collateral's value, a partial liquidation is initiated. In this scenario, liquidator bots receives a 15% liquidation incentive. They will liquidate up to 50% of the borrower's collateral. After deducting the liquidation incentive, the remaining amount is returned to the borrower, thereby restoring the borrower's health factor to a stable level.\
\
**NOTE:** as soon as the borrowing occurs, the interest rate is starting to accumulate, it is inadvisable to borrow maximum collateral limit.
