# Strategy Family #7 (`volume_displacement_continuation`) Final Post-Mortem

**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Strategy Slug:** `volume_displacement_continuation`  
**Protocol Identifier:** `PROTOCOL-STRATEGY-07-V1.0` (Document Revision: 1.0.1)  
**OOS Authorization Document:** `OOS-AUTH-STRATEGY-07-V1.0`  
**Final Governance Status:** `PERMANENTLY REJECTED AND ARCHIVED`  
**2026 OOS Result:** `DUAL_ASSET_OOS_FAILED` (Pre-Declared MaxDD Ceiling Breached on Both Assets)

---

## 1. Strategy Family #7 Research Objective & Quantitative Thesis

Strategy Family #7 was formulated to test a structural alternative to the failure modes of previous families:
1. **Alternative to Breakout Liquidity Sweeps:** Rather than entering at geometric price extremes (Donchian / Bollinger / Keltner channels, which failed on Bitcoin in Families #5B and #6), Family #7 hypothesized that entering on the *mitigation / retest* of a confirmed volume-displacement impulse and 3-bar Fair Value Gap (FVG) would avoid buying directly into liquidity exhaustion.
2. **Alternative to Counter-Trend Mean Reversion:** Unlike Family #5A (which faded momentum extremes and suffered catastrophic short-side tail risk), Family #7 was strictly directional and aligned with medium-term trend structure ($\text{EMA}_{50}$).
3. **Friction Resilience:** Utilized asymmetric ATR profit targets ($2.0R$) to ensure expected trade profits comfortably exceeded exchange taker friction ($0.08\%$ round-turn).

---

## 2. Stage-A Baseline Screening Summary (`C00` Benchmark)

Evaluated over the full chronological pre-OOS period (BTC: 2020–2025; ETH: 2022–2025) using standard futures execution:
* **BTCUSDT 4H:** $N = 342, PF = 1.3195, \text{Exp} = +\$2.90, \text{Net Return} = +99.22\%, MDD = 44.36\% \rightarrow$ **PASS**
* **BTCUSDT 1H:** $N = 1,213, PF = 1.1729, \text{Exp} = +\$1.39, \text{Net Return} = +168.19\%, MDD = 44.07\% \rightarrow$ **PASS**
* **ETHUSDT 4H:** $N = 214, PF = 2.0465, \text{Exp} = +\$9.84, \text{Net Return} = +210.51\%, MDD = 29.24\% \rightarrow$ **PASS**
* **ETHUSDT 1H:** $N = 873, PF = 1.0964, \text{Exp} = +\$0.60, \text{Net Return} = +52.69\%, MDD = 62.66\% \rightarrow$ **PASS**

Both candidate timeframes passed non-catastrophic baseline screening, advancing to Stage-B.

---

## 3. Stage-B Bounded Calibration & Dual-Asset Intersection

Evaluated across 37 configurations (1 baseline comparator `C00` + 36 calibration candidates `C01`–`C36`) $\times$ 4 tracks $\times$ 2 chronological slices = 296 backtest slices:
* **4H Timeframe:** BTC failed 100% of calibration combinations ($0/36$ passed; top candidate $PF = 0.6423$); ETH passed $36/36$. $\text{Intersection} = \emptyset \rightarrow$ **4H ELIMINATED**.
* **1H Timeframe:** BTC passed 5 candidates (`C04`, `C13`, `C22`, `C28`, `C31`); ETH passed 3 candidates (`C22`, `C25`, `C31`).
* **Exact Mathematical Candidate ID Intersection on 1H:**
  $$\text{DUAL\_ASSET\_CANDIDATES} = \text{BTC\_PASS\_IDS} \cap \text{ETH\_PASS\_IDS} = \{\text{C22}, \text{C31}\}$$

---

## 4. Pre-OOS Robustness Testing & Finalist Selection (`C31`)

Pre-OOS diagnostics were conducted on `C22` and `C31` across multiple dimensions:
1. **In-Grid Neighborhood Stability:** Both candidates reside in a shared parameter pocket along the `volume_mult` axis (`C22` and `C31` are mutual 1-step neighbors). Classified as `LOCAL PARAMETER STABILITY WITH LIMITED SHARED-PASS NEIGHBORHOOD`.
2. **Trade Distribution & Long/Short Symmetry:** Profits were distributed evenly between Longs and Shorts on both assets with no directional decay.
3. **1,000-Run Bootstrap Monte Carlo Simulations:**
   * `C31` achieved $98.6\%$ probability of ending profitable on ETH 1H (median $PF = 1.3541$) and $75.9\%$ on BTC 1H (median $PF = 1.1064$).
4. **Fee / Friction Stress Testing:**
   * Moderate Stress ($0.06\%$/side): Both candidates maintained $PF > 1.0500$ on both assets (`C31` BTC $PF=1.0636$, ETH $PF=1.3226$).
   * Severe Friction ($0.08\%$/side): Classified as `SEVERE FRICTION — VALIDATION EDGE DEGRADES BELOW THE NORMAL PF GATE ON BTC` (`C31` BTC $PF=1.0237$).
5. **Selection Decision:** `C31` was chosen as the sole frozen finalist due to higher volume impulse selectivity (`volume_mult=1.7`), superior ETH validation profit factor ($1.3534$ vs $1.3262$), higher 5-year in-sample train returns on BTC ($+144.0\%$ vs $+123.2\%$), and lower validation drawdown on BTC ($36.8\%$ vs $37.4\%$).

---

## 5. Authorized 2026 Out-of-Sample (OOS) Evaluation

Under `OOS-AUTH-STRATEGY-07-V1.0`, candidate `C31` underwent a single blind evaluation over the pre-declared 8-month window:
* **OOS Window:** `2026-01-01 00:00:00 UTC` to `2026-08-31 23:59:59 UTC` (5,832 one-hour bars)
* **Execution Configuration:** Standard futures ($1,000 capital, 1% risk/trade, max 3 positions, 5x leverage, 4 bps taker fee/side, dynamic slippage, 8h funding rate accounting, conservative stop-first collision).

### 2026 OOS Results & Hard Gate Evaluation:

$$\text{DUAL\_ASSET\_OOS\_PASS} = \text{BTC\_OOS\_PASS} \land \text{ETH\_OOS\_PASS}$$

| Gate Criterion | Pre-Declared Hard Gate | BTCUSDT 1H Result | BTC Status | ETHUSDT 1H Result | ETH Status | Joint Dual-Asset Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Minimum Closed Trades ($N$)** | $N \ge 15$ | $N = 137$ | **PASS** | $N = 137$ | **PASS** | **PASS** |
| **Profit Factor ($PF$)** | $PF \ge 1.0500$ | $PF = 1.0844$ | **PASS** | $PF = 1.2231$ | **PASS** | **PASS** |
| **Trade Expectancy ($E$)** | $E > \$0.00$ | $E = +\$0.38$ | **PASS** | $E = +\$1.22$ | **PASS** | **PASS** |
| **Maximum Drawdown ($MDD$)** | $MDD \le 35.00\%$ | $MDD = 38.5\%$ | **FAIL** (+3.5%) | $MDD = 36.8\%$ | **FAIL** (+1.8%) | **FAIL** |
| **Liquidations ($L$)** | $L == 0$ | $L = 0$ | **PASS** | $L = 0$ | **PASS** | **PASS** |
| **Overall OOS Verdict** | Simultaneous Pass | **FAIL** | — | **FAIL** | — | **`DUAL_ASSET_OOS_FAILED`** |

---

## 6. Why Positive Net Profitability Does NOT Override the MaxDD Failure

In quantitative research governance:
1. **Integrity of Pre-Declared Gates:** The $MDD \le 35.00\%$ ceiling was pre-declared ex-ante in `data/strategy_07_oos_authorization_v1.md`. Relaxing a hard gate after observing performance violates the fundamental principle of scientific testing.
2. **Economic Risk Profile:** Although `C31` generated net positive returns on both assets in 2026 ($+5.2\%$ on BTC, $+16.7\%$ on ETH) and maintained positive expectancy over 137 trades per asset, the drawdown depth ($38.5\%$ on BTC, $36.8\%$ on ETH) demonstrates that the fixed ATR risk model experienced unacceptably clustered loss runs during prolonged 2026 consolidation regimes.
3. **Dual-Asset Mandate:** Because the MaxDD gate was breached on both assets, the strategy cannot be certified as having passed dual-asset out-of-sample validation.

---

## 7. Anti-Retuning Directives & Permanent Archival Status

* **Anti-Retuning Rule:** In accordance with institutional research rules, no parameter modifications, post-OOS calibrations, or candidate substitutions are permitted.
* **Final Verdict:** `VolumeDisplacementContinuationStrategy` (`volume_displacement_continuation`) is **PERMANENTLY REJECTED AND ARCHIVED**.

---

## 8. Key Quantitative Lessons for Future Research (Strategy Family #8)

1. **Volume Displacement Mechanism Holds Positive Edge:** Strategy #7 was the first family in the terminal's research history to produce net positive returns on both major crypto assets in 2026 OOS while overcoming realistic taker fees ($0.08\%$ round-turn). The core premise—entering on volume-confirmed displacement retests rather than breakout peaks—demonstrated structural merit.
2. **Fixed ATR Risk Limits Suffer Drawdown Clustering:** Using static ATR multipliers ($2.2\times\text{ATR}$) with static $2.0R$ targets without regime-adaptive exposure scaling or dynamic trailing stops allowed drawdowns to expand past the $35.00\%$ ceiling during low-volatility chop.
3. **Mandate for Future Architecture:** Strategy Family #8 must investigate dynamic, regime-aware risk management (e.g., volatility-adjusted exposure scaling, multi-state trend anchors, or structural trail stops) while preserving a robust, volume-confirmed directional edge.
