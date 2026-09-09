# IPOR Protocol Audits

Full audit evidence for the current **IPOR Fusion** vault infrastructure (Plasma Vaults, fuses) —
scope, dates, auditors and completed reports — is published at
**[docs.ipor.io/build-on-fusion/developer-guide/security-and-audits](https://docs.ipor.io/build-on-fusion/developer-guide/security-and-audits)**.

This repository holds the audit reports for the earlier **IPOR interest-rate-derivatives protocol**
(the IPOR Index, AMM and Liquidity Mining contracts that predate Fusion).

## Reports in this repository

| Report | Auditor | Date | Scope | Findings |
|---|---|---|---|---|
| [IPOR protocol audit report](<./IPOR protocol audit report - 2022.08 - Zokyo.pdf>) ([summary](<./IPOR protocol audit report - 2022.08 - Zokyo.md>)) | Zokyo | 2022-08-15 | Milton (AMM), Joseph (liquidity pool), Stanley (asset management strategies), IPOR Oracle, IpToken/IvToken | 7 total — 0 Critical/High/Medium, 2 Low, 5 Informational. Scored 98/100, "Low Risk". |
| [IPOR token audit report](<./IPOR token audit report - 2022.11 - Aacke.pdf>) ([summary](<./IPOR token audit report - 2022.11 - Aacke.md>)) | Ackee Blockchain | 2022-11-09 (fix review 2022-11-21) | `IporToken` contract | 2 total — 0 Critical/High/Medium, 1 Warning, 1 Info. No exploitable threat found. |
| [IPOR liquidity mining audit report](<./IPOR liquidity mining audit report - 2023.01 - Aacke.pdf>) ([summary](<./IPOR liquidity mining audit report - 2023.01 - Aacke.md>)) | Ackee Blockchain | 2022-11-09, revised through 2023-01-27 | `LiquidityMining` and `PowerIpor` contracts | 21 total — 0 Critical, 1 High, 3 Medium, 1 Warning, 16 Info. All fixed or acknowledged. |

Each report above has a companion Markdown summary in this repo with the full findings breakdown
and the current status of every finding.

## Looking for Fusion vault audits?

IPOR Fusion is a separate, newer product from the interest-rate-derivatives protocol audited here,
and is audited independently. See
[Security and Audits](https://docs.ipor.io/build-on-fusion/developer-guide/security-and-audits) on
docs.ipor.io for the BlocSec and Protofire reports covering the live Fusion contracts.
