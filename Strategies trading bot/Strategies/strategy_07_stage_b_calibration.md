# Strategy Family #7 (Volume Displacement Continuation) Stage-B Calibration Report

**Protocol:** `PROTOCOL-STRATEGY-07-V1.0` (Document Revision: 1.0.1)  
**Strategy Family:** `VolumeDisplacementContinuationStrategy` (`volume_displacement_continuation`)  
**Execution Date:** 2026-09-12 00:36:25 UTC  
**Total Configurations Evaluated:** 37 (1 Baseline Comparator `C00` + 36 Calibration Candidates `C01`–`C36`)  
**Total Backtests Executed:** 37 configs $\times$ 4 tracks $\times$ 2 slices = 296  
**OOS Status:** 2026 dataset strictly locked and excluded (`timestamp < 2026-01-01 00:00:00 UTC`).

---

## 1. Executive Summary & Dual-Asset Timeframe Decisions

| Timeframe | Baseline C00 Both Passed? | BTC Calib Passed (of 36) | ETH Calib Passed (of 36) | Shared Calibration Count | Shared Candidate IDs | Timeframe Decision |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **4H** | **NO** | 0/36 (Top: `C01`) | 36/36 (Top: `C23`) | **0** | NONE | **`FAILED_DUAL_ASSET_VALIDATION`** |
| **1H** | **NO** | 5/36 (Top: `C31`) | 3/36 (Top: `C31`) | **2** | `C22`, `C31` | **`QUALIFIES_FOR_DUAL_ASSET_SHORTLIST`** |

---

## 2. Track Summary & Top Candidates

### Track: `BTCUSDT_4H`
* **Baseline Comparator (`C00`):** $N=60, WR=21.7\%, PF=0.5169, E=\$-3.08, MDD=43.8\%$ $\rightarrow$ **FAIL**
* **Passing Calibration Candidates:** 0/36 candidates
* **Top Calibration Candidate ID:** `C01`
* **Top Candidate Parameters:** `{'body_mult': 1.3, 'volume_mult': 1.3, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 1.8, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Top Candidate Train Metrics:** $N=394$, $WR=41.9\%$, $PF=1.3367$, $E=\$2.48$, $\text{Ret}=97.6\%$, $MDD=37.4\%$
* **Top Candidate Validation (2025) Metrics:** $N=92$, $WR=28.3\%$, $PF=0.6423$, $E=\$-2.04$, $\text{Ret}=-18.7\%$, $MDD=43.4\%$, $\text{Score}=-0.9025$
* **Gate Result:** **FAIL** (Reasons: `['Negative/zero expectancy: -2.04 <= 0.00', 'Profit factor below threshold: 0.64 < 1.05', 'Excessive max drawdown: 43.4% > 40.0%']`)
* **In-Grid Neighbor Stability:** Spread = 0.0026, Failing Neighbors = 6/6, Isolated Spike = `False`

### Track: `ETHUSDT_4H`
* **Baseline Comparator (`C00`):** $N=75, WR=46.7\%, PF=2.0616, E=\$6.42, MDD=21.6\%$ $\rightarrow$ **PASS**
* **Passing Calibration Candidates:** 36/36 candidates
* **Top Calibration Candidate ID:** `C23`
* **Top Candidate Parameters:** `{'body_mult': 1.6, 'volume_mult': 1.3, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.5, 'stop_type': 'atr'}`
* **Top Candidate Train Metrics:** $N=118$, $WR=42.4\%$, $PF=1.6241$, $E=\$4.40$, $\text{Ret}=51.9\%$, $MDD=30.3\%$
* **Top Candidate Validation (2025) Metrics:** $N=66$, $WR=50.0\%$, $PF=2.4761$, $E=\$7.93$, $\text{Ret}=52.4\%$, $MDD=19.7\%$, $\text{Score}=0.5186$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.1128, Failing Neighbors = 0/6, Isolated Spike = `False`

### Track: `BTCUSDT_1H`
* **Baseline Comparator (`C00`):** $N=238, WR=33.2\%, PF=1.0773, E=\$0.36, MDD=37.9\%$ $\rightarrow$ **PASS**
* **Passing Calibration Candidates:** 5/36 candidates
* **Top Calibration Candidate ID:** `C31`
* **Top Candidate Parameters:** `{'body_mult': 1.6, 'volume_mult': 1.7, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Top Candidate Train Metrics:** $N=869$, $WR=42.6\%$, $PF=1.2305$, $E=\$1.66$, $\text{Ret}=144.0\%$, $MDD=40.0\%$
* **Top Candidate Validation (2025) Metrics:** $N=219$, $WR=39.7\%$, $PF=1.1057$, $E=\$0.48$, $\text{Ret}=10.5\%$, $MDD=36.8\%$, $\text{Score}=0.1117$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.4728, Failing Neighbors = 4/6, Isolated Spike = `False`

### Track: `ETHUSDT_1H`
* **Baseline Comparator (`C00`):** $N=240, WR=39.2\%, PF=1.3681, E=\$3.08, MDD=44.0\%$ $\rightarrow$ **FAIL**
* **Passing Calibration Candidates:** 3/36 candidates
* **Top Calibration Candidate ID:** `C31`
* **Top Candidate Parameters:** `{'body_mult': 1.6, 'volume_mult': 1.7, 'volume_period': 20, 'ema_period': 50, 'displacement_lookback': 5, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Top Candidate Train Metrics:** $N=545$, $WR=37.8\%$, $PF=1.0370$, $E=\$0.23$, $\text{Ret}=12.5\%$, $MDD=54.9\%$
* **Top Candidate Validation (2025) Metrics:** $N=215$, $WR=43.7\%$, $PF=1.3534$, $E=\$2.45$, $\text{Ret}=52.7\%$, $MDD=39.1\%$, $\text{Score}=0.1834$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.5052, Failing Neighbors = 4/6, Isolated Spike = `False`

---

## 3. Complete 37-Configuration Performance Matrix

| ID | Type | Body Mult | Vol Mult | ATR Mult | RR | BTC 4H Val PF (N) | ETH 4H Val PF (N) | BTC 1H Val PF (N) | ETH 1H Val PF (N) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `C00` | Baseline | 1.5 | 1.5 | 2.0 | 2.5 | 0.52 (60) | 2.06 (75)* | 1.08 (238)* | 1.37 (240) |
| `C01` | Calib | 1.3 | 1.3 | 1.8 | 2.0 | 0.64 (92) | 1.42 (98)* | 0.97 (342) | 1.14 (316) |
| `C02` | Calib | 1.3 | 1.3 | 1.8 | 2.5 | 0.68 (91) | 1.64 (90)* | 0.98 (319) | 1.25 (296) |
| `C03` | Calib | 1.3 | 1.3 | 1.8 | 3.0 | 0.50 (83) | 1.98 (85)* | 0.97 (292) | 1.30 (291) |
| `C04` | Calib | 1.3 | 1.3 | 2.2 | 2.0 | 0.72 (87) | 1.98 (87)* | 1.11 (301) | 1.20 (278) |
| `C05` | Calib | 1.3 | 1.3 | 2.2 | 2.5 | 0.51 (78) | 2.34 (78)* | 1.06 (273) | 1.26 (270) |
| `C06` | Calib | 1.3 | 1.3 | 2.2 | 3.0 | 0.53 (76) | 1.79 (58)* | 1.06 (259) | 1.25 (256) |
| `C07` | Calib | 1.3 | 1.3 | 2.5 | 2.0 | 0.72 (79) | 2.20 (78)* | 1.10 (277) | 1.23 (272) |
| `C08` | Calib | 1.3 | 1.3 | 2.5 | 2.5 | 0.64 (71) | 2.04 (58)* | 1.02 (258) | 1.35 (255) |
| `C09` | Calib | 1.3 | 1.3 | 2.5 | 3.0 | 0.71 (61) | 2.59 (49)* | 1.12 (249) | 1.20 (222) |
| `C10` | Calib | 1.3 | 1.7 | 1.8 | 2.0 | 0.65 (83) | 1.24 (93)* | 0.95 (307) | 1.23 (297) |
| `C11` | Calib | 1.3 | 1.7 | 1.8 | 2.5 | 0.68 (82) | 1.53 (86)* | 0.95 (302) | 1.35 (277) |
| `C12` | Calib | 1.3 | 1.7 | 1.8 | 3.0 | 0.48 (74) | 1.79 (82)* | 0.91 (280) | 1.39 (272) |
| `C13` | Calib | 1.3 | 1.7 | 2.2 | 2.0 | 0.73 (78) | 1.87 (83)* | 1.08 (286) | 1.30 (260)* |
| `C14` | Calib | 1.3 | 1.7 | 2.2 | 2.5 | 0.54 (71) | 2.14 (75)* | 1.00 (264) | 1.35 (252) |
| `C15` | Calib | 1.3 | 1.7 | 2.2 | 3.0 | 0.56 (69) | 1.54 (55)* | 0.95 (254) | 1.34 (238) |
| `C16` | Calib | 1.3 | 1.7 | 2.5 | 2.0 | 0.71 (71) | 2.03 (75)* | 1.07 (267) | 1.31 (255) |
| `C17` | Calib | 1.3 | 1.7 | 2.5 | 2.5 | 0.68 (65) | 1.78 (55)* | 0.94 (251) | 1.44 (239) |
| `C18` | Calib | 1.3 | 1.7 | 2.5 | 3.0 | 0.80 (56) | 2.23 (46)* | 1.03 (245) | 1.31 (200) |
| `C19` | Calib | 1.6 | 1.3 | 1.8 | 2.0 | 0.84 (57) | 1.31 (76)* | 0.99 (242) | 1.34 (237) |
| `C20` | Calib | 1.6 | 1.3 | 1.8 | 2.5 | 0.92 (56) | 1.48 (73)* | 0.95 (236) | 1.45 (227) |
| `C21` | Calib | 1.6 | 1.3 | 1.8 | 3.0 | 0.61 (50) | 1.67 (71)* | 0.97 (223) | 1.44 (224) |
| `C22` | Calib | 1.6 | 1.3 | 2.2 | 2.0 | 0.84 (53) | 2.41 (70)* | 1.11 (225)* | 1.33 (218)* |
| `C23` | Calib | 1.6 | 1.3 | 2.2 | 2.5 | 0.43 (46) | 2.48 (66)* | 1.05 (211)* | 1.33 (212) |
| `C24` | Calib | 1.6 | 1.3 | 2.2 | 3.0 | 0.52 (46) | 1.34 (52)* | 1.06 (205) | 1.27 (204) |
| `C25` | Calib | 1.6 | 1.3 | 2.5 | 2.0 | 0.68 (48) | 2.47 (65)* | 1.12 (211)* | 1.26 (215) |
| `C26` | Calib | 1.6 | 1.3 | 2.5 | 2.5 | 0.53 (44) | 1.71 (50)* | 1.05 (201) | 1.32 (206) |
| `C27` | Calib | 1.6 | 1.3 | 2.5 | 3.0 | 0.51 (42) | 1.96 (43)* | 1.11 (197) | 1.21 (182) |
| `C28` | Calib | 1.6 | 1.7 | 1.8 | 2.0 | 0.74 (54) | 1.31 (76)* | 1.01 (229) | 1.36 (234) |
| `C29` | Calib | 1.6 | 1.7 | 1.8 | 2.5 | 0.80 (53) | 1.48 (73)* | 0.98 (226) | 1.48 (224) |
| `C30` | Calib | 1.6 | 1.7 | 1.8 | 3.0 | 0.49 (47) | 1.67 (71)* | 0.98 (215) | 1.46 (221) |
| `C31` | Calib | 1.6 | 1.7 | 2.2 | 2.0 | 0.72 (50) | 2.41 (70)* | 1.11 (219)* | 1.35 (215)* |
| `C32` | Calib | 1.6 | 1.7 | 2.2 | 2.5 | 0.39 (45) | 2.48 (66)* | 1.04 (208) | 1.35 (209) |
| `C33` | Calib | 1.6 | 1.7 | 2.2 | 3.0 | 0.47 (45) | 1.34 (52)* | 1.00 (202) | 1.29 (201) |
| `C34` | Calib | 1.6 | 1.7 | 2.5 | 2.0 | 0.55 (45) | 2.47 (65)* | 1.13 (207)* | 1.29 (212) |
| `C35` | Calib | 1.6 | 1.7 | 2.5 | 2.5 | 0.48 (43) | 1.71 (50)* | 1.00 (198) | 1.34 (203) |
| `C36` | Calib | 1.6 | 1.7 | 2.5 | 3.0 | 0.51 (42) | 1.96 (43)* | 1.09 (194) | 1.23 (179) |

\* indicates candidate passed all validation hard gates ($N \ge 15, PF \ge 1.05, E > 0, MDD \le 40\%, L=0$).

---

## 4. 2026 OOS Protection Verification

* **OOS Status:** Fully locked and untouched.
* **Maximum Timestamp Evaluated:** Strictly $\le 2025-12-31 23:59:59 UTC$ across all 296 backtests.
* **Next Step:** Awaiting formal human gatekeeper review.

---
*Report generated automatically by `scripts/run_stage_07_b.py`.*
