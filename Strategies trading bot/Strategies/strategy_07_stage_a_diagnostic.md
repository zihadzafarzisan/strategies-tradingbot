# Strategy Family #7 (Volume Displacement Continuation) Stage-A Baseline Screening Diagnostic Report

**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0`  
**Strategy Family:** `VolumeDisplacementContinuationStrategy` (`volume_displacement_continuation`)  
**Execution Date:** 2026-09-12 00:13:04 UTC  
**OOS Status:** 2026 dataset strictly locked and excluded (`timestamp < 2026-01-01 00:00:00 UTC`).

---

## 1. Baseline Screening Summary (C00 Frozen Benchmark)

| Experiment ID | Symbol | TF | Bars | Trades ($N$) | Win Rate | Profit Factor | Expectancy | Net Return | Max DD | Evidence Class | Stage-A Result |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `EXP_VDC_BTC_4H` | BTCUSDT | 4h | 13,151 | 342 | 37.4% | 1.3195 | +$2.90 | +99.2% | 44.4% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_BTC_1H` | BTCUSDT | 1h | 52,576 | 1,213 | 36.0% | 1.1729 | +$1.39 | +168.2% | 44.1% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_ETH_4H` | ETHUSDT | 4h | 8,766 | 214 | 47.2% | 2.0465 | +$9.84 | +210.5% | 29.2% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_ETH_1H` | ETHUSDT | 1h | 35,063 | 873 | 33.7% | 1.0964 | +$0.60 | +52.7% | 62.7% | `ADEQUATE_EVIDENCE` | **PASS** |

---

## 2. Timeframe Architecture Advancement Decisions

Under `PROTOCOL-STRATEGY-07-V1.0` Section 5.2, a candidate timeframe advances to Stage-B parameter calibration **only if both BTCUSDT and ETHUSDT pass all Stage-A screening rules** ($N \ge 30$ and non-catastrophic).

| Timeframe | BTC Baseline Status | ETH Baseline Status | Both Passed Stage-A? | Stage-B Advancement Decision |
| :--- | :--- | :--- | :--- | :--- |
| **4H** | **PASS** ($PF=1.3195, N=342$) | **PASS** ($PF=2.0465, N=214$) | **YES** | **`ADVANCES_TO_STAGE_B`** |
| **1H** | **PASS** ($PF=1.1729, N=1213$) | **PASS** ($PF=1.0964, N=873$) | **YES** | **`ADVANCES_TO_STAGE_B`** |

---

## 3. Standardized Execution & Accounting Audit

* **Market Type:** Futures (5x leverage, isolated margin)
* **Capital & Risk:** $1,000 starting equity, 1.0% risk per trade, max 3 open positions
* **Fees & Friction:** 0.04% taker fee per side (0.08% round-turn), dynamic tick slippage embedded in fills, 8h funding rate accounting
* **Execution Timing:** Signal at bar $i$ close; fill at bar $i+1$ open; conservative stop-first intra-bar priority
* **Accounting Identity:** $\text{Net PnL} = \text{Gross Profit} - \text{Gross Loss} = \text{Final Equity} - \text{Initial Capital}$

---

## 4. 2026 OOS Protection Verification

* **OOS Status:** Fully locked and untouched.
* **Maximum Timestamp Loaded:** Strictly $< 2026-01-01 00:00:00 UTC$ across all 4 experiments (`end_ms=1767225600000`).
* **Parameter Tuning Status:** Zero parameters tuned during Stage-A.
* **Data Slicing Integrity:** No 2026 candles accessed, queried, or evaluated.

---
*Diagnostic report verified against `data/strategy_07_stage_a_screening.json`.*
