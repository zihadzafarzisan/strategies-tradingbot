# Strategy Family #7 (`volume_displacement_continuation`) Implementation & Causality Audit Report

**Protocol:** `PROTOCOL-STRATEGY-07-V1.0` (Document Revision: 1.0.1)  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Audit Date:** 2026-09-12  
**Audit Verdict:** `VERIFIED — STRICT CAUSALITY CONFIRMED`

---

## 1. Line-by-Line Implementation Verification

### 1.1 Volatility & Volume Indicators
* `atr_14 = calc_atr(high, low, close, period=14, shift=1)`: Computes Wilder ATR shifted by 1 bar. At bar $i$, sees ATR up to bar $i-1$. **Causal.**
* `vol_sma = calc_volume_sma(volume, period=20, shift=1)`: Computes 20-period simple moving average of volume shifted by 1 bar. At bar $i$, sees volume SMA up to bar $i-1$. **Causal.**
* `ema_50 = calc_ema(close, period=50, shift=1)`: Computes 50-period exponential moving average of close shifted by 1 bar. At bar $i$, sees EMA up to bar $i-1$. **Causal.**

### 1.2 Displacement Candle Identification
* `body_size = (close.shift(1) - open.shift(1)).abs()`: Evaluates the real body of the closed candle $i-1$.
* `is_large_body = body_size >= (body_mult * atr_14)`: Compares closed candle body to ATR up to $i-1$.
* `is_volume_surge = volume.shift(1) >= (volume_mult * vol_sma)`: Compares closed candle volume to volume SMA up to $i-1$.

### 1.3 3-Bar Imbalance (Fair Value Gap) Definition
* **Bullish FVG:** `(close.shift(1) > open.shift(1)) & (low.shift(1) > high.shift(3))`
  * Tests that the low of closed bar $i-1$ is strictly higher than the high of closed bar $i-3$, creating an unmitigated 3-bar imbalance window.
  * Verified strictly point-in-time: Uses `shift(1)` and `shift(3)`. Zero current or future bar data is accessed.
* **Bearish FVG:** `(close.shift(1) < open.shift(1)) & (high.shift(1) < low.shift(3))`
  * Tests that the high of closed bar $i-1$ is strictly lower than the low of closed bar $i-3$.
  * Verified strictly point-in-time.

### 1.4 Trend Alignment & Mitigation Setup
* `recent_bull_disp = bullish_disp.rolling(disp_lookback, min_periods=1).max() == 1`: Evaluates whether a confirmed displacement occurred within the preceding `disp_lookback` closed bars.
* `bullish_retest = recent_bull_disp & (close.shift(1) > ema_50)`: Validates ongoing trend alignment above $\text{EMA}_{50}$.
* `_long_setup` / `_short_setup`: Stored in DataFrame at bar $i$, reflecting only information available at the close of bar $i-1$.

### 1.5 Entry Signal & Order Execution
* `entry_signal(df, i)`: Checks `bool(df["_long_setup"].iloc[i])` or `bool(df["_short_setup"].iloc[i])`.
* BacktestEngine signal timing: Evaluated at bar $i$; pending order fills at `open[i+1]`.
* Stop-Loss & Take-Profit: Computed based on `atr_multiplier` and `risk_reward_ratio` from point-in-time ATR at fill.

---

## 2. Causality & Anti-Lookahead Verification

1. **Perturbation Test:** Mutating future bars $i+1 \dots N$ does not change `_long_setup[i]`, `_short_setup[i]`, or `entry_signal(i)`. Verified by `tests/test_strategy_07.py::test_causality_and_no_lookahead` (**PASSED**).
2. **Execution Timing:** All entries occur at next-bar `open[i+1]` following signal generation at bar $i$ close.
3. **No Intrabar Omniscience:** Stops and targets are fixed at fill; conservative stop-first collision assumption applied during same-bar high/low touches.

---

## 3. Implementation Audit Conclusion
`VolumeDisplacementContinuationStrategy` is mathematically sound, fully vectorized, strictly causal, and free of look-ahead bias.
