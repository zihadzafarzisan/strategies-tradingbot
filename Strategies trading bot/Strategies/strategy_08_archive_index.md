# Strategy Family #8 Archive Index

**Strategy Slug:** `adaptive_displacement_trailing`  
**Protocol:** `PROTOCOL-STRATEGY-08-V1.3`  
**Index Status:** Maintained (V1.2 superseded; V1.3 archived after 2025 Validation failure)

---

## Version / Lifecycle Governance

| Version | Status | Detail |
| :--- | :--- | :--- |
| **V1.2** | SUPERSEDED — ARCHIVED (immutable) | Frozen protocol `protocol_strategy_08_v1_2_frozen.md`; Stage-A artifacts archived as historical evidence. V1.2 treated `body_mult`/`volume_mult`/`volume_period` as grid dimensions without signal math (collapsed grid). **V1.2 survivors were never promoted to Stage-B / V1.3.** |
| **V1.3** | PROTOCOL FROZEN → ARCHIVED (this index) | Corrected body/volume qualification math; full protocol run executed and archived after a genuine 2025 Validation failure. |

---

## Artifact Inventory (V1.2)

| Artifact | Path | Role / Status |
| :--- | :--- | :--- |
| Frozen Protocol (V1.2) | `data/protocol_strategy_08_v1_2_frozen.md` | Immutable archive. SHA `5bf062e15aa8a91d7d521dd678fa5015d0ea43a6686e4ba995914a0e93688457` |
| Stage-A Diagnostic Archive | `data/strategy_08_v1_2_stage_a_diagnostic_archive.md` | Historical evidence (never promoted) |
| Stage-A Screening Archive | `data/strategy_08_v1_2_stage_a_screening_archive.json` | Historical evidence (never promoted) |

## Artifact Inventory (V1.3)

| Artifact | Path | Role / Status |
| :--- | :--- | :--- |
| Frozen Protocol | `data/protocol_strategy_08.md` | Canonical V1.3. SHA `3446ea12673fc26d4c2cf5481d19e753a3be5857c35af5279626ff3cd192e08a` (20,507 B) |
| Implementation | `src/crypto_quant/strategies/adaptive_displacement_trailing.py` | Verified. SHA `f02850c51b9cba7a48b15ba23bc2d9fc4ec9c7a344a7c15fa0450f4d073e3bde` |
| Unit/Invariant Tests | `tests/test_strategy_08.py` | Verified. SHA `bbcdfcbadbcdca9eee6e3f3dd23f3f4e727056798d13aa78baf506c0802ae245` |
| Implementation Audit | `data/strategy_08_implementation_audit.md` | Line-by-line causality / anti-lookahead report |
| **Stage-A** | `data/strategy_08_stage_a_screening.json` | **PASSED.** 37 candidates; exact intersection C00–C36. SHA `6362f611997cd631008ffa614101d1c206bcde696d87bfb3c576908858057538` |
| Stage-A Diagnostic | `data/strategy_08_stage_a_diagnostic.md` | Human-readable Stage-A report |
| **Stage-B** | `data/strategy_08_stage_b_results.json` | **PASSED.** Dual-asset survivors {C34, C35, C36}. SHA `bc1451e300ee0b28d753ace383fc93b9afeda2838f2ad3ff0830c6b203f9fc4b` |
| Stage-B Diagnostic | `data/strategy_08_stage_b_diagnostic.md` | Human-readable Stage-B report |
| **2025 Validation** | `data/strategy_08_2025_validation.json` | **FAILED.** Zero dual-asset survivors. SHA `a1b1e23f915477e7da561ba4622ba4f0a51dd52b05971cc5ddabf78dd9e98c6d` |
| Validation Diagnostic | `data/strategy_08_2025_validation_diagnostic.md` | Human-readable Validation report. SHA `d5bd6eafcc97409884a17a5348119d50528fe2dc108758e5f91f27210827bb6f` |
| Validation Post-Mortem | `data/strategy_08_v1_3_validation_post_mortem.md` | **This file's companion — authoritative closure record** |
| Runners | `run_stage_a_s8.py`, `run_stage_b_s8.py`, `run_validation_s8.py` | Reproducible stage runners |

---

## Governance Disposition
* **Validation Result:** `STRATEGY_08_V1_3_VALIDATION_FAILED`
* **Validation Forensic Audit:** `S8_V1_3_2025_VALIDATION_FORENSIC_PASS`
* **Final Verdict:** `STRATEGY_08_V1_3_VALIDATION_FAILED_AND_ARCHIVED`
* **Reason:** All three Stage-B survivors (C34, C35, C36) failed the frozen 2025 Validation hard gates; the dual-asset survivor set is empty. BTC candidates were unprofitable (PF 0.33–0.39); on ETH, C35 was profitable but N=13 < 15 (minimum-N gate), and C34/C36 failed profitability/expectancy. No gate was loosened; positive profitability did not override a hard gate.
* **2026/OOS Status:** BLIND — not accessed, not authorized.
* **Downstream:** OOS, robustness, Monte Carlo, paper trading, live trading — NOT authorized, NOT executed.
* **Era Closure:** `STRATEGY_08_ARCHIVED_IMMUTABLE` — sealed 2026-09-14 under `ERA_SINGLE_ASSET_1H_PERP_FORMALLY_CLOSED`. All artifacts immutable. Cross-reference: `data/master_strategy_archive_index.md`.

## Historical Integrity
* V1.2 artifacts are immutable and were never modified, relabeled, or deleted.
* V1.3 Stage-A/B/Validation artifacts are permanently archived; no overwriting, no relabeling, no deletion.
* This index is a live pointer only; it does not alter any artifact.