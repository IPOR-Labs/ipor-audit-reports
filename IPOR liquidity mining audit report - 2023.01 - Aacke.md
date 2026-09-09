# IPOR liquidity mining audit report — Ackee Blockchain (2022-11-09, revised through 2023-01-27)

- **Auditor:** Ackee Blockchain (Lukáš Böhm, Lead Auditor; Miroslav Škrabal, Auditor; Josef
  Gattermayer, Ph.D., Audit Supervisor)
- **Date:** Revision 1.0 (final report) November 9, 2022; Revision 1.1 (fix review) November 21,
  2022; Revision 1.2 (fix review, after the codebase moved to `IPOR-Labs/ipor-power-tokens`)
  December 23, 2022; Revision 1.3 (protocol naming update, diff-only review) January 27, 2023
- **Scope:** `LiquidityMining` and `PowerIpor` contracts, plus differential fuzz testing of the
  ABDK math library used for quadruple-precision calculations.
- **Result:** No actual threat found in the initial review; the most severe issue found overall (a
  High-severity inability to unstake once a contract runs out of rewards, reported independently
  via a public post) was identified and fixed in revision 1.2.

## Findings by severity

| Severity | Count | Status |
|---|---|---|
| Critical | 0 | — |
| High | 1 | Fixed |
| Medium | 3 | 2 fixed, 1 acknowledged |
| Warning | 1 | Acknowledged |
| Informational | 16 | 13 fixed, 1 partly fixed, 2 acknowledged |
| **Total** | **21** | |

## Notable findings

- **H1: Inability to unstake when the contract runs out of rewards** — High, Fixed (added in
  revision 1.2)
- **M1: Reclaiming renounced ownership** — Medium, Fixed
- **M2: Renounce ownership risk** — Medium, Acknowledged
- **M3: Non-programmatic approach for setting constants** — Medium, Fixed
- **W1: Usage of `solc` optimizer** — Warning, Acknowledged

16 Informational findings (I1–I16, code quality/gas/readability): 13 Fixed; "I10: Reading length of
an array in for loop" Partly fixed; "I3: Variables should be declared as constants" and "I5:
Unnecessary use of `_msgSender()`" Acknowledged.

Full report: [IPOR liquidity mining audit report - 2023.01 - Aacke.pdf](<./IPOR liquidity mining audit report - 2023.01 - Aacke.pdf>)
