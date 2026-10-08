# STRATEGY #7 OUT-OF-SAMPLE (OOS) AUTHORIZATION DOSSIER

**Document Identifier:** `OOS-AUTH-STRATEGY-07-V1.0`  
**Strategy Family:** Strategy Family #7 (`volume_displacement_continuation`)  
**Strategy Class:** `VolumeDisplacementContinuationStrategy` (`src/crypto_quant/strategies/volume_displacement_continuation.py`)  
**Strategy Slug:** `volume_displacement_continuation`  
**Protocol Specification:** `PROTOCOL-STRATEGY-07-V1.0` (Document Revision: 1.0.1)  
**Governance Status:** `OOS AUTHORIZATION DOCUMENT — PROPOSED / AWAITING HUMAN APPROVAL`  
**2026 OOS Status:** `BLIND & LOCKED — ZERO 2026 DATA ACCESSED OR LOADED`

---

## 1. Frozen Finalist Candidate Specification (`C31`)

Candidate `C31` is the sole authorized finalist surfaced from the Stage-B dual-asset calibration and pre-OOS robustness analysis:

```json
{
  "candidate_id": "C31",
  "strategy": "volume_displacement_continuation",
  "timeframe": "1h",
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

*Every parameter is strictly frozen. No further parameter adjustments, tuning, or candidate substitutions are permitted under any circumstances.*

---

## 2. Pre-Declared Out-of-Sample (OOS) Testing Window

* **OOS Start Timestamp:** `2026-01-01 00:00:00 UTC` (`1767225600000` ms)
* **OOS End Timestamp:** `2026-08-31 23:59:59 UTC` (`1788220799000` ms)
* **Asset Universe:** `BTCUSDT` and `ETHUSDT` (USDT-M Perpetual Futures)
* **Authorized Timeframe:** `1h` (4H is permanently eliminated)
* **Pre-Declaration Notice:** `OOS ENDPOINT WAS PRE-DECLARED WITHOUT INSPECTING 2026 MARKET DATA.` The end timestamp was established ex-ante as the latest complete calendar month relative to the terminal governance anchor date.

---

## 3. Standardized Execution Configuration

All OOS backtesting must strictly use the existing standardized execution engine configuration:
* **Initial Capital:** $1,000.00 per asset
* **Risk per Trade:** 1.0% of portfolio equity
* **Maximum Open Positions:** 3 concurrent positions
* **Maximum Leverage:** 5x isolated margin
* **Market Type:** Futures (USDT-M Perpetual)
* **Fee Model:** 0.04% taker fee per side (0.08% round-turn)
* **Slippage Model:** Dynamic tick slippage embedded in fill prices
* **Funding Model:** 8-hour funding rate accounting deducted per open position
* **Execution Timing:** Signal evaluated on closed bar $i$; order filled at next-bar `open[i+1]`
* **Stop-Loss / Take-Profit:** Fixed ATR stop-loss ($2.2\times\text{ATR}$) and static $2.0R$ take-profit
* **Liquidation Accounting:** Isolated margin liquidation model
* **Intrabar Collision Priority:** Conservative stop-first assumption

---

## 4. Exact Pre-Declared OOS Success Criteria (Hard Gates)

Strategy Family #7 `C31` will be considered **SUCCESSFUL** on 2026 OOS **if and only if all five hard gates are simultaneously satisfied on BOTH BTCUSDT and ETHUSDT**:

$$\text{DUAL\_ASSET\_OOS\_PASS} = \text{BTC\_OOS\_PASS} \land \text{ETH\_OOS\_PASS}$$

| Gate Criterion | BTCUSDT 1H Requirement | ETHUSDT 1H Requirement | Joint Dual-Asset Requirement |
| :--- | :--- | :--- | :--- |
| **Minimum Closed Trades ($N$)** | $N \ge 15$ | $N \ge 15$ | Mandatory on both assets |
| **Profit Factor ($PF$)** | $PF \ge 1.0500$ | $PF \ge 1.0500$ | Mandatory on both assets |
| **Expectancy ($E$)** | $E > \$0.00$ | $E > \$0.00$ | Mandatory on both assets |
| **Maximum Drawdown ($MDD$)** | $MDD \le 35.00\%$ | $MDD \le 35.00\%$ | Mandatory on both assets |
| **Liquidations ($L$)** | $L == 0$ | $L == 0$ | Zero liquidations tolerated |

* **Gate Definitions:**
  * `BTC_OOS_PASS` = all five BTC criteria simultaneously satisfied.
  * `ETH_OOS_PASS` = all five ETH criteria simultaneously satisfied.
  * `DUAL_ASSET_OOS_PASS` = `BTC_OOS_PASS AND ETH_OOS_PASS`.
* **No Partial Pass:** If either asset fails any gate, `DUAL_ASSET_OOS_PASS = False`.

---

## 5. Explicit Justification of the 35.00% MaxDD Gate

* **Governance Status:** `PRE-DECLARED OOS HARD GATE`.
* **Rationale:** The $MDD \le 35.00\%$ ceiling is established ex-ante as a tighter post-calibration robustness barrier than the Stage-B gate ($40.0\%$). It is permanently fixed before inspecting any 2026 market data or performance curves.

---

## 6. Strict Blindness & Anti-Retuning Directives

1. **Single Blind Execution:** The 2026 OOS evaluation may be executed **exactly once**. There are no second chances, trial runs, or iterative adjustments.
2. **Zero Post-OOS Retuning:** If `C31` fails any OOS hard gate on either asset, Strategy Family #7 is permanently classified as `FAILED OOS / ARCHIVED`. 2026 data may never be used to modify, recalibrate, or redesign the strategy.
3. **No Threshold or Endpoint Revisions:** Hard gates and date boundaries are locked. No post-hoc changes are permitted.
4. **No Subperiod Cherry-Picking:** The entire 8-month 2026 OOS window must be evaluated as an unbroken chronological test.
5. **No Automatic Production Authorization:** A successful OOS outcome authorizes human production review; it does NOT automatically start live trading.
6. **Current Status:** `2026 OOS REMAINS BLIND AND LOCKED — THIS DOCUMENT DOES NOT EXECUTE OOS.`
