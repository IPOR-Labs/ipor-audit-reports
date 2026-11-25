# IPOR Fusion security review — Three Sigma (2026-11)

- **Auditor:** Three Sigma (2 auditors, 6 person weeks)
- **Date:** October 29 to November 14, 2026
- **Scope:** IPOR Fusion at commit
  [`004d0545`](https://github.com/IPOR-Labs/ipor-fusion/tree/004d0545774f19b3a4f03acabeb4dceeb73d44fb):
  - Fusion Vault (PlasmaVault, PlasmaVaultBase, PlasmaVaultGovernance and vault libraries), Access
    Management, Fee Manager, Withdraw Manager, Rewards Manager, Price Oracle Middleware Manager,
    Context Manager, Plasma Vault Pauser, Prehooks
  - Crosschain extension on Chainlink CCIP: Dispatcher, Executor and Factory, crosschain fuses
    (command, supply, balance, claim), Rescue module
  - Fuses: HyperCore, Euler V2, ERC-4626 Supply, Universal Token Swapper with Verification, Plasma
    Vault Request Shares
- **Result:** 34 findings, none Critical. All 5 High findings were addressed in code. Of the 29
  Medium and Low findings, 20 were addressed and 9 acknowledged.

## Findings by severity

| Severity | Found | Addressed | Acknowledged |
|---|---|---|---|
| Critical | 0 | 0 | 0 |
| High | 5 | 5 | 0 |
| Medium | 19 | 12 | 7 |
| Low | 10 | 8 | 2 |
| **Total** | **34** | **25** | **9** |

## Findings

Status is quoted from the report. "Addressed in #…" gives the short hash of the fix commit.

| ID | Severity | Finding | Status |
|---|---|---|---|
| 3S-H01 | High | Unauthenticated CallbackData in the Euler callback path allows ALPHA to grant a persistent unrestricted allowance over every vault token | Addressed in `4ad9dd9` |
| 3S-H02 | High | EulerV2BatchFuse::enter approves and calls unvalidated approval-pair addresses, so ALPHA can drain the vault | Addressed in `ed021d0` |
| 3S-H03 | High | EulerV2BalanceFuse::balanceOf values EulerSwap sub-accounts inside the swap callback, so deposit mints at deflated NAV | Addressed in `45d3a5d` |
| 3S-H04 | High | Fixed 20% attestation band around bridged principal on a leveraged remote leg leads to day-long freezes and clamped share prices that let Index subscribers and liquidators take value from existing holders | Addressed in `2422743` |
| 3S-H05 | High | Oracle valuation of EulerSwap pool holdings that ignores the swapper's reversible claim allows atomic NAV inflation for redemptions at the expense of remaining holders | Addressed in `4151c4e` |
| 3S-M01 | Medium | Rewards claimed on the vault's behalf counted in the live idle balance allow anyone to bypass reward vesting and capture accrued rewards | Acknowledged |
| 3S-M02 | Medium | Unguarded share-price views during a PlasmaVault's execute batch and instant withdrawal allow parent vaults to mint and redeem against a transient child NAV | Acknowledged |
| 3S-M03 | Medium | LP balance fuses splitting positions at the live pool price allow a flash swap to inflate NAV and let a redeeming holder take value from other holders | Acknowledged |
| 3S-M04 | Medium | Missing market balance refresh before deposit and idle-funded exit pricing allows timed entries and exits to take unrecognized yield and shift unrecognized losses to other holders | Acknowledged |
| 3S-M05 | Medium | Callback-path market refresh at a transient mid-batch state leads to phantom NAV, performance fees on unreal gains and bypassed market limits | Addressed in `2978f71` |
| 3S-M06 | Medium | Missing underlying-asset skip in ERC-4626 and Euler V2 balance fuses leads to double-counted idle assets and redemptions paid from remaining holders' funds | Addressed in `a01445a` |
| 3S-M07 | Medium | PlasmaVault::_checkCanCall checks the caller's redemption lock when the caller moves another owner's shares | Addressed in `98c4ac6` |
| 3S-M08 | Medium | PlasmaVault::_updateMarketsBalances enforces market limits on every refresh, including refreshes that add no exposure | Addressed in `28429d1` |
| 3S-M09 | Medium | Unconditional untracking after an incomplete vault sweep removes live shares from NAV and disables their normal exit paths | Addressed in `7d41b06` |
| 3S-M10 | Medium | Remote ERC-4626 shares are valued with convertToAssets, which excludes exit fees, so attested cross-chain NAV can exceed redeemable assets | Acknowledged |
| 3S-M11 | Medium | Euler callback handler that authenticates only the caller and selector, and forwards caller-chosen forceApprove parameters, allows any external contract reached during execute to obtain a persistent allowance over every vault token | Addressed in `7d41b06` |
| 3S-M12 | Medium | RedemptionDelayLib::lockChecks restarts the lock on the receiver's entire balance at every deposit | Acknowledged |
| 3S-M13 | Medium | EulerSwap pools enabled without a capital-flow NAV refresh requirement allow stale-priced deposits and redemptions that shift pool gains and losses between holders | Acknowledged |
| 3S-M14 | Medium | Removed fuse remains in the instant-withdrawal list and is still delegatecalled on user withdrawals, which allows a revoked fuse to drain the vault or block exits | Addressed in `0ef60cb` |
| 3S-M15 | Medium | Context sender returned for any caller during relayed calls allows reentrant external contracts to steal the relayed user's vault shares | Addressed in `5302604` |
| 3S-M16 | Medium | Instant withdrawal sized by share value instead of available Euler cash leads to reverted vault withdrawals despite sufficient combined liquidity | Addressed in `dbc876a` |
| 3S-M17 | Medium | Unbacked withdrawal requests without a redemption lock allow fresh deposits to consume released withdrawal capacity and bypass the redemption delay | Addressed in `31f8af4` |
| 3S-M18 | Medium | Missing freshness and round-completeness validation for custom price feeds in PriceOracleMiddlewareManager enables stale-price NAV mispricing and value extraction | Addressed in `b330ccc` |
| 3S-M19 | Medium | HyperCoreSendFuse::_bridgeBaseline ignores vested rewards that RewardsClaimManager pushes into the vault | Addressed in `6389657` |
| 3S-L01 | Low | Recall queued on a shared CCIP pool rate limit allows any bridge user to stall the dispatcher queue and freeze all deposits and withdrawals of the source vault | Addressed in `590af52` |
| 3S-L02 | Low | Single BALANCE_APPROVER key can block a chain with rejectBalanceAndBlock and freeze all vault user flows, and the immutable key cannot be rotated or neutralized | Addressed in `fb75359` |
| 3S-L03 | Low | Missing management fee realization before performance fee crystallization in execute and updateMarketsBalances leads to performance fees charged on the accrued management fee | Addressed in `68df2e3` |
| 3S-L04 | Low | Fee shares sized at the pre-mint share price lead to performance and management fees below the configured rate | Addressed in `68df2e3` |
| 3S-L05 | Low | EulerV2SupplyFuse::_performWithdraw forwards all gas, so a paused Euler vault makes redeem run out of gas | Addressed in `2422743` |
| 3S-L06 | Low | Performance fee update without prior crystallization leads to retroactive repricing and reassignment of already earned gains | Addressed in `de20155` |
| 3S-L07 | Low | Erc4626BalanceFuse::balanceOf values ERC-4626 shares at convertToAssets instead of what a redeem pays | Acknowledged |
| 3S-L08 | Low | Erc4626BalanceFuse::balanceOf reads a PlasmaVault child's cached value without refreshing the child | Acknowledged |
| 3S-L09 | Low | Disabled CCIP route is still accepted by ccipReceive, leading to inbound state changes during a lane shutdown | Addressed in `4aa9a89` |
| 3S-L10 | Low | EulerV2BalanceFuse::balanceOf ignores that each EVC sub-account has limited liability | Addressed in `b5b23a3` |

Full report: [IPOR Fusion security review - 2026.11 - Three Sigma.pdf](<./IPOR Fusion security review - 2026.11 - Three Sigma.pdf>)
