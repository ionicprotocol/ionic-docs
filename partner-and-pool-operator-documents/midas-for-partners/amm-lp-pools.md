# AMM LP Pools

AMM’s interested in allowing users to borrow against their AMM LP tokens can create custom pools allowing the use of the LP tokens as collateral.

Once AMM LP tokens are deposited into a Midas pool, Midas’ ERC-4626 plugins stake the LP tokens in their respective staking contract so users can earn trading fees and farming yield while using their LP tokens as collateral.

Historically, if a user wanted to provide liquidity to an AMM, the user had no access to the liquidity in the LP token.

However, Midas pools enable users to borrow against these LP tokens so users can access the liquidity locked in their LP token and come up with a variety of strategies like leveraged yield farming, hedged positions, or delta-neutral.
