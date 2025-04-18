# Glossary

### **Yield-bearing Token**

Yield-bearing Token is a general term referring to any token that can generate yield or has potential yield. Examples include Stone, slisBNB, stETH, Blast ETH, GLP, LP liquidity tokens, and so on.

### **Underlying Asset Token**

Underlying Asset Token refers to the underlying asset token of a Yield-bearing Token. For example, the Underlying Asset Token for Stone, stETH, and rETH is ETH.

### **SY = Standardized Yield Token**

SY is a vault token based on the [ERC5115](https://eips.ethereum.org/EIPS/eip-5115) standard designed to encapsulate yield-bearing tokens. It can wrap any yield-bearing token and provides a standardized interface for interacting with the yield-generating mechanisms of any yield-bearing token.

In OutStake, staking SY and specifying a lock-up period will mint three types of tokens: **PT (Principal Token)**, **YT (Yield Rate Token)** and **SP (Staking Position)**.

### **PT = Principal Token**

PT is a component of the principal split from yield-bearing tokens. PT tokens can be wrapped into SP or used independently. Holding PT or SP signifies ownership of the principal, and upon the expiration of the locked position period, the principal portion of the yield-bearing tokens can be redeemed.

Unlike other protocols, OutStake's PT is a standard ERC20 token with no expiration date. When staking for different durations of SY, the same PT token is minted, but the quantity minted will vary slightly depending on the staking period. Each yield-bearing token will have a corresponding PT token.

### **UPT = Omnichain Universal Principal Token**

UPT is an omnichain universal principal token supported by the **LayerZero** protocol. Unlike a unique principal token (PT) corresponding to each specific yield-bearing token, UPT is backed by multiple yield-bearing tokens supported by the same underlying asset. When staking and locking positions, users can choose to mint UPT or a standard PT. For example, staking Stone, wstETH, or BETH allows users to opt for minting UETH. The protocol will manage which yield-bearing tokens can be staked and locked to mint corresponding UPT through a whitelist, preventing security issues arising from potential abuse.

It’s worth noting that **choosing to mint UPT instead of a standard PT means forgoing potential future Points rewards from external protocols**, as these Points rewards are managed off-chain by various external protocols.

### **YT = Yield Rate Token**

YT is the component of yield that is separated from yield-bearing tokens. Holding YT represents your ownership of all the yield generated by the underlying assets, and you can redeem the accumulated yield in the current yield pool at any time by burning YT.

Unlike other protocols, OutStake's YT is a universal ERC20 token with no expiration date, and YTs minted from different staking times are the same token (with the same token contract address). Unlike UPT, each type of Yield-bearing Token mints a corresponding YT.

The redeemable value of YT (the yields obtained by burning YT) starts at 0. Over time, the yield pool accumulates yields  from the staked assets, causing the redeemable value of YT to continuously increase. Eventually, it will surpass the yield rate of the yield-bearing token itself and will fluctuate based on market behavior.

### **SP = Staking Position**

SP is a token based on the [ERC6909](https://eips.ethereum.org/EIPS/eip-6909) standard used to encapsulate staked positions. Holding SP represents ownership of the principal redemption rights for a locked staked position upon maturity. Users can encapsulate PT (or UPT) tokens to mint transferable SP tokens and then sell them, effectively completing a "redemption" operation before the SP lock-up period expires. After the SP lock-up period ends, users can burn the SP tokens to redeem the principal portion of the staked yield-bearing tokens. Since SP adheres to the ERC6909 standard, it supports partial encapsulation and redemption of positions.

SP records the staked quantity of yield-bearing tokens in the locked position, a fixed principal value, and the minted PT (or UPT) quantity. Therefore, after the lock-up period expires, the principal value redeemed by burning SP tokens is fixed. This creates a fixed yield rate based on its trading price and transaction timing, allowing holders of SP to earn fixed-rate yields based on the underlying asset.

It’s worth noting that if the initial owner of the locked position does not mint SP tokens, they can directly burn the PT (or UPT) tokens upon maturity to redeem the principal portion of the locked position.

### **PYT = Points Yield Token**

PYT is a component of the external protocol points yields derived from splitting interest-bearing tokens. PYT is also a token based on the ERC6909 standard, and holding PYT signifies ownership of all external protocol points yields generated by the corresponding locked position.

When staking and locking yield-bearing tokens to mint PT/YT, PYT is minted simultaneously. However, it’s important to note that not all external protocols have points incentive programs, and these programs may change with the external protocols. This means the value of PYT could potentially be zero, with the final interpretation rights belonging to the external protocols, not Outrun.

Additionally, if users choose to mint UPT when locking staked interest-bearing tokens, PYT will not be minted, meaning they forfeit any potential future or existing external points yields.
