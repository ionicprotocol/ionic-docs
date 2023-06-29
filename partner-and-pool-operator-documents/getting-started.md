# Getting Started

### Process:

1. Reach out to Midas team (via [Discord](https://discord.gg/cddSv7ATcq) or [TG](https://t.me/midascapitaltg)) to discuss pool structure, setup, goals, etc.
   * **Key considerations:**
     * Pool Structure
       1. What should be used as collateral and at what LTV?
       2. What assets should be borrowable?
     * Asset Support
       1. Do assets need plugin support? (ie. use of yield bearing tokens like AMM LP tokens or vault tokens that need to be staked in another contract)
       2. Do the requested assets have reliable oracle infrastructure?
       3. How much liquidity is available to reliably liquidate a position? If liquidity depth is low, then supply caps may be needed.
     * Seed Liquidity
       1. How will you source seed liquidity into the pool? Some pool creators seed the liquidity themselves, while others use farming rewards to attract liquidity.
       2. Will you be using farming rewards to incentivize the pool?
     * Interest Rate Model (IRM)
       1. Do you want a custom interest rate model? Midas’ default IRM is the kink rate model so at what utilization (% borrowed vs supplied) do you want the kink to begin and what will the interest rate be at the kink?
2. Midas will provide feedback on pool design, structure, etc.
3. Once pool is finalized send pool setup fee to \[0x…]. This setup fee covers gas costs to deploy the pool and Midas’ labor hours to get the pool set up.
4. After the pool has been set up by Midas, the team will deliver the pool back to you – you can decide whether you want to take ownership of the pool or leave the pool with Midas for updates and changes.
5. Seed the pool with liquidity and partner with Midas to co-promote the pool. Typical promotional campaigns include a Medium article and a Twitter post.

