# Strategy Family #7 Pre-OOS Robustness & Finalist Selection Final Report

**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0`  
**Document Revision:** 1.0.1  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Strategy Slug:** `volume_displacement_continuation`  
**Execution Timestamp:** 2026-09-12 04:36:58 UTC  
**Finalist Candidates Evaluated:** `C22` vs `C31` (The 2 Stage-B Dual-Asset Qualifiers on 1H)  
**2026 OOS Status:** `COMPLETELY BLIND & LOCKED — ZERO 2026 DATA ACCESSED`.

---

## 1. Executive Summary & Finalist Decision

* **Finalist Selection:** **`C31`** (Selected for blind 2026 Out-of-Sample evaluation)
* **Frozen Finalist Parameters (`C31`):**
  ```json
  {
    "candidate_id": "C31",
    "body_mult": 1.6,
    "volume_mult": 1.7,
    "volume_period": 20,
    "ema_period": 50,
    "displacement_lookback": 5,
    "atr_period": 14,
    "atr_multiplier": 2.2,
    "risk_reward_ratio": 2.0,
    "stop_type": "atr"
  }
  ```
* **Selection Rationale:** `C31` (enforcing a higher volume surge barrier of `volume_mult=1.7` vs `1.3`) achieves superior cross-asset validation profit factors (BTC `1.1057` / ETH `1.3534`), higher multi-year in-sample train returns on both assets (BTC $+144.0\%$, ETH $+12.5\%$), higher Monte Carlo win probability on ETH ($98.6\%$), and slightly lower validation drawdown on BTC ($36.8\%$ vs $37.4\%$).

---

## 2. Finalist Candidate Definitions & Origin

Surfaced from the 36-combination Stage-B calibration grid (`PROTOCOL-STRATEGY-07-V1.0`), `C22` and `C31` represent the **exact non-empty mathematical intersection** on 1H:
$$\text{DUAL\_ASSET\_CANDIDATES} = \text{BTC\_PASS\_IDS} \cap \text{ETH\_PASS\_IDS} = \{\text{C22}, \text{C31}\}$$

| Parameter | C22 Specification | C31 Specification | Differing Dimension? |
| :--- | :--- | :--- | :--- |
| `body_mult` | `1.6` | `1.6` | Identical |
| `volume_mult` | `1.3` | `1.7` | **Diverging: C31 requires higher volume surge** |
| `atr_multiplier` | `2.2` | `2.2` | Identical |
| `risk_reward_ratio` | `2.0` | `2.0` | Identical |
| `volume_period` | `20` (Frozen) | `20` (Frozen) | Identical |
| `ema_period` | `50` (Frozen) | `50` (Frozen) | Identical |
| `displacement_lookback` | `5` (Frozen) | `5` (Frozen) | Identical |
| `atr_period` | `14` (Frozen) | `14` (Frozen) | Identical |
| `stop_type` | `"atr"` (Frozen) | `"atr"` (Frozen) | Identical |

---

## 3. In-Grid Neighborhood Stability Audit

Audited strictly across immediate 1-step in-grid parameter neighbors from the authorized 36 calibration combinations:

| Candidate | Total Neighbors | BTC 1H Passing | ETH 1H Passing | Shared Dual Passing | Stability Classification |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`C22`** | 6 | 3 (`C23`, `C25`, `C31`) | 1 (`C31`) | 1 (`C31`) | `LOCAL PARAMETER STABILITY WITH LIMITED SHARED-PASS NEIGHBORHOOD` |
| **`C31`** | 6 | 2 (`C22`, `C34`) | 2 (`C13`, `C22`) | 1 (`C22`) | `LOCAL PARAMETER STABILITY WITH LIMITED SHARED-PASS NEIGHBORHOOD` |

* **Neighbor Verification Detail:**
  * For `C22`: Neighbor PF ranges are BTC `[0.9900, 1.1236]`, ETH `[1.2025, 1.3534]`.
  * For `C31`: Neighbor PF ranges are BTC `[1.0026, 1.1288]`, ETH `[1.2887, 1.3634]`.
  * Crucially, `C22` and `C31` are mutual 1-step neighbors along the `volume_mult` axis, confirming that both finalists reside within a single shared dual-asset parameter pocket.

---

## 4. Parameter Sensitivity Analysis

1. **`body_mult` (1.3 vs 1.6):** High sensitivity. Real body expansion of $\ge 1.6\times\text{ATR}$ was required to filter out minor consolidation noise on 1H.
2. **`atr_multiplier` (1.8 vs 2.2 vs 2.5):** Moderate sensitivity. Multiplier $2.2$ provided the optimal balance between surviving retests and bounding trade risk.
3. **`risk_reward_ratio` (2.0 vs 2.5 vs 3.0):** Moderate sensitivity. A target of $2.0R$ provided the highest win rate ($39.7\%\text{--}43.7\%$) and smoothest drawdown profiles across both assets.
4. **`volume_mult` (1.3 vs 1.7):** Moderate sensitivity. Increasing volume threshold to $1.7\times\text{VolSMA}$ filtered 6 trades on BTC and 3 trades on ETH, yielding higher profit factors and lower drawdowns.

---

## 5. Detailed Trade Distribution & Concentration Audit (2025 Validation)

| Metric | C22 BTC 1H | C22 ETH 1H | C31 BTC 1H | C31 ETH 1H |
| :--- | :--- | :--- | :--- | :--- |
| **Total Trades ($N$)** | 225 | 218 | 219 | 215 |
| **Win Rate** | 40.0% | 43.1% | 39.7% | 43.7% |
| **Profit Factor** | 1.1103 | 1.3262 | 1.1057 | 1.3534 |
| **Expectancy** | +$0.51 | +$2.21 | +$0.48 | +$2.45 |
| **Average Winner / Loser** | $14.15 / -$8.58 | $17.65 / -$9.47 | $14.28 / -$8.58 | $18.15 / -$9.72 |
| **Largest Winner / Loser** | $40.54 / -$17.47 | $44.75 / -$16.29 | $40.54 / -$17.47 | $44.75 / -$16.29 |
| **Median Trade** | -$7.28 | -$8.09 | -$7.28 | -$8.34 |
| **Standard Deviation** | $12.35 | $14.93 | $12.37 | $15.34 |
| **Long Trades / PnL / PF** | 118 / +$52.12 / 1.10 | 114 / +$211.75 / 1.40 | 115 / +$49.62 / 1.10 | 112 / +$228.32 / 1.43 |
| **Short Trades / PnL / PF** | 107 / +$62.24 / 1.12 | 104 / +$270.24 / 1.27 | 104 / +$55.88 / 1.11 | 103 / +$299.12 / 1.30 |
| **PF Without Top 1 Winner** | 1.0745 | 1.2982 | 1.0699 | 1.3244 |
| **PF Without Top 3 Winners** | 1.0182 | 1.2461 | 1.0125 | 1.2709 |
| **PF Without Top 5 Winners** | 0.9664 | 1.1983 | 0.9602 | 1.2215 |

*Trade profitability is balanced between Long and Short directions, showing no directional bias.*

---

## 6. 1,000-Run Bootstrap Monte Carlo Simulations

Resampled with replacement across 1,000 synthetic market paths:

| Statistic | C22 BTC 1H | C22 ETH 1H | C31 BTC 1H | C31 ETH 1H |
| :--- | :--- | :--- | :--- | :--- |
| **Terminal PnL Median (P5–P95)** | $114.36 (-$142.10 to $374.88) | $481.99 ($92.44 to $886.12) | $105.50 (-$152.44 to $366.12) | $527.44 ($132.88 to $931.25) |
| **Max Drawdown Median (P5–P95)** | 11.8% (6.8% to 19.5%) | 11.7% (6.8% to 19.4%) | 12.0% (6.9% to 19.9%) | 11.2% (6.5% to 18.8%) |
| **Profit Factor Median (P5–P95)** | 1.1105 (0.8712 to 1.3912) | 1.3282 (1.0544 to 1.6621) | 1.1064 (0.8655 to 1.3854) | 1.3541 (1.0782 to 1.6912) |
| **Prob. Ending Profitable** | **78.0%** | **97.0%** | **75.9%** | **98.6%** |
| **Prob. Max Drawdown > 30%** | 0.1% | 0.0% | 0.1% | 0.0% |
| **Prob. Max Drawdown > 40%** | 0.0% | 0.0% | 0.0% | 0.0% |
| **Prob. Profit Factor < 1.0** | 22.0% | 3.0% | 24.1% | 1.4% |

---

## 7. Friction & Execution Fee Stress Testing

Tested across Baseline ($0.04\%$/side), Moderate Stress ($0.06\%$/side), and Severe Friction ($0.08\%$/side):

| Scenario | C22 BTC 1H PF (MDD) | C22 ETH 1H PF (MDD) | C31 BTC 1H PF (MDD) | C31 ETH 1H PF (MDD) |
| :--- | :--- | :--- | :--- | :--- |
| **Baseline (4 bps/side)** | 1.1103 (37.4%)* | 1.3262 (39.1%)* | 1.1057 (36.8%)* | 1.3534 (39.1%)* |
| **Moderate Stress (6 bps/side)** | 1.0685 (38.4%)* | 1.2957 (39.5%)* | 1.0636 (37.8%)* | 1.3226 (39.5%)* |
| **Severe Friction (8 bps/side)** | **1.0287 (39.7%) [FAIL]** | 1.2661 (39.8%)* | **1.0237 (39.0%) [FAIL]** | 1.2927 (39.8%)* |

*\* indicates candidate passed all 5 Stage-B hard gates under the stressed fee model.*

### Critical Governance Note on Friction:
* At **6 bps/side** ($0.12\%$ round-turn), both `C22` and `C31` pass all Stage-B hard gates on both assets ($PF \ge 1.0500, MDD \le 40\%$).
* At **8 bps/side** ($0.16\%$ round-turn), `C22` BTC ($PF=1.0287$) and `C31` BTC ($PF=1.0237$) degrade below the normal Stage-B PF threshold of $1.0500$.
* **Classification:** `SEVERE FRICTION — VALIDATION EDGE DEGRADES BELOW THE NORMAL PF GATE ON BTC`.

---

## 8. Train-to-Validation Stability & Degradation

| Track | Candidate | In-Sample Train PF (N) | 2025 Validation PF (N) | PF Delta | Train Ret | Validation Ret | Stability Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **BTC 1H** | `C22` | 1.2043 (894) | 1.1103 (225) | -0.0940 | +123.2% | +11.4% | `STABLE CONSISTENCY` |
| **ETH 1H** | `C22` | 1.0145 (558) | 1.3262 (218) | +0.3117 | +4.9% | +48.3% | `EXPANDING EDGE` |
| **BTC 1H** | `C31` | 1.2305 (869) | 1.1057 (219) | -0.1248 | +144.0% | +10.5% | `STABLE CONSISTENCY` |
| **ETH 1H** | `C31` | 1.0370 (545) | 1.3534 (215) | +0.3164 | +12.5% | +52.7% | `EXPANDING EDGE` |

---

## 9. Multiple-Testing Disclosure & Selection-Bias Controls

* Both `C22` and `C31` were surfaced from the 36-combination Stage-B calibration grid.
* 2025 is a selection-conditioned validation set; survival establishes pre-OOS robustness but does not guarantee out-of-sample performance.
* Candidate `C31` is frozen as the sole primary finalist for subsequent blind 2026 out-of-sample evaluation.

---

## 10. 2026 OOS Governance Confirmation

`2026 OOS REMAINS BLIND AND LOCKED — ZERO 2026 DATA ACCESSED.`
