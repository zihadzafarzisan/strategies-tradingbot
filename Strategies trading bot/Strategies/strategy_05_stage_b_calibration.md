# Strategy Family #5 (Volatility Squeeze Breakout) Stage-B Calibration Report

**Protocol:** `PROTOCOL-STRATEGY-05-V1.0`  
**Strategy Family:** `VolatilitySqueezeBreakoutStrategy` (`volatility_squeeze_breakout`)  
**Execution Date:** 2026-09-11 22:17:58 UTC  
**Total Combinations Evaluated:** 48  
**Total Backtests Executed:** 48 combos $\times$ 4 tracks $\times$ 2 slices = 384  
**OOS Status:** 2026 dataset strictly locked and excluded (`timestamp < 2026-01-01 00:00:00 UTC`).

---

## 1. Executive Summary & Dual-Asset Timeframe Decisions

| Timeframe | BTC Passing Candidates | ETH Passing Candidates | Shared (Intersection) Count | Shared Candidate IDs | Timeframe Decision |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **4H** | 0/48 (Top: `C33`) | 30/48 (Top: `C31`) | **0** | NONE | **`FAILED_DUAL_ASSET_VALIDATION`** |
| **1H** | 9/48 (Top: `C16`) | 1/48 (Top: `C11`) | **0** | NONE | **`FAILED_DUAL_ASSET_VALIDATION`** |

---

## 2. Track Summary & Top Candidates

### Track: `BTCUSDT_4H`
* **Passing Validation Count:** 0/48 candidates
* **Top Candidate ID:** `C33` 
* **Parameters:** `{'bb_period': 20, 'bb_std': 1.8, 'kc_period': 20, 'kc_atr_period': 14, 'kc_mult': 1.8, 'mom_period': 12, 'volume_mult': 1.0, 'volume_period': 20, 'atr_period': 14, 'atr_multiplier': 1.8, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=589$, $WR=38.2\%$, $PF=1.0822$, $E=\$0.63$, $\text{Ret}=37.0\%$, $MDD=44.0\%$
* **Validation (2025) Metrics:** $N=113$, $WR=31.9\%$, $PF=0.8057$, $E=\$-1.23$, $\text{Ret}=-13.9\%$, $MDD=36.1\%$, $\text{Score}=-0.9011$
* **Gate Result:** **FAIL** (Reasons: `['Negative/zero expectancy: -1.23 <= 0.00', 'Profit factor below threshold: 0.81 < 1.05']`)
* **In-Grid Neighbor Stability:** Spread = 0.0020, Failing Neighbors = 6/6, Isolated Spike = `False`

### Track: `ETHUSDT_4H`
* **Passing Validation Count:** 30/48 candidates
* **Top Candidate ID:** `C31` 
* **Parameters:** `{'bb_period': 20, 'bb_std': 2.0, 'kc_period': 20, 'kc_atr_period': 14, 'kc_mult': 1.5, 'mom_period': 12, 'volume_mult': 1.2, 'volume_period': 20, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=222$, $WR=35.6\%$, $PF=0.9958$, $E=\$-0.03$, $\text{Ret}=-0.6\%$, $MDD=40.3\%$
* **Validation (2025) Metrics:** $N=54$, $WR=44.4\%$, $PF=1.4712$, $E=\$2.78$, $\text{Ret}=15.0\%$, $MDD=18.8\%$, $\text{Score}=0.2971$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.4397, Failing Neighbors = 1/6, Isolated Spike = `False`

### Track: `BTCUSDT_1H`
* **Passing Validation Count:** 9/48 candidates
* **Top Candidate ID:** `C16` 
* **Parameters:** `{'bb_period': 20, 'bb_std': 2.0, 'kc_period': 20, 'kc_atr_period': 14, 'kc_mult': 1.2, 'mom_period': 12, 'volume_mult': 1.2, 'volume_period': 20, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.5, 'stop_type': 'atr'}`
* **Train Metrics:** $N=938$, $WR=28.5\%$, $PF=0.7907$, $E=\$-0.71$, $\text{Ret}=-66.8\%$, $MDD=78.8\%$
* **Validation (2025) Metrics:** $N=147$, $WR=35.4\%$, $PF=1.1556$, $E=\$0.60$, $\text{Ret}=8.8\%$, $MDD=37.3\%$, $\text{Score}=0.1123$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.5034, Failing Neighbors = 3/6, Isolated Spike = `False`

### Track: `ETHUSDT_1H`
* **Passing Validation Count:** 1/48 candidates
* **Top Candidate ID:** `C11` 
* **Parameters:** `{'bb_period': 20, 'bb_std': 2.0, 'kc_period': 20, 'kc_atr_period': 14, 'kc_mult': 1.2, 'mom_period': 12, 'volume_mult': 1.0, 'volume_period': 20, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=565$, $WR=31.1\%$, $PF=0.7854$, $E=\$-0.93$, $\text{Ret}=-52.8\%$, $MDD=67.5\%$
* **Validation (2025) Metrics:** $N=171$, $WR=39.2\%$, $PF=1.1229$, $E=\$0.71$, $\text{Ret}=12.2\%$, $MDD=36.4\%$, $\text{Score}=0.1240$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.0001, Failing Neighbors = 6/6, Isolated Spike = `False`

---

## 3. Complete 48-Candidate Performance Matrix

| ID | KC Mult | BB Std | Vol Mult | ATR Mult | RR | BTC 4H Val PF (N) | ETH 4H Val PF (N) | BTC 1H Val PF (N) | ETH 1H Val PF (N) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `C01` | 1.2 | 1.8 | 1.0 | 1.8 | 2.0 | 0.56 (66) | 0.55 (47) | 0.98 (248) | 0.92 (261) |
| `C02` | 1.2 | 1.8 | 1.0 | 1.8 | 2.5 | 0.47 (66) | 0.43 (44) | 0.95 (234) | 0.90 (248) |
| `C03` | 1.2 | 1.8 | 1.0 | 2.2 | 2.0 | 0.43 (60) | 0.47 (45) | 0.94 (230) | 1.01 (241) |
| `C04` | 1.2 | 1.8 | 1.0 | 2.2 | 2.5 | 0.44 (60) | 0.30 (43) | 1.08 (219)* | 0.90 (224) |
| `C05` | 1.2 | 1.8 | 1.2 | 1.8 | 2.0 | 0.56 (58) | 0.43 (42) | 1.03 (229) | 0.89 (238) |
| `C06` | 1.2 | 1.8 | 1.2 | 1.8 | 2.5 | 0.51 (58) | 0.33 (40) | 0.97 (218) | 0.84 (231) |
| `C07` | 1.2 | 1.8 | 1.2 | 2.2 | 2.0 | 0.46 (53) | 0.39 (41) | 0.98 (217) | 0.93 (225) |
| `C08` | 1.2 | 1.8 | 1.2 | 2.2 | 2.5 | 0.51 (54) | 0.28 (39) | 1.12 (206)* | 0.83 (211) |
| `C09` | 1.2 | 2.0 | 1.0 | 1.8 | 2.0 | 0.52 (49) | 0.48 (38) | 1.14 (179)* | 1.02 (182) |
| `C10` | 1.2 | 2.0 | 1.0 | 1.8 | 2.5 | 0.64 (49) | 0.37 (36) | 0.99 (169) | 0.93 (175) |
| `C11` | 1.2 | 2.0 | 1.0 | 2.2 | 2.0 | 0.57 (45) | 0.38 (36) | 1.01 (167) | 1.12 (171)* |
| `C12` | 1.2 | 2.0 | 1.0 | 2.2 | 2.5 | 0.57 (45) | 0.29 (36) | 1.13 (158)* | 0.99 (156) |
| `C13` | 1.2 | 2.0 | 1.2 | 1.8 | 2.0 | 0.51 (45) | 0.32 (34) | 1.15 (167)* | 0.99 (167) |
| `C14` | 1.2 | 2.0 | 1.2 | 1.8 | 2.5 | 0.65 (45) | 0.23 (33) | 0.99 (157) | 0.86 (161) |
| `C15` | 1.2 | 2.0 | 1.2 | 2.2 | 2.0 | 0.57 (41) | 0.27 (33) | 1.04 (156) | 1.01 (159) |
| `C16` | 1.2 | 2.0 | 1.2 | 2.2 | 2.5 | 0.62 (42) | 0.24 (33) | 1.16 (147)* | 0.85 (148) |
| `C17` | 1.5 | 1.8 | 1.0 | 1.8 | 2.0 | 0.71 (87) | 1.07 (101)* | 0.92 (406) | 0.80 (375) |
| `C18` | 1.5 | 1.8 | 1.0 | 1.8 | 2.5 | 0.66 (86) | 1.04 (99) | 0.93 (379) | 0.74 (363) |
| `C19` | 1.5 | 1.8 | 1.0 | 2.2 | 2.0 | 0.70 (80) | 1.13 (97)* | 0.96 (365) | 0.85 (349) |
| `C20` | 1.5 | 1.8 | 1.0 | 2.2 | 2.5 | 0.65 (78) | 1.14 (86)* | 1.03 (336) | 0.81 (327) |
| `C21` | 1.5 | 1.8 | 1.2 | 1.8 | 2.0 | 0.73 (79) | 1.07 (93)* | 0.95 (370) | 0.81 (349) |
| `C22` | 1.5 | 1.8 | 1.2 | 1.8 | 2.5 | 0.70 (79) | 1.06 (91)* | 0.92 (353) | 0.74 (341) |
| `C23` | 1.5 | 1.8 | 1.2 | 2.2 | 2.0 | 0.77 (75) | 1.20 (88)* | 0.98 (343) | 0.82 (332) |
| `C24` | 1.5 | 1.8 | 1.2 | 2.2 | 2.5 | 0.71 (73) | 1.14 (77)* | 1.07 (320)* | 0.78 (313) |
| `C25` | 1.5 | 2.0 | 1.0 | 1.8 | 2.0 | 0.79 (74) | 1.49 (63)* | 0.94 (307) | 0.86 (301) |
| `C26` | 1.5 | 2.0 | 1.0 | 1.8 | 2.5 | 0.71 (73) | 1.28 (61)* | 0.98 (291) | 0.79 (291) |
| `C27` | 1.5 | 2.0 | 1.0 | 2.2 | 2.0 | 0.64 (70) | 1.37 (61)* | 0.98 (285) | 0.88 (285) |
| `C28` | 1.5 | 2.0 | 1.0 | 2.2 | 2.5 | 0.65 (69) | 1.20 (55)* | 1.10 (264)* | 0.84 (270) |
| `C29` | 1.5 | 2.0 | 1.2 | 1.8 | 2.0 | 0.83 (66) | 1.50 (56)* | 0.93 (282) | 0.87 (280) |
| `C30` | 1.5 | 2.0 | 1.2 | 1.8 | 2.5 | 0.77 (66) | 1.33 (54)* | 0.94 (273) | 0.80 (273) |
| `C31` | 1.5 | 2.0 | 1.2 | 2.2 | 2.0 | 0.71 (65) | 1.47 (54)* | 0.98 (271) | 0.84 (270) |
| `C32` | 1.5 | 2.0 | 1.2 | 2.2 | 2.5 | 0.73 (64) | 1.25 (48)* | 1.10 (254)* | 0.80 (259) |
| `C33` | 1.8 | 1.8 | 1.0 | 1.8 | 2.0 | 0.81 (113) | 1.16 (111)* | 0.83 (426) | 0.97 (403) |
| `C34` | 1.8 | 1.8 | 1.0 | 1.8 | 2.5 | 0.87 (111) | 1.21 (106)* | 0.84 (402) | 0.90 (385) |
| `C35` | 1.8 | 1.8 | 1.0 | 2.2 | 2.0 | 0.83 (109) | 1.27 (106)* | 0.93 (384) | 0.92 (377) |
| `C36` | 1.8 | 1.8 | 1.0 | 2.2 | 2.5 | 0.90 (104) | 1.30 (97)* | 0.95 (355) | 0.92 (353) |
| `C37` | 1.8 | 1.8 | 1.2 | 1.8 | 2.0 | 0.87 (101) | 1.18 (105)* | 0.84 (390) | 0.96 (370) |
| `C38` | 1.8 | 1.8 | 1.2 | 1.8 | 2.5 | 0.97 (99) | 1.27 (100)* | 0.83 (374) | 0.90 (359) |
| `C39` | 1.8 | 1.8 | 1.2 | 2.2 | 2.0 | 0.94 (97) | 1.30 (100)* | 0.95 (362) | 0.90 (355) |
| `C40` | 1.8 | 1.8 | 1.2 | 2.2 | 2.5 | 1.03 (92) | 1.31 (91)* | 1.00 (338) | 0.94 (336) |
| `C41` | 1.8 | 2.0 | 1.0 | 1.8 | 2.0 | 0.60 (84) | 1.04 (100) | 0.79 (393) | 0.94 (342) |
| `C42` | 1.8 | 2.0 | 1.0 | 1.8 | 2.5 | 0.62 (83) | 1.10 (95)* | 0.80 (372) | 0.86 (330) |
| `C43` | 1.8 | 2.0 | 1.0 | 2.2 | 2.0 | 0.67 (80) | 1.20 (95)* | 0.86 (355) | 0.90 (321) |
| `C44` | 1.8 | 2.0 | 1.0 | 2.2 | 2.5 | 0.72 (78) | 1.32 (85)* | 0.92 (330) | 0.90 (307) |
| `C45` | 1.8 | 2.0 | 1.2 | 1.8 | 2.0 | 0.63 (74) | 1.10 (94)* | 0.81 (358) | 0.95 (316) |
| `C46` | 1.8 | 2.0 | 1.2 | 1.8 | 2.5 | 0.70 (73) | 1.16 (89)* | 0.82 (344) | 0.87 (307) |
| `C47` | 1.8 | 2.0 | 1.2 | 2.2 | 2.0 | 0.76 (71) | 1.22 (89)* | 0.89 (334) | 0.88 (303) |
| `C48` | 1.8 | 2.0 | 1.2 | 2.2 | 2.5 | 0.81 (69) | 1.32 (80)* | 0.99 (312) | 0.90 (290) |

\* indicates candidate passed all validation hard gates ($N \ge 15, PF \ge 1.05, E > 0, MDD \le 40\%, L=0$).

---

## 4. 2026 OOS Protection Verification

* **OOS Status:** Fully locked and untouched.
* **Maximum Timestamp Evaluated:** Strictly $\le 2025-12-31 23:59:59 UTC$ across all 384 backtests.
* **Next Step:** Awaiting formal human gatekeeper review.

---
*Report generated automatically by `scripts/run_stage_05_b.py`.*
