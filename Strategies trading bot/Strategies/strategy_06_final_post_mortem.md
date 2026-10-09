# Strategy Family #6 (`trend_channel_breakout`) Final Post-Mortem

**Strategy Class:** `TrendChannelBreakoutStrategy` (`src/crypto_quant/strategies/trend_channel_breakout.py`)  
**Strategy Slug:** `trend_channel_breakout`  
**Protocol:** `PROTOCOL-STRATEGY-06-V1.0`  
**Final Governance Status:** `PERMANENTLY REJECTED AND ARCHIVED`  
**2026 OOS Status:** `NEVER ACCESSED / NEVER AUTHORIZED`  

---

## 1. Research Hypothesis & Quantitative Thesis
Strategy Family #6 hypothesized that entering directional breakouts of an $N$-period Donchian Channel, filtered by medium-term EMA trend alignment ($\text{Close} > \text{EMA}_{50}$ for Longs, $< \text{EMA}_{50}$ for Shorts) and Wilder ADX trend strength ($\text{ADX}_{14} \ge \text{threshold}$), would capture directional trend continuation while filtering out range-bound consolidation chop and overcoming transaction fee hurdles via asymmetric ATR trailing targets ($2.0R\text{--}3.0R$).

---

## 2. Stage-A Baseline Screening Summary
Evaluated over 2020/2022–2025:
* **BTCUSDT 4H:** $N = 695, PF = 1.2205, \text{Exp} = +\$3.03, \text{Ret} = +210.4\%, MDD = 41.1\% \rightarrow$ **PASS**
* **BTCUSDT 1H:** $N = 2,566, PF = 0.9202, \text{Exp} = -\$0.29, \text{Ret} = -74.9\%, MDD = 85.4\% \rightarrow$ **PASS** (Non-catastrophic gate)
* **ETHUSDT 4H:** $N = 454, PF = 0.9789, \text{Exp} = -\$0.12, \text{Ret} = -5.4\%, MDD = 48.3\% \rightarrow$ **PASS**
* **ETHUSDT 1H:** $N = 1,730, PF = 0.9902, \text{Exp} = -\$0.04, \text{Ret} = -7.0\%, MDD = 72.2\% \rightarrow$ **PASS**

Both candidate timeframes qualified for Stage-B calibration under non-catastrophic baseline screening rules.

---

## 3. Stage-B Calibration Search Space
A pre-declared, bounded 36-combination grid evaluated across 4 tracks $\times$ 2 slices (288 total backtests):
* `channel_period`: `[20, 30]` (2)
* `adx_threshold`: `[20.0, 25.0]` (2)
* `atr_multiplier`: `[1.8, 2.2, 2.5]` (3)
* `risk_reward_ratio`: `[2.0, 2.5, 3.0]` (3)
* Frozen: `ema_period=50`, `adx_period=14`, `atr_period=14`, `stop_type="atr"`

---

## 4. Dual-Asset Intersection Results (Exact Parameter Match)

Under `PROTOCOL-STRATEGY-06-V1.0` Section 7, dual-asset qualification requires:
$$\text{DUAL\_ASSET\_CANDIDATES} = \text{BTC\_PASSING\_IDS} \cap \text{ETH\_PASSING\_IDS} \neq \emptyset$$

### 4.1 4H Timeframe
* **BTC 4H Passing Candidates ($N=0$):** `[]` (0/36 passed, 100% failure rate)
* **ETH 4H Passing Candidates ($N=14$):** `['C02', 'C03', 'C04', 'C05', 'C06', 'C09', 'C18', 'C20', 'C21', 'C22', 'C23', 'C29', 'C30', 'C31']`
* **Shared Passing IDs:** `[]` ($\text{Count} = 0$)
* **Timeframe Decision:** `FAILED_DUAL_ASSET_VALIDATION`

### 4.2 1H Timeframe
* **BTC 1H Passing Candidates ($N=0$):** `[]` (0/36 passed, 100% failure rate)
* **ETH 1H Passing Candidates ($N=11$):** `['C07', 'C13', 'C14', 'C15', 'C16', 'C17', 'C18', 'C30', 'C33', 'C35', 'C36']`
* **Shared Passing IDs:** `[]` ($\text{Count} = 0$)
* **Timeframe Decision:** `FAILED_DUAL_ASSET_VALIDATION`

---

## 5. Failure Analysis

### 5.1 Why BTC Failed Completely in 2025
* **BTC 4H:** Across all 36 combinations, 2025 validation performance collapsed ($PF \le 1.0028$, maximum expectancy $\le \$0.00$). 2025 Bitcoin price action was characterized by structural liquidity sweeps outside recent highs/lows followed by rapid mean-reversion, triggering breakout entries at the exact exhaustion point of moves.
* **BTC 1H:** Suffered severe drawdown ($MDD \ge 50\%$) and net losses across all 36 combinations ($PF = 0.69\text{--}0.91$). High-frequency channel breaks on 1H in BTC generated persistent false signals and heavy fee bleed.

### 5.2 ETH-Only Divergence & Single-Asset Quarantine
* ETH demonstrated genuine parameter clustering in 2025 ($14/36$ passed on 4H with $PF = 1.06\text{--}1.19$; $11/36$ passed on 1H with $PF = 1.10\text{--}1.25$).
* **Governance Barrier:** Granting an ad-hoc single-asset exemption for ETH violates the dual-asset research mandate. Multiple past strategy families have displayed promising ETH-only backtests that later failed out-of-sample due to asset-specific curve fitting. ETH results remain quarantined as single-asset observations.

---

## 6. Selection-Bias & Multiple-Testing Limitations
Evaluating 36 combinations across 4 tracks represents 144 candidate-track evaluations. While ETH exhibited multi-neighbor clusters on both 4H and 1H, the total lack of transferability to BTC confirms that the mechanism lacks structural universality across the crypto asset class.

---

## 7. Execution and Infrastructure Integrity
* Standardized futures execution accounting strictly enforced ($0.04\%$ taker fee per side, dynamic slippage, 8-hour funding rates, conservative stop-first bar collision).
* Zero look-ahead: All indicators computed with point-in-time causal shifting; order fills at $t+1$ open.
* Zero 2026 leakage: Verified query-level boundary `end_ms = 1767225600000` (2026-01-01 00:00:00 UTC).

---

## 8. Final Governance Conclusion
`TrendChannelBreakoutStrategy` failed to produce any shared parameter configuration satisfying 2025 validation across both BTC and ETH on either candidate timeframe ($\text{Intersection} = \emptyset$).

**DECISION:**  
`TrendChannelBreakoutStrategy IS PERMANENTLY REJECTED AND ARCHIVED.`  
* **OOS Authorization:** STRICTLY FORBIDDEN (No 2026 evaluation).
* **Anti-Retuning Rule:** No further parameter searches or structural revisions of Strategy Family #6 are permitted.
