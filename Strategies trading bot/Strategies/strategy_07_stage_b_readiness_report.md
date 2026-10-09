# Strategy Family #7 Stage-B Calibration Readiness Report

**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0`  
**Document Revision:** 1.0.1  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Strategy Slug:** `volume_displacement_continuation`  
**Audit Date:** 2026-09-12  
**Readiness Status:** `STAGE-B READY FOR HUMAN AUTHORIZATION`

---

## 1. Governance & Protocol Consistency Checklist

| Question | Verification Status | Detail |
| :--- | :--- | :--- |
| **Is the protocol internally consistent?** | **YES** | Protocol defines hypotheses, execution, gates, and splits without ambiguity. |
| **Is C00 correctly separated?** | **YES** | `C00` is explicitly designated as a frozen baseline comparator, distinct from calibration candidates `C01`–`C36`. |
| **Is the 36-combination grid correct?** | **YES** | Cardinality is exactly $2 \times 2 \times 3 \times 3 = 36$ calibration combinations. |
| **Is the Stage-B runner implemented?** | **YES** | `scripts/run_stage_07_b.py` built and verified via py_compile and unit tests. |
| **Is causality verified?** | **YES** | Perturbation tests confirm zero look-ahead; all indicators shifted point-in-time; next-bar-open execution. |
| **Is the train/validation split correct?** | **YES** | BTC Train: 2020–2024; ETH Train: 2022–2024; Validation: 2025 (both). |
| **Is the dual-asset intersection correct?** | **YES** | $\text{DUAL\_ASSET\_CANDIDATES} = \text{BTC\_PASS\_IDS} \cap \text{ETH\_PASS\_IDS}$ is enforced; independent pass counts rejected. |
| **Is 2026 data protected?** | **YES** | Dual protection: query-level bound (`end_ms=1767225600000`) + dataframe timestamp assertions. |
| **Are artifacts ready?** | **YES** | All diagnostic reports, protocols, runners, and test suites are synchronized to the project root. |
| **Is Stage-B ready for execution?** | **YES** | Execution can begin immediately upon explicit human approval. |

---

## 2. Configuration & Execution Slices Summary

* **Configurations Evaluated:** 37 Total
  * **1 Standalone Baseline Comparator:** `C00`
  * **36 Calibration Candidates:** `C01`–`C36`
* **Authorized Tracks:** 4 Tracks (`BTCUSDT_4H`, `ETHUSDT_4H`, `BTCUSDT_1H`, `ETHUSDT_1H`)
* **Chronological Slices per Track:** 2 (In-Sample Train + 2025 Validation)
* **Total Expected Backtest Slices:** $37 \times 4 \times 2 = \mathbf{296\text{ backtest slices}}$

---

## 3. Verified Artifact Hashes (Canonical Project Root)

| Component | Path | SHA-256 Hash |
| :--- | :--- | :--- |
| **Protocol Specification** | `data/protocol_strategy_07.md` | `673b14d481c5a9a0677eb8a99c3def6d809ee04497e976db64d5e89c6c5d3c4b` |
| **Clean Stage-A Diagnostic** | `data/strategy_07_stage_a_diagnostic_clean.md` | `b117ff62eb39b37c03f86d4f52162375338efad94e92433a11fc8d1cd227e9b5` |
| **Stage-A JSON Results** | `data/strategy_07_stage_a_screening.json` | `da910c50604c5d5ae0e06b3df9ba1dde7087b88f63580173f798035c25d5f8c6` |
| **Implementation Audit** | `data/strategy_07_implementation_audit.md` | `4bc069894fe74a702fdbe566dab2359d4333823fb945247565f59013975a0f57` |
| **Strategy Implementation** | `src/crypto_quant/strategies/volume_displacement_continuation.py` | `3929236f1e735cc640831cb186ddfcad71f005b7993b314c1ff9a2123ea790af` |
| **Stage-A Runner** | `scripts/run_stage_07_a.py` | `3a4a5cacb37bdeeba10063efb9c302a8234e906523ca248ed170506a15b143b8` |
| **Stage-B Runner** | `scripts/run_stage_07_b.py` | `c1565cbd65ec56a3e9e1c856e1214a7e5a1c3ca76792867dff4db25bfe3e43b1` |
| **Strategy Unit Tests** | `tests/test_strategy_07.py` | `541a571b604496db978413c335cfdb2d198c235686e1b0547b6fcce1d9bacac2` |
| **Stage-B Runner Tests** | `tests/test_stage_07_b_runner.py` | `463995aa8a7056f4368a04969a70944f676964d0a1067bd99f99017485cf084a` |

---

## 4. 2026 OOS Governance Confirmation

`2026 OOS REMAINS BLIND AND LOCKED. ZERO 2026 DATA WAS ACCESSED OR LOADED.`
