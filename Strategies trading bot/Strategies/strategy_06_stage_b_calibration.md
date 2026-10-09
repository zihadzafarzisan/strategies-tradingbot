# Strategy Family #6 (Trend Channel Breakout) Stage-B Calibration Report

**Protocol:** `PROTOCOL-STRATEGY-06-V1.0`  
**Strategy Family:** `TrendChannelBreakoutStrategy` (`trend_channel_breakout`)  
**Execution Date:** 2026-09-11 23:55:35 UTC  
**Total Combinations Evaluated:** 36  
**Total Backtests Executed:** 36 combos $\times$ 4 tracks $\times$ 2 slices = 288  
**OOS Status:** 2026 dataset strictly locked and excluded (`timestamp < 2026-01-01 00:00:00 UTC`).

---

## 1. Executive Summary & Dual-Asset Timeframe Decisions

| Timeframe | BTC Passing Candidates | ETH Passing Candidates | Shared (Intersection) Count | Shared Candidate IDs | Timeframe Decision |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **4H** | 0/36 (Top: `C01`) | 14/36 (Top: `C18`) | **0** | NONE | **`FAILED_DUAL_ASSET_VALIDATION`** |
| **1H** | 0/36 (Top: `C01`) | 11/36 (Top: `C15`) | **0** | NONE | **`FAILED_DUAL_ASSET_VALIDATION`** |

---

## 2. Track Summary & Top Candidates

### Track: `BTCUSDT_4H`
* **Passing Validation Count:** 0/36 candidates
* **Top Candidate ID:** `C01` 
* **Parameters:** `{'channel_period': 20, 'ema_period': 50, 'adx_period': 14, 'adx_threshold': 20.0, 'atr_period': 14, 'atr_multiplier': 1.8, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=650$, $WR=41.1\%$, $PF=1.2766$, $E=\$2.23$, $\text{Ret}=145.2\%$, $MDD=35.8\%$
* **Validation (2025) Metrics:** $N=126$, $WR=34.1\%$, $PF=0.9000$, $E=\$-0.62$, $\text{Ret}=-7.8\%$, $MDD=35.4\%$, $\text{Score}=-0.9006$
* **Gate Result:** **FAIL** (Reasons: `['Negative/zero expectancy: -0.62 <= 0.00', 'Profit factor below threshold: 0.90 < 1.05']`)
* **In-Grid Neighbor Stability:** Spread = 0.0008, Failing Neighbors = 6/6, Isolated Spike = `False`

### Track: `ETHUSDT_4H`
* **Passing Validation Count:** 14/36 candidates
* **Top Candidate ID:** `C18` 
* **Parameters:** `{'channel_period': 20, 'ema_period': 50, 'adx_period': 14, 'adx_threshold': 25.0, 'atr_period': 14, 'atr_multiplier': 2.5, 'risk_reward_ratio': 3.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=215$, $WR=29.8\%$, $PF=1.0987$, $E=\$0.82$, $\text{Ret}=17.6\%$, $MDD=34.8\%$
* **Validation (2025) Metrics:** $N=72$, $WR=29.2\%$, $PF=1.1199$, $E=\$0.91$, $\text{Ret}=6.6\%$, $MDD=19.5\%$, $\text{Score}=0.2365$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.4175, Failing Neighbors = 5/6, Isolated Spike = `False`

### Track: `BTCUSDT_1H`
* **Passing Validation Count:** 0/36 candidates
* **Top Candidate ID:** `C01` 
* **Parameters:** `{'channel_period': 20, 'ema_period': 50, 'adx_period': 14, 'adx_threshold': 20.0, 'atr_period': 14, 'atr_multiplier': 1.8, 'risk_reward_ratio': 2.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=2257$, $WR=34.1\%$, $PF=0.8806$, $E=\$-0.36$, $\text{Ret}=-80.5\%$, $MDD=86.6\%$
* **Validation (2025) Metrics:** $N=541$, $WR=32.5\%$, $PF=0.7249$, $E=\$-0.86$, $\text{Ret}=-46.7\%$, $MDD=60.5\%$, $\text{Score}=-0.9000$
* **Gate Result:** **FAIL** (Reasons: `['Negative/zero expectancy: -0.86 <= 0.00', 'Profit factor below threshold: 0.72 < 1.05', 'Excessive max drawdown: 60.5% > 40.0%']`)
* **In-Grid Neighbor Stability:** Spread = 0.0000, Failing Neighbors = 6/6, Isolated Spike = `False`

### Track: `ETHUSDT_1H`
* **Passing Validation Count:** 11/36 candidates
* **Top Candidate ID:** `C15` 
* **Parameters:** `{'channel_period': 20, 'ema_period': 50, 'adx_period': 14, 'adx_threshold': 25.0, 'atr_period': 14, 'atr_multiplier': 2.2, 'risk_reward_ratio': 3.0, 'stop_type': 'atr'}`
* **Train Metrics:** $N=838$, $WR=25.9\%$, $PF=0.8931$, $E=\$-0.48$, $\text{Ret}=-40.6\%$, $MDD=72.9\%$
* **Validation (2025) Metrics:** $N=298$, $WR=32.2\%$, $PF=1.2466$, $E=\$2.09$, $\text{Ret}=62.2\%$, $MDD=37.2\%$, $\text{Score}=0.1943$
* **Gate Result:** **PASS** (Reasons: `[]`)
* **In-Grid Neighbor Stability:** Spread = 0.4901, Failing Neighbors = 2/6, Isolated Spike = `False`

---

## 3. Complete 36-Candidate Performance Matrix

| ID | Channel Period | ADX Thresh | ATR Mult | RR | BTC 4H Val PF (N) | ETH 4H Val PF (N) | BTC 1H Val PF (N) | ETH 1H Val PF (N) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `C01` | 20 | 20.0 | 1.8 | 2.0 | 0.90 (126) | 1.00 (123) | 0.72 (541) | 1.06 (493) |
| `C02` | 20 | 20.0 | 1.8 | 2.5 | 0.86 (119) | 1.06 (119)* | 0.75 (512) | 1.12 (463) |
| `C03` | 20 | 20.0 | 1.8 | 3.0 | 0.88 (113) | 1.09 (111)* | 0.76 (488) | 1.25 (438) |
| `C04` | 20 | 20.0 | 2.2 | 2.0 | 0.88 (116) | 1.07 (117)* | 0.84 (500) | 1.08 (454) |
| `C05` | 20 | 20.0 | 2.2 | 2.5 | 0.92 (102) | 1.12 (106)* | 0.84 (465) | 1.14 (418) |
| `C06` | 20 | 20.0 | 2.2 | 3.0 | 0.95 (95) | 1.08 (101)* | 0.83 (428) | 1.16 (383) |
| `C07` | 20 | 20.0 | 2.5 | 2.0 | 0.91 (111) | 1.07 (105) | 0.87 (461) | 1.15 (426)* |
| `C08` | 20 | 20.0 | 2.5 | 2.5 | 0.91 (96) | 0.97 (99) | 0.80 (412) | 1.14 (384) |
| `C09` | 20 | 20.0 | 2.5 | 3.0 | 0.92 (84) | 1.10 (89)* | 0.84 (391) | 1.11 (349) |
| `C10` | 20 | 25.0 | 1.8 | 2.0 | 0.89 (87) | 0.96 (99) | 0.71 (374) | 1.03 (358) |
| `C11` | 20 | 25.0 | 1.8 | 2.5 | 0.90 (84) | 1.03 (96) | 0.73 (357) | 1.06 (342) |
| `C12` | 20 | 25.0 | 1.8 | 3.0 | 0.90 (80) | 1.05 (90) | 0.74 (346) | 1.21 (330) |
| `C13` | 20 | 25.0 | 2.2 | 2.0 | 0.91 (83) | 1.04 (95) | 0.77 (349) | 1.11 (337)* |
| `C14` | 20 | 25.0 | 2.2 | 2.5 | 1.00 (78) | 1.04 (87) | 0.81 (334) | 1.20 (316)* |
| `C15` | 20 | 25.0 | 2.2 | 3.0 | 1.00 (72) | 1.01 (85) | 0.77 (307) | 1.25 (298)* |
| `C16` | 20 | 25.0 | 2.5 | 2.0 | 0.87 (81) | 1.00 (88) | 0.81 (334) | 1.10 (320)* |
| `C17` | 20 | 25.0 | 2.5 | 2.5 | 0.86 (73) | 0.98 (83) | 0.80 (311) | 1.19 (296)* |
| `C18` | 20 | 25.0 | 2.5 | 3.0 | 0.79 (70) | 1.12 (72)* | 0.78 (289) | 1.18 (284)* |
| `C19` | 30 | 20.0 | 1.8 | 2.0 | 0.92 (109) | 1.04 (106) | 0.76 (453) | 1.02 (417) |
| `C20` | 30 | 20.0 | 1.8 | 2.5 | 0.91 (104) | 1.16 (102)* | 0.81 (431) | 1.08 (396) |
| `C21` | 30 | 20.0 | 1.8 | 3.0 | 0.91 (99) | 1.19 (96)* | 0.78 (409) | 1.19 (381) |
| `C22` | 30 | 20.0 | 2.2 | 2.0 | 0.87 (102) | 1.09 (101)* | 0.91 (423) | 1.02 (389) |
| `C23` | 30 | 20.0 | 2.2 | 2.5 | 0.92 (95) | 1.09 (94)* | 0.87 (394) | 1.13 (369) |
| `C24` | 30 | 20.0 | 2.2 | 3.0 | 0.96 (87) | 1.02 (89) | 0.87 (367) | 1.19 (338) |
| `C25` | 30 | 20.0 | 2.5 | 2.0 | 0.93 (98) | 0.99 (96) | 0.91 (398) | 1.12 (370) |
| `C26` | 30 | 20.0 | 2.5 | 2.5 | 0.95 (87) | 0.92 (89) | 0.83 (363) | 1.16 (343) |
| `C27` | 30 | 20.0 | 2.5 | 3.0 | 0.98 (77) | 1.01 (83) | 0.87 (338) | 1.09 (314) |
| `C28` | 30 | 25.0 | 1.8 | 2.0 | 0.86 (80) | 1.00 (88) | 0.69 (331) | 1.02 (317) |
| `C29` | 30 | 25.0 | 1.8 | 2.5 | 0.86 (77) | 1.10 (86)* | 0.73 (317) | 1.05 (303) |
| `C30` | 30 | 25.0 | 1.8 | 3.0 | 0.83 (73) | 1.13 (82)* | 0.71 (305) | 1.18 (295)* |
| `C31` | 30 | 25.0 | 2.2 | 2.0 | 0.86 (76) | 1.07 (85)* | 0.82 (309) | 1.05 (301) |
| `C32` | 30 | 25.0 | 2.2 | 2.5 | 0.89 (72) | 1.05 (80) | 0.83 (293) | 1.14 (290) |
| `C33` | 30 | 25.0 | 2.2 | 3.0 | 0.98 (67) | 0.96 (77) | 0.81 (273) | 1.21 (271)* |
| `C34` | 30 | 25.0 | 2.5 | 2.0 | 0.80 (74) | 0.94 (83) | 0.85 (296) | 1.05 (290) |
| `C35` | 30 | 25.0 | 2.5 | 2.5 | 0.84 (68) | 0.86 (77) | 0.83 (279) | 1.14 (271)* |
| `C36` | 30 | 25.0 | 2.5 | 3.0 | 0.77 (64) | 1.00 (70) | 0.84 (259) | 1.09 (258)* |

\* indicates candidate passed all validation hard gates ($N \ge 15, PF \ge 1.05, E > 0, MDD \le 40\%, L=0$).

---

## 4. 2026 OOS Protection Verification

* **OOS Status:** Fully locked and untouched.
* **Maximum Timestamp Evaluated:** Strictly $\le 2025-12-31 23:59:59 UTC$ across all 288 backtests.
* **Next Step:** Awaiting formal human gatekeeper review.

---
*Report generated automatically by `scripts/run_stage_06_b.py`.*
