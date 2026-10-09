# Strategy Family #5 (`volatility_squeeze_breakout`) Final Post-Mortem

**Strategy Class:** `VolatilitySqueezeBreakoutStrategy` (`src/crypto_quant/strategies/volatility_squeeze_breakout.py`)  
**Strategy Slug:** `volatility_squeeze_breakout`  
**Protocol:** `PROTOCOL-STRATEGY-05-V1.0`  
**Final Governance Status:** `PERMANENTLY REJECTED AND ARCHIVED`  
**2026 OOS Status:** `NEVER ACCESSED / NEVER AUTHORIZED`  

---

## 1. Research Hypothesis & Quantitative Thesis
Strategy Family #5 hypothesized that extended periods of low volatility (Bollinger Bands contracting inside Keltner Channels) represent institutional absorption/coiling, and that directional expansions out of these squeezes—confirmed by momentum and volume surges—would capture asymmetric directional trend moves in crypto perpetual futures.

---

## 2. Stage-A Baseline Screening Summary
The frozen baseline parameter set evaluated across 2020/2022–2025:
* **BTCUSDT 4H:** $N = 485, PF = 0.7315, \text{Exp} = -\$1.28, MDD = 72.86\% \rightarrow$ PASS (non-catastrophic gate)
* **ETHUSDT 4H:** $N = 294, PF = 1.0603, \text{Exp} = +\$0.43, MDD = 42.95\% \rightarrow$ PASS
* **BTCUSDT 1H:** $N = 1,810, PF = 0.9419, \text{Exp} = -\$0.26, MDD = 78.45\% \rightarrow$ PASS ($PF \ge 0.75$, non-catastrophic)
* **ETHUSDT 1H:** $N = 1,193, PF = 0.8776, \text{Exp} = -\$0.49, MDD = 69.82\% \rightarrow$ PASS

Stage-A baseline screening passed non-catastrophic survival criteria, unlocking bounded Stage-B calibration for 4H and 1H.

---

## 3. Stage-B Calibration Search Space
A pre-declared, bounded 48-combination grid was tested across 4 tracks $\times$ 2 slices (384 total backtest runs):
* `kc_mult`: `[1.2, 1.5, 1.8]` (3)
* `bb_std`: `[1.8, 2.0]` (2)
* `volume_mult`: `[1.0, 1.2]` (2)
* `atr_multiplier`: `[1.8, 2.2]` (2)
* `risk_reward_ratio`: `[2.0, 2.5]` (2)

---

## 4. Dual-Asset Intersection Results (Exact Parameter Match)

Under `PROTOCOL-STRATEGY-05-V1.0`, dual-asset qualification requires:
$$\text{DUAL\_ASSET\_CANDIDATES} = \text{BTC\_PASSING\_IDS} \cap \text{ETH\_PASSING\_IDS} \neq \emptyset$$

### 4.1 4H Timeframe
* **BTC 4H Passing IDs ($N=0$):** `[]` (0/48 passed)
* **ETH 4H Passing IDs ($N=30$):** `['C17', 'C19', 'C20', 'C21', 'C22', 'C23', 'C24', 'C25', 'C26', 'C27', 'C28', 'C29', 'C30', 'C31', 'C32', 'C33', 'C34', 'C35', 'C36', 'C37', 'C38', 'C39', 'C40', 'C42', 'C43', 'C44', 'C45', 'C46', 'C47', 'C48']`
* **Shared Passing IDs:** `[]` ($\text{Count} = 0$)
* **Timeframe Decision:** `FAILED_DUAL_ASSET_VALIDATION`

### 4.2 1H Timeframe
* **BTC 1H Passing IDs ($N=9$):** `['C04', 'C08', 'C09', 'C12', 'C13', 'C16', 'C24', 'C28', 'C32']`
* **ETH 1H Passing IDs ($N=1$):** `['C11']`
* **Shared Passing IDs:** `[]` ($\text{Count} = 0$)
* **Timeframe Decision:** `FAILED_DUAL_ASSET_VALIDATION`

---

## 5. Failure Analysis

### 5.1 Why 4H Failed
On BTC 4H, volatility squeezes frequently resolved into false breakout sweeps before reversing into choppy consolidations. All 48 parameter variations failed to achieve $PF \ge 1.0500$ in 2025 (maximum achieved was $PF = 0.8057$). Despite strong performance on ETH 4H (30 passing candidates), BTC 4H was completely unviable.

### 5.2 Why 1H Failed
On 1H, BTC favored tighter channels with wider targets (`C04`, `C08`, `C09`, `C12`, `C13`, `C16`, `C24`, `C28`, `C32`), while ETH was heavily penalized by transaction fees and chop on 1H, with only a single candidate (`C11`) passing validation. Crucially, `C11` failed BTC 1H ($PF = 1.0082 < 1.0500$). The mathematical intersection between BTC 1H and ETH 1H was strictly empty.

### 5.3 Candidate C11 Single-Asset Analysis & Advancement Prohibition
* **C11 Parameters:** `kc_mult=1.2, bb_std=2.0, volume_mult=1.0, atr_multiplier=2.2, risk_reward_ratio=2.0`
* **ETH 1H Validation:** $N = 171, PF = 1.1229, \text{Exp} = +\$0.71, MDD = 36.4\% \rightarrow$ **PASS**
* **BTC 1H Validation:** $N = 167, PF = 1.0082, \text{Exp} = +\$0.03, MDD = 38.4\% \rightarrow$ **FAIL** ($PF < 1.0500$)
* **Governance Barrier:** Single-asset survival does not satisfy the dual-asset portfolio requirement. Creating an ad-hoc asset-specific exemption violates cross-asset universality principles and invites selection bias. `C11` remains archived as a single-asset diagnostic.

---

## 6. Selection-Bias & Multiple-Testing Limitations
Evaluating 48 parameter configurations across 4 tracks represents 192 candidate-track tests. The emergence of `C11` as the sole surviving ETH 1H candidate carries high probability of in-sample sample-path variance. Without cross-validation on BTC, advancing `C11` would constitute curve-fitting to 2025 ETH market microstructure.

---

## 7. Execution and Infrastructure Integrity
* All backtests used standardized futures execution accounting ($0.04\%$ taker fee per side, dynamic slippage, 8-hour funding rates, conservative stop-first bar collision).
* Zero look-ahead: All indicators computed with point-in-time causal shifting; order fills at $t+1$ open.
* Zero 2026 leakage: Verified query-level boundary `end_ms = 1767225600000` (2026-01-01 00:00:00 UTC).

---

## 8. Final Governance Conclusion
`VolatilitySqueezeBreakoutStrategy` failed to produce any shared parameter configuration satisfying the pre-declared Stage-B validation criteria across BTC and ETH on either candidate timeframe.

**DECISION:**  
`VolatilitySqueezeBreakoutStrategy IS PERMANENTLY REJECTED AND CLOSED FOR THE DUAL-ASSET RESEARCH PROGRAM.`  
* **OOS Authorization:** STRICTLY FORBIDDEN (No 2026 evaluation).
* **Anti-Retuning Rule:** No further parameter searches or structural revisions of Strategy Family #5 are permitted.
