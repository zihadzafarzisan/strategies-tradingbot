# Strategy Family #7 Archive Index

| Artifact | Path | Purpose |
| :--- | :--- | :--- |
| **Protocol Specification** | `data/protocol_strategy_07.md` | Protocol definition, baseline params, and 36-combination search space |
| **Strategy Implementation** | `src/crypto_quant/strategies/volume_displacement_continuation.py` | Python strategy class |
| **Stage-A Runner** | `scripts/run_stage_07_a.py` | Baseline screening script |
| **Stage-A JSON Results** | `data/strategy_07_stage_a_screening.json` | Machine-readable Stage-A metrics |
| **Clean Stage-A Diagnostic** | `data/strategy_07_stage_a_diagnostic_clean.md` | Verified Stage-A screening report |
| **Implementation Audit** | `data/strategy_07_implementation_audit.md` | Verified line-by-line causality & anti-lookahead report |
| **Stage-B Runner** | `scripts/run_stage_07_b.py` | 37-configuration calibration runner (296 slices, query-bound protected) |
| **Stage-B JSON Results** | `data/strategy_07_stage_b_optimization.json` | Machine-readable 296-slice calibration matrix |
| **Stage-B Calibration Report** | `data/strategy_07_stage_b_calibration.md` | Comprehensive Stage-B calibration report |
| **Stage-B Readiness Report** | `data/strategy_07_stage_b_readiness_report.md` | Pre-calibration consistency and readiness report |
| **Pre-OOS Robustness Engine** | `scripts/run_stage_07_pre_oos_robustness.py` | Pre-OOS diagnostics engine (Monte Carlo, friction stress) |
| **Pre-OOS Robustness JSON** | `data/strategy_07_pre_oos_robustness.json` | Machine-readable robustness outputs |
| **Final Robustness Report** | `data/strategy_07_pre_oos_robustness_final.md` | Authoritative pre-OOS robustness and finalist selection report |
| **OOS Authorization Dossier** | `data/strategy_07_oos_authorization_v1.md` | Pre-declared OOS parameters, gates, and authorization document |
| **OOS Runner** | `scripts/run_stage_07_oos.py` | 2026 Out-of-Sample evaluation runner |
| **OOS JSON Results** | `data/strategy_07_oos_report.json` | Machine-readable 2026 OOS metrics |
| **OOS Markdown Report** | `data/strategy_07_oos_report.md` | Official 2026 OOS evaluation report |
| **Final Post-Mortem** | `data/strategy_07_final_post_mortem.md` | Authoritative post-mortem and permanent closure declaration |

## Governance Disposition
* **Final Verdict:** `PERMANENTLY REJECTED AND ARCHIVED`
* **Reason:** Candidate `C31` achieved net positive profitability on both assets in 2026 OOS (BTC $+5.2\%$, ETH $+16.7\%$), but breached the pre-declared maximum drawdown hard gate ($MDD \le 35.00\%$) on both assets (actual: BTC $38.5\%$, ETH $36.8\%$). Under strict governance, the outcome is classified as `DUAL_ASSET_OOS_FAILED`.
* **2026 OOS Status:** Completed over the pre-declared 8-month window (`2026-01-01` to `2026-08-31`). Zero post-OOS retuning permitted.
* **Era Closure:** `STRATEGY_07_ARCHIVED_IMMUTABLE` — sealed 2026-09-14 under `ERA_SINGLE_ASSET_1H_PERP_FORMALLY_CLOSED`. All artifacts immutable. Cross-reference: `data/master_strategy_archive_index.md`.
