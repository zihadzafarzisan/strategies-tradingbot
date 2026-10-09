# Strategy Family #5 Archive Index

| Artifact | Path | Purpose |
| :--- | :--- | :--- |
| **Protocol Specification** | `data/protocol_strategy_05.md` | Protocol definition, baseline params, and 48-combination search space |
| **Strategy Implementation** | `src/crypto_quant/strategies/volatility_squeeze_breakout.py` | Python strategy class |
| **Stage-A Runner** | `scripts/run_stage_05_a.py` | Baseline screening script |
| **Stage-A JSON Results** | `data/strategy_05_stage_a_screening.json` | Machine-readable Stage-A metrics |
| **Stage-A Diagnostic Report** | `data/strategy_05_stage_a_diagnostic.md` | Stage-A screening report |
| **Stage-B Runner** | `scripts/run_stage_05_b.py` | 48-combination calibration runner (with query-bound protection) |
| **Stage-B JSON Results** | `data/strategy_05_stage_b_optimization.json` | Machine-readable 384-slice calibration matrix |
| **Stage-B Calibration Report** | `data/strategy_05_stage_b_calibration.md` | Comprehensive Stage-B calibration report |
| **Parity Report** | `data/strategy_05_stage_b_parity_report.md` | Pre-calibration file and SHA-256 verification |
| **Final Post-Mortem** | `data/strategy_05_final_post_mortem.md` | Authoritative post-mortem and permanent closure declaration |

## Governance Disposition
* **Final Verdict:** `PERMANENTLY REJECTED AND ARCHIVED`
* **Reason:** Zero shared parameter combinations passed 2025 validation across BTC and ETH ($C_{\text{dual}} = \emptyset$ on both 4H and 1H).
* **2026 OOS Status:** Strictly locked; no 2026 data evaluated.
* **Era Closure:** `STRATEGY_05_ARCHIVED_IMMUTABLE` — sealed 2026-09-14 under `ERA_SINGLE_ASSET_1H_PERP_FORMALLY_CLOSED`. All artifacts immutable. Cross-reference: `data/master_strategy_archive_index.md`.
