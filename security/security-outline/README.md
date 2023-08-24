# Security Outline

**The goal of the Ionic protocol is to act as a shelling point for companies, DAOs and other protocols, delivering standardized and secure infrastructure for DeFi use cases such as isolated pools, yield strategies and staking.**

For this vision to become a reality, security is of the highest importance and at the heart of all decisions made by the team. A few of the tenants of our security philosophy:

#### **“Slow and steady”**

The paradigm around DeFi has always been “build fast and break things”. At Ionic, we want to be a protocol that is around for a long time in the future. We are willing to sacrifice speed of onboarding pools and assets in order to ensure everything we ship is robustly tested and verified.

#### **Review of partners**

We strive to work with high quality partners who share the same thoughts around security that we do. We go through a stringent review process to onboard partners and make it very clear that security is the utmost priority in our relationship.\
\
The core of our philosophy around security is to build from a stable foundation. We believe that moving more intentionally and not chasing every opportunity lets us focus on the core strengths of the protocol. Teams working on similar designs have failed to achieve long term success in the past, when growth of the system turned exponential without having the adequate strategies in place to deal with the increase in complexity. Security practices have to be automated as much as possible to handle the plethora of assets that can be plugged into the protocol. DeFi applications inherently deal with many attack vectors, so aiming for sustainable growth is the best insurance policy for the longevity of a project.

#### Permissioned creation

Tier 2 or 3 pool can only be created by Ionic after thorough investigation and set up of price oracle, pool parameters and other customisation options. Once done, the ownership of the pool will transfered to the partnering entity.

### **Broadly there are three main areas of risk for users interacting with the protocol:**

**1.** The risk of onboarding assets and pricing them correctly. These risks mainly affect the economic security of individual pools and assets need to be carefully monitored and selected.

\
Learn more about Ionic approach to these so called Oracle Risks [here](oracle-security.md).\
\
**2.** Smart Contract risk of the Ionic Core contracts and the Ionic SDK/FE. These risks are mainly a consequence of code quality and engineering processes. The main mitigation factors are extensive internal testing infrastructure, usage of battle tested and standardized code wherever possible and external code audits.

\
Learn more about Ionic engineering practices [here](../../developers/ionic-sdk/), and about our risk-scoring framework for ERC4626 strategies [here](yield-bearing-4626-strategy-risk-scoring.md).\
\
**3.** Pool Operator risk of the independent operators using underlying Ionic contracts. These risks are mostly centered around keeping bad actors from abusing the system. Mitigation mechanisms are the permissioning of the oracle creation process and the B2B approach of the Ionic to work very closely with our partners.

