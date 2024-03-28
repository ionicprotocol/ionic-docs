# Borrow

Borrow allows you to keep the exposure to the asset price movements and underlying yield if any. Thus obtaining free liquidity to execute a plethora of DeFi opportunities.&#x20;

## How to borrow?

To initiate a loan, borrowers must supply and enable asset as collateral (see [How to supply](supply-and-earn.md#how-to-supply)), on the same "Markets" page, choose the asset you would like to borrow and click on "Borrow/Repay" button. In the pop-up window choose the amount you want to borrow, and click "Borrow". After transaction goes through, you will have your borrowed asset.&#x20;

**NOTE:** Max borrow button shows maximum amount you can borrow with the given collateral (Loan-to-Value ratio for all the assets is 70%), however proceeding with max borrow will lead to [liquidation](https://app.gitbook.com/o/cXjAOr4ODBYcke19Ss5e/s/4L4EczL4rCp3jyJhAxHG/\~/changes/35/ionic-protocol/liquidations). Team advises not to borrow more than 80% from the available borrow-able amount, unless you are an experienced DeFi user.\
\
**Important:** You cannot borrow the collateral asset (ie supply USDC and borrow USDC), this also goes for supplying and enabling several collateral assets (ie if you supply WETH, USDC, USDT and borrow USDC -> USDC will not be counted as collateral).

## Position health

After the first borrow, head over to the "Dashboard" section to see the stats on your lending/borrowing, and 'Position Health'. 'Position Health' number shows you how close you are to a [liquidation](https://app.gitbook.com/o/cXjAOr4ODBYcke19Ss5e/s/4L4EczL4rCp3jyJhAxHG/\~/changes/35/ionic-protocol/liquidations), make sure to keep it above 1 (if it reaches 1 you will be partially [liquidated](https://app.gitbook.com/o/cXjAOr4ODBYcke19Ss5e/s/4L4EczL4rCp3jyJhAxHG/\~/changes/35/ionic-protocol/liquidations)).&#x20;

Make sure to check on your 'Position Health', as it will be gradually decreasing with time due to interest accrued, on top of that the market conditions can influence the value of your collateral which could also drop your 'Position Health'. In this case, be advised to partially repay your loan to balance out your position.

## How to repay?

Before repaying, you need to keep in mind the accrued interest on your borrow, the interest is paid in borrowed asset. Therefore to 'Max Repay' you need to have the amount borrowed + interest. Optionally you can partially repay your loan, in this case you will need just a part of the borrowed asset (partial repay can be used to increase your 'Position Health', or to allow you to withdraw part of the collateral, to later use it for full repayment).

Once you got interest figured out, head over to the "Markets" section and use the same "Borrow/Repay" button, then switch to the 'Repay' part of the pop-up window. Choose the amount you want to repay, either max repay (borrowed amount + interest) or partial repay (any amount). Once the the transaction goes through, you will see your borrow position disappear/decrease.
