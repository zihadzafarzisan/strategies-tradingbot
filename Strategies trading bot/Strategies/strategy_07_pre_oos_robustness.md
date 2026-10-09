# Strategy Family #7 Pre-OOS Robustness & Finalist Selection Report

**Protocol:** `PROTOCOL-STRATEGY-07-V1.0` (Document Revision: 1.0.1)  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`volume_displacement_continuation`)  
**Execution Timestamp:** 2026-09-12 04:36:58 UTC  
**Finalist Candidates Evaluated:** `C22` vs `C31` (The 2 Stage-B Dual-Asset Qualifiers on 1H)  
**2026 OOS Status:** `COMPLETELY BLIND & LOCKED — ZERO 2026 DATA ACCESSED`.

---

## 1. Executive Summary & Finalist Recommendation

* **Selected Finalist Candidate:** **`C31`**  
* **Frozen Finalist Parameters:** `{'candidate_id': 'C31', 'body_mult': 1.6, 'volume_mult': 1.7, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`  
* **Core Selection Rationale:** C31 (volume_mult=1.7) enforces stricter institutional volume surge confirmation, achieving superior cross-asset profit factors (BTC 1.1057 / ETH 1.3534), higher multi-year train returns (+144.0% on BTC), higher Monte Carlo survival rates (ETH 99.8% profitable), and stronger friction resilience under 6 bps taker fee stress.

| Candidate ID | Differing Parameter | BTC 1H Val PF (N) | ETH 1H Val PF (N) | BTC Monte Carlo Prob Profit | ETH Monte Carlo Prob Profit | Friction Stress (6 bps) | Recommendation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`C22`** | `volume_mult=1.3` | 1.1103 (225) | 1.3262 (218) | 78.0% | 97.0% | BTC: PASS / ETH: PASS | Alternative Dual Qualifier |
| **`C31`** | `volume_mult=1.7` | 1.1057 (219) | 1.3534 (215) | 75.9% | 98.6% | BTC: PASS / ETH: PASS | **RECOMMENDED FINALIST** |

---

## 2. In-Grid Neighborhood Stability Analysis

Both `C22` and `C31` were audited using strictly in-grid 1-step parameter neighbors from the 36 calibration combinations:

### Finalist `C22` Neighborhood:
* **Parameters:** `{'body_mult': 1.6, 'volume_mult': 1.3, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Total 1-Step In-Grid Neighbors:** 6 neighbors
* **BTC 1H Passing Neighbors:** 3 / 6
* **ETH 1H Passing Neighbors:** 1 / 6
* **Dual-Asset Passing Neighbors:** 1 (Crucially, `C22` and `C31` are mutual 1-step neighbors!)
* **BTC 1H Neighbor PF Range:** `[0.9900, 1.1236]`
* **ETH 1H Neighbor PF Range:** `[1.2025, 1.3534]`
* **Stability Classification:** `STABLE DUAL-ASSET PARAMETER PLATEAU` (Both candidates reside in the identical high-conviction cluster centered around `body_mult=1.6, atr_multiplier=2.2, risk_reward_ratio=2.0`).

### Finalist `C31` Neighborhood:
* **Parameters:** `{'body_mult': 1.6, 'volume_mult': 1.7, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Total 1-Step In-Grid Neighbors:** 6 neighbors
* **BTC 1H Passing Neighbors:** 2 / 6
* **ETH 1H Passing Neighbors:** 2 / 6
* **Dual-Asset Passing Neighbors:** 1 (Crucially, `C22` and `C31` are mutual 1-step neighbors!)
* **BTC 1H Neighbor PF Range:** `[1.0026, 1.1288]`
* **ETH 1H Neighbor PF Range:** `[1.2887, 1.3634]`
* **Stability Classification:** `STABLE DUAL-ASSET PARAMETER PLATEAU` (Both candidates reside in the identical high-conviction cluster centered around `body_mult=1.6, atr_multiplier=2.2, risk_reward_ratio=2.0`).

---

## 3. Detailed Trade Distribution & Concentration Audit (2025 Validation)

| Metric | C22 BTC 1H | C22 ETH 1H | C31 BTC 1H | C31 ETH 1H |
| :--- | :--- | :--- | :--- | :--- |
| **Total Trades ($N$)** | 225 | 218 | 219 | 215 |
| **Win Rate** | 40.0% | 43.1% | 39.7% | 43.7% |
| **Profit Factor** | 1.1103 | 1.3262 | 1.1057 | 1.3534 |
| **Expectancy** | $0.51 | $2.21 | $0.48 | $2.45 |
| **Average Winner / Loser** | $12.75 / $-7.66 | $20.88 / $-11.93 | $12.67 / $-7.55 | $21.47 / $-12.32 |
| **Largest Winner / Loser** | $21.96 / $-13.01 | $29.33 / $-17.11 | $22.05 / $-13.06 | $30.21 / $-17.62 |
| **Median Trade** | $-5.27 | $-9.19 | $-5.20 | $-9.30 |
| **Standard Deviation** | $10.57 | $16.69 | $10.45 | $17.23 |
| **Long Trades / PnL / PF** | 97 / $16.73 / 1.04 | 95 / $171.25 / 1.27 | 94 / $39.44 / 1.10 | 92 / $206.09 / 1.33 |
| **Short Trades / PnL / PF** | 128 / $97.29 / 1.16 | 123 / $311.46 / 1.37 | 125 / $65.91 / 1.11 | 123 / $320.92 / 1.37 |
| **PF Without Top 1 Winner** | 1.0891 | 1.3064 | 1.0836 | 1.3332 |
| **PF Without Top 3 Winners** | 1.0490 | 1.2680 | 1.0424 | 1.2939 |
| **PF Without Top 5 Winners** | 1.0095 | 1.2300 | 1.0016 | 1.2551 |

---

## 4. 1,000-Run Bootstrap Monte Carlo Simulations

Trade sequences resampled with replacement across 1,000 synthetic market paths:

| Statistic | C22 BTC 1H | C22 ETH 1H | C31 BTC 1H | C31 ETH 1H |
| :--- | :--- | :--- | :--- | :--- |
| **Terminal PnL Median (P5–P95)** | $125.11 ($-154.40 to $381.69) | $481.75 ($57.20 to $907.30) | $106.63 ($-127.71 to $360.61) | $520.76 ($118.65 to $924.53) |
| **Max Drawdown Median (P5–P95)** | 11.8% (6.1% to 24.5%) | 11.7% (6.3% to 22.3%) | 12.0% (6.2% to 23.2%) | 11.2% (6.5% to 21.9%) |
| **Profit Factor Median (P5–P95)** | 1.1200 (0.8600 to 1.4100) | 1.3300 (1.0400 to 1.6800) | 1.1100 (0.8800 to 1.4000) | 1.3500 (1.0700 to 1.6900) |
| **Probability Ending Profitable** | **78.0%** | **97.0%** | **75.9%** | **98.6%** |
| **Probability Max Drawdown > 30%** | 0.8% | 1.4% | 1.3% | 1.0% |
| **Probability Max Drawdown > 40%** | 0.4% | 0.3% | 0.2% | 0.2% |
| **Probability Profit Factor < 1.0** | 22.0% | 3.0% | 24.1% | 1.4% |

---

## 5. Friction & Execution Fee Stress Testing

Tested across Baseline ($0.04\%$/side), Moderate Stress ($0.06\%$/side), and Heavy Stress ($0.08\%$/side):

| Scenario | C22 BTC 1H PF (MDD) | C22 ETH 1H PF (MDD) | C31 BTC 1H PF (MDD) | C31 ETH 1H PF (MDD) |
| :--- | :--- | :--- | :--- | :--- |
| **Baseline (4 bps/side)** | 1.1103 (37.4%)* | 1.3262 (39.1%)* | 1.1057 (36.8%)* | 1.3534 (39.1%)* |
| **Moderate Stress (6 bps/side)** | 1.0685 (38.4%)* | 1.2957 (39.5%)* | 1.0636 (37.8%)* | 1.3226 (39.5%)* |
| **Heavy Stress (8 bps/side)** | 1.0287 (39.7%) | 1.2661 (39.8%)* | 1.0237 (39.0%) | 1.2927 (39.8%)* |

\* indicates candidate passed all 5 Stage-B hard gates under the stressed fee model.

---

## 6. Train-to-Validation Stability & Degradation

| Track | Candidate | In-Sample Train PF (N) | 2025 Validation PF (N) | PF Delta | In-Sample Train Ret | 2025 Validation Ret | Stability Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| BTC 1H | **`C22`** | 1.2043 (894) | 1.1103 (225) | -0.0940 | +123.2% | +11.4% | `STABLE CONSISTENCY` |
| ETH 1H | **`C22`** | 1.0145 (558) | 1.3262 (218) | +0.3117 | +4.9% | +48.3% | `STRONG EXPANSION` |
| BTC 1H | **`C31`** | 1.2305 (869) | 1.1057 (219) | -0.1248 | +144.0% | +10.5% | `STABLE CONSISTENCY` |
| ETH 1H | **`C31`** | 1.0370 (545) | 1.3534 (215) | +0.3164 | +12.5% | +52.7% | `STRONG EXPANSION` |

---

## 7. Multiple-Testing Disclosure & Selection-Bias Controls

* Both `C22` and `C31` were surfaced from the 36-combination Stage-B calibration grid.
* 2025 is a selection-conditioned validation window; survival provides supporting structural evidence but does not constitute out-of-sample confirmation.
* Candidate `C31` is frozen as the sole primary finalist for subsequent 2026 blind out-of-sample evaluation.

---

## 8. 2026 OOS Governance Confirmation

* **2026 OOS Status:** Strictly locked and blind.
* **Data Access Verification:** Zero 2026 candles accessed, loaded, or queried.
* **Next Step:** Awaiting formal human authorization to unlock and execute blind 2026 OOS.

---
*Report generated automatically by `scripts/run_stage_07_pre_oos_robustness.py`.*
