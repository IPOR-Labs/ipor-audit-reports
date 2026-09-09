# IPOR token audit report — Ackee Blockchain (2022-11-09)

- **Auditor:** Ackee Blockchain (Lukáš Böhm, Lead Auditor; Miroslav Škrabal, Auditor; Josef
  Gattermayer, Ph.D., Audit Supervisor)
- **Date:** Revision 1.0 (final report) November 9, 2022; Revision 1.1 (fix review) November 21,
  2022
- **Scope:** `IporToken` contract, reviewed at commit `01c08c3`. (A companion contract set,
  `LiquidityMining`/`PowerIpor`, was split into a separate report at the client's request — see the
  liquidity mining audit summary in this repo.)
- **Result:** No actual threat found; both findings relate to code quality/configuration, not
  exploitable vulnerabilities.

## Findings by severity

| Severity | Count | Status |
|---|---|---|
| Critical | 0 | — |
| High | 0 | — |
| Medium | 0 | — |
| Warning | 1 | Acknowledged |
| Informational | 1 | Fixed |
| **Total** | **2** | |

## Findings

1. **W1: Usage of `solc` optimizer** — Warning, Acknowledged (already in use in deployed IPOR
   Protocol contracts; team will monitor for related issues)
2. **I1: Redundant inheritance of Ownable** — Informational, Fixed (redundant inheritance removed)

Full report: [IPOR token audit report - 2022.11 - Aacke.pdf](<./IPOR token audit report - 2022.11 - Aacke.pdf>)
