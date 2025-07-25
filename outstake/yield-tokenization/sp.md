---
description: Staking Position
---

# SP

The **Staking Position (SP)** token represents **the redemption right of the principal for a locked position upon maturity**. Supported by the [ERC-6909](https://eips.ethereum.org/EIPS/eip-6909) standard, it enables users to transfer partial redemption rights of their position. Holders can sell their SP, effectively achieving a "pre-redemption" operation. The SP contract records the immutable metadata of the position, including the **SY staking amount, constant principal value, SP minted amount, lock-up expiration time, whether it's in UPT mode, and more**.

### Underlying Mechanism

1. **Staking:** Users stake their **SY tokens** and choose whether to enable **UPT  mode**.
2. **Minting:** Staking will result in the 1:1 minting of **transferable SP (Staking Position) tokens** based on the value of the SY token relative to its accounting asset. For example, if 1 SY-wstETH = 1.1 ETH, staking 1 SY-wstETH will mint 1.1 SP-wstETH.
3. **Splitting:** Users can split their **SP tokens** into **PT(UPT)** according to the **position's mode** (which is unchangeable). This operation makes the original SP non-transferable but does not destroy it, allowing it to still be tracked.
   * **If the position is in non-UPT mode:** SP tokens can be split into PT on a 1:1 basis.
   * **If the position is in UPT mode:** the amount of UPT split is also related to the staking duration (i.e., the amount of YT minted). The specific calculation method is as follows:

<p align="center"><span class="math">\text{SP Quantity} = \text{SY Accounting Value} - (\text{YT Quantity} \times \text{YT Redeemable Value})</span></p>

3. **Synthesizing:** Users retain the right to burn their **PT(UPT)** at any time. This operation will synthesize the PT(UPT) with the non-transferable SP back into the original transferable SP.

After the position's lock-up period expires, **a fixed quantity of transferable SP can be burned to redeem a corresponding fixed quantity of the yield-bearing token's principal for that position**. This mechanism allows for the formation of varying fixed interest rates based on market prices and the lock-up expiration time. By holding transferable SP, you can earn fixed interest rate yields denominated in the accounting asset.

In general, Yield-bearing Tokens can be roughly classified as follows:

1. **Rebase Tokens** - Tokens that increase their balance over time.

_Examples: stETH, aUSDC_

2. **Yield-bearing Non-Rebase Tokens** - Tokens that appreciate in value over time.

_Examples: wstETH, Stone, slisBNB_

**It is important to note**: For reward-bearing non-rebase Yield-bearing Tokens, the quantity of staked Yield-bearing Tokens in the position does not change after the lock-up period expires. However, their value (relative to the **account asset token**'s exchange ratio) will increase with the accumulation of yields. Thus, burning PT does not redeem the same quantity of non-rebase Yield-bearing Tokens as initially staked, instead, it will be slightly less because part of the value is attributed to YT.

### SP Trading Market

Building an **SP (Staking Position) trading market** comes with a very interesting characteristic: even though SP is an ERC-6909 standard token, its trading market doesn't require proactive market making. This is because the nature of SP inherently gives any SP trading market **AMM-like properties**.

Users trade SP to obtain a **fixed interest rate**. This fixed interest rate, at a given listed price, will automatically increase as the token approaches its lock-up expiration time. This means that any SP trading market inherently possesses a **price discovery mechanism**. Users will purchase SP tokens at a fixed interest rate they deem appropriate, thereby confirming SP's true market value. As long as the quoted price of SP does not exceed the value of the principal redeemable upon maturity, it is guaranteed to be sold.
