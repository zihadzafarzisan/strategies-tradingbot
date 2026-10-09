# Strategy Family #7 (Volume Displacement Continuation) 2026 Out-of-Sample Report

**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0`  
**Authorization Document:** `OOS-AUTH-STRATEGY-07-V1.0`  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`volume_displacement_continuation`)  
**Candidate Evaluated:** `C31`  
**Execution Timestamp:** 2026-09-12 04:49:40 UTC  
**OOS Testing Window:** `2026-01-01 00:00:00 UTC` to `2026-08-31 23:59:59 UTC` (8 Months)  
**Final Dual-Asset OOS Verdict:** **`DUAL_ASSET_OOS_FAILED`**

---

## 1. Executive Summary & Hard Gate Decisions

| Gate Criterion | BTCUSDT 1H Result | BTC Gate Status | ETHUSDT 1H Result | ETH Gate Status | Joint Requirement |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Closed Trades ($N \ge 15$)** | $N = 137$ | **PASS** | $N = 137$ | **PASS** | Mandatory $\ge 15$ |
| **Profit Factor ($PF \ge 1.0500$)** | $PF = 1.0844$ | **PASS** | $PF = 1.2231$ | **PASS** | Mandatory $\ge 1.0500$ |
| **Expectancy ($E > \$0.00$)** | $E = \$0.38$ | **PASS** | $E = \$1.22$ | **PASS** | Mandatory $> \$0.00$ |
| **Max Drawdown ($MDD \le 35.00\%$)** | $MDD = 38.5\%$ | **FAIL** | $MDD = 36.8\%$ | **FAIL** | Mandatory $\le 35.00\%$ |
| **Liquidations ($L == 0$)** | $L = 0$ | **PASS** | $L = 0$ | **PASS** | Zero Liquidations |
| **Overall OOS Status** | **FAIL** | — | **FAIL** | — | **`DUAL_ASSET_OOS_FAILED`** |

---

## 2. Frozen Candidate Parameters (`C31`)

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

---

## 3. Comprehensive Performance Metrics (2026 OOS)

| Metric | BTCUSDT 1H (2026 OOS) | ETHUSDT 1H (2026 OOS) |
| :--- | :--- | :--- |
| **Bars Evaluated** | 5,832 | 5,832 |
| **Total Closed Trades ($N$)** | 137 | 137 |
| **Long / Short Trades** | 60 Long / 77 Short | 78 Long / 59 Short |
| **Winning / Losing Trades** | 52 Wins / 85 Losses | 59 Wins / 78 Losses |
| **Win Rate** | 38.0% | 43.1% |
| **Profit Factor** | 1.0844 | 1.2231 |
| **Trade Expectancy** | $0.38 | $1.22 |
| **Net Return** | +5.2% | +16.7% |
| **Net PnL** | $+51.91 | $+166.83 |
| **Max Drawdown** | 38.5% | 36.8% |
| **Sharpe Ratio** | 0.0319 | 0.0966 |
| **Sortino Ratio** | 0.0218 | 0.0612 |
| **Calmar Ratio** | 0.1347 | 0.4529 |
| **Total Exchange Fees** | $49.21 | $49.57 |
| **Total Slippage** | $4968.94 | $152.01 |
| **Total Funding Cost** | $23.08 | $17.32 |
| **Liquidations** | 0 | 0 |
| **Evidence Class** | `ADEQUATE_EVIDENCE` | `ADEQUATE_EVIDENCE` |

---

## 4. Chronological Robustness Progression (Train $\rightarrow$ Validation $\rightarrow$ OOS)

| Track | Phase | Period | Trades ($N$) | Profit Factor | Net Return | Max Drawdown |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **BTC 1H** | In-Sample Train | 2020–2024 (5 Yrs) | 869 | 1.2305 | +144.0% | 40.0% |
| **BTC 1H** | Validation | 2025 (1 Yr) | 219 | 1.1057 | +10.5% | 36.8% |
| **BTC 1H** | **2026 OOS** | **2026 (8 Mos)** | **137** | **1.0844** | **+5.2%** | **38.5%** |
| **ETH 1H** | In-Sample Train | 2022–2024 (3 Yrs) | 545 | 1.0370 | +12.5% | 54.9% |
| **ETH 1H** | Validation | 2025 (1 Yr) | 215 | 1.3534 | +52.7% | 39.1% |
| **ETH 1H** | **2026 OOS** | **2026 (8 Mos)** | **137** | **1.2231** | **+16.7%** | **36.8%** |

---

## 5. Governance Directives & Production Status

* **Anti-Retuning Rule:** No post-OOS parameter modifications or retuning are permitted.
* **Production Next Steps:** Awaiting formal human review to determine production deployment readiness.

---
*Report generated automatically by `scripts/run_stage_07_oos.py`.*
