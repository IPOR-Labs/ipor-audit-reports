# IPOR protocol audit report — Zokyo (2022-08-15)

- **Auditor:** Zokyo
- **Date:** August 15, 2022 (v1.0)
- **Scope:** Core IPOR protocol contracts, reviewed at commit `2a7cf870657f6ea0f7a356df79d7a60d5a3d2713`
  of `IPOR-Labs/ipor-protocol`: `Milton` (AMM) and its Dai/Internal/Storage/Usdc variants,
  `IporSwapLogic`, `SoapIndicatorLogic`, `Joseph` (liquidity pool manager) and its Dai/Internal
  variants, the `MiltonSpreadModel` family, `Stanley` (asset management strategy router) and its
  Dai/Usdc/Usdt variants, `StrategyAave`, `StrategyCompound`, `StrategyCore`, `IpToken`, `IvToken`,
  `IporOracle`, `IporMath`, `IporOwnable`/`IporOwnableUpgradeable`, plus supporting error and
  utility libraries.
- **Result:** PASS, score 98/100, contract status "Low Risk". No critical issues found; the
  reported findings have no impact on contract performance or security.

## Findings by severity

| Severity | Count | Status |
|---|---|---|
| Critical | 0 | — |
| High | 0 | — |
| Medium | 0 | — |
| Low | 2 | 1 resolved, 1 unresolved |
| Informational | 5 | 4 resolved, 1 acknowledged |
| **Total** | **7** | |

## Findings

1. **Multiple external calls executed in the same transaction (MiltonInternal)** — Low, Unresolved
2. **Multiple external calls executed in the same transaction (StrategyAave)** — Low, Resolved
3. **Incorrect balance assertion (MiltonInternal)** — Informational, Acknowledged
4. **Incorrect balance assertion (Joseph)** — Informational, Acknowledged
5. **Redundant usage of SafeMath (IvToken)** — Low, Resolved
6. **Variable shadowing (MiltonStorage)** — Informational, Resolved
7. **Logical operator gas optimization** — Informational, Resolved

Full report: [IPOR protocol audit report - 2022.08 - Zokyo.pdf](<./IPOR protocol audit report - 2022.08 - Zokyo.pdf>)
