# Strategy Family #7 (Volume Displacement Continuation) Clean Stage-A Diagnostic Report

**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0`  
**Document Revision:** 1.0.1  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Strategy Slug:** `volume_displacement_continuation`  
**Execution Timestamp:** 2026-09-12 00:13:04 UTC  
**OOS Status:** 2026 dataset strictly locked and excluded (`timestamp < 2026-01-01 00:00:00 UTC`).

---

## 1. Baseline Screening Summary (C00 Frozen Benchmark)

The uncalibrated baseline configuration `C00`:
* `body_mult`: `1.5`
* `volume_mult`: `1.5`
* `volume_period`: `20`
* `ema_period`: `50`
* `displacement_lookback`: `5`
* `atr_period`: `14`
* `atr_multiplier`: `2.0`
* `risk_reward_ratio`: `2.5`
* `stop_type`: `"atr"`

### Verified Pre-OOS Baseline Results:

| Experiment ID | Symbol | TF | Bars | Trades ($N$) | Win Rate | Profit Factor | Expectancy | Net Return | Max DD | Evidence Class | Stage-A Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `EXP_VDC_BTC_4H` | BTCUSDT | 4h | 13,151 | 342 | 37.4% | 1.3195 | +$2.90 | +99.2% | 44.4% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_BTC_1H` | BTCUSDT | 1h | 52,576 | 1,213 | 36.0% | 1.1729 | +$1.39 | +168.2% | 44.1% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_ETH_4H` | ETHUSDT | 4h | 8,766 | 214 | 47.2% | 2.0465 | +$9.84 | +210.5% | 29.2% | `ADEQUATE_EVIDENCE` | **PASS** |
| `EXP_VDC_ETH_1H` | ETHUSDT | 1h | 35,063 | 873 | 33.7% | 1.0964 | +$0.60 | +52.7% | 62.7% | `ADEQUATE_EVIDENCE` | **PASS** |

*Source of truth: `data/strategy_07_stage_a_screening.json`.*

---

## 2. Stage-A Gate Evaluation & Timeframe Advancement

Under `PROTOCOL-STRATEGY-07-V1.0` Section 5.2, a candidate timeframe advances to Stage-B parameter calibration **only if both BTCUSDT and ETHUSDT pass all Stage-A screening rules** ($N \ge 30$ and non-catastrophic performance: $\text{NOT }(PF < 0.75 \land MDD > 75.0\%)$).

| Timeframe | BTC Baseline Status | ETH Baseline Status | Both Passed Stage-A? | Dual-Asset Advancement Decision |
| :--- | :--- | :--- | :--- | :--- |
| **4H** | **PASS** ($PF=1.3195, N=342$) | **PASS** ($PF=2.0465, N=214$) | **YES** | **`ADVANCES_TO_STAGE_B`** |
| **1H** | **PASS** ($PF=1.1729, N=1213$) | **PASS** ($PF=1.0964, N=873$) | **YES** | **`ADVANCES_TO_STAGE_B`** |

---

## 3. Standardized Execution & Accounting Audit

* **Market Type:** Futures (5x leverage, isolated margin)
* **Capital & Risk:** $1,000.00 starting equity, 1.0% risk per trade, max 3 open positions
* **Fees & Friction:** 0.04% taker fee per side (0.08% round-turn), dynamic tick slippage embedded in fills, 8h funding rate accounting
* **Execution Timing:** Signal at bar $i$ close; fill at bar $i+1$ open; conservative stop-first intra-bar priority
* **Accounting Identity:** $\text{Net PnL} = \text{Gross Profit} - \text{Gross Loss} = \text{Final Equity} - \text{Initial Capital}$

---

## 4. 2026 OOS Protection Verification

* **OOS Status:** Strictly locked and untouched.
* **Maximum Timestamp Loaded:** Strictly $< 2026-01-01 00:00:00 UTC$ (`end_ms=1767225600000`).
* **Parameter Tuning Status:** Zero parameters tuned during Stage-A.
* **Data Slicing Integrity:** No 2026 data accessed or evaluated.
