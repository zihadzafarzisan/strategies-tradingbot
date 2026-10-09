# Strategy #8 (`adaptive_displacement_trailing`) — V1.3 2025 Validation Post-Mortem

**Strategy Class:** `AdaptiveDisplacementTrailingStrategy`  
**Strategy Slug:** `adaptive_displacement_trailing`  
**Protocol Identifier:** `PROTOCOL-STRATEGY-08-V1.3`  
**Stage Reached:** 2025 Validation (frozen Stage-B survivors evaluated forward)  
**Validation Outcome:** `STRATEGY_08_V1_3_VALIDATION_FAILED`  
**Final Governance Status:** `STRATEGY_08_V1_3_VALIDATION_FAILED_AND_ARCHIVED`

---

## 1. Strategy identity
- Strategy: Adaptive Displacement & Structural Trailing (`adaptive_displacement_trailing`)
- Implements body/volume-qualified Fair Value Gap (FVG) displacement entry, Kaufman Efficiency-Ratio regime filter, breakeven + ATR trailing stop, take-profit at 2.0R.

## 2. Protocol identity and SHA
- `data/protocol_strategy_08.md` — `PROTOCOL-STRATEGY-08-V1.3` (APPROVED AND FROZEN)
- SHA-256: `3446ea12673fc26d4c2cf5481d19e753a3be5857c35af5279626ff3cd192e08a` — **20,507 bytes** (verified)

## 3. V1.2 archive identity and SHA
- `data/protocol_strategy_08_v1_2_frozen.md` — immutable historical archive
- SHA-256: `5bf062e15aa8a91d7d521dd678fa5015d0ea43a6686e4ba995914a0e93688457` — **11,807 bytes** (verified)
- V1.2 is superseded and permanently archived; its Stage-A survivors were never promoted to V1.3.

## 4. Implementation identity and SHA
- `src/crypto_quant/strategies/adaptive_displacement_trailing.py`
- **Verified on-disk SHA-256 (64-char): `f02850c51b9cba7a48b15ba23bc2d9fc4ec9c7a344a7c15fa0450f4d073e3bde`** — 16,922 bytes.
- Governance note: one authorization message pinned a malformed 67-character value (`f02850c51b9cba7a48b18b15ba23bc2d9fc4ec9c7a344a7c15fa0450f4d073e3bde`, an extra `8b1`). This is not a valid SHA-256 and does not match the file. The on-disk hash above, corroborated by `strategy_08_implementation_audit.md` and `strategy_08_v1_3_final_implementation_readiness.md`, is the authoritative canonical. The implementation was verified unchanged and was not modified.

## 5. Stage-A provenance
- `data/strategy_08_stage_a_screening.json` — SHA-256 `6362f611997cd631008ffa614101d1c206bcde696d87bfb3c576908858057538` — 71,343 bytes (verified)
- Fresh V1.3 Stage-A: 37 candidates (C00–C36) screened on both assets; exact intersection C00–C36.

## 6. Stage-B provenance
- `data/strategy_08_stage_b_results.json` — SHA-256 `bc1451e300ee0b28d753ace383fc93b9afeda2838f2ad3ff0830c6b203f9fc4b` — 73,683 bytes (verified)
- 37 × 2 backtests; BTC pass {C34,C35,C36}, ETH pass {C07–C09,C16–C18,C21,C25–C27,C34,C35,C36}; exact dual-asset intersection {C34, C35, C36}.
- Stage-B forensic audit = `S8_V1_3_STAGE_B_FORENSIC_PASS`; Stage-A artifact identity = `S8_V1_3_STAGE_A_ARTIFACT_IDENTITY_RECONCILED`.

## 7. Validation provenance
- `data/strategy_08_2025_validation.json` — SHA-256 `a1b1e23f915477e7da561ba4622ba4f0a51dd52b05971cc5ddabf78dd9e98c6d` — 11,008 bytes (verified)
- `data/strategy_08_2025_validation_diagnostic.md` — SHA-256 `d5bd6eafcc97409884a17a5348119d50528fe2dc108758e5f91f27210827bb6f` — 2,447 bytes (verified)
- Validation forensic audit = `S8_V1_3_2025_VALIDATION_FORENSIC_PASS`.

## 8. Frozen survivor configurations (ONLY candidates entering Validation)
| ID | body_mult | volume_mult | er_threshold | atr_multiplier |
| :--- | :---: | :---: | :---: | :---: |
| C34 | 1.70 | 1.80 | 0.45 | 1.80 |
| C35 | 1.70 | 1.80 | 0.45 | 2.20 |
| C36 | 1.70 | 1.80 | 0.45 | 2.50 |

Frozen protocol constants: `body_period = 20`, `volume_period = 20` (not grid dimensions). No candidate added, removed, or substituted; no retuning.

## 9. 2025 data window
- `2025-01-01 00:00:00 UTC` through `2025-12-31 23:59:59 UTC` (exclusive upper bound `2026-01-01 00:00:00 UTC`).
- BTCUSDT 8,760 hourly rows; ETHUSDT 8,760 hourly rows; maximum bar `2025-12-31 23:00 UTC`.
- 2026 was never accessed (OOS blinds kept).

## 10. Validation gate (frozen, reused from protocol §9.2; protocol defines no separate numeric Validation gate)
`N >= 15` AND `PF >= 1.0500` AND `Expectancy > 0` AND `MaxDD <= 30.00%` AND `Liquidations == 0` — applied identically on both assets.

## 11. BTC results (2025)
| ID | N | Win% | PF | Exp | Net P&L | Ret% | MaxDD% | MDDdur | Fee | Slippage* | Fund | Liq | Gate |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| C34 | 19 | 21.1% | 0.373 | −2.85 | −54.20 | −5.42% | 22.20% | 352d | 7.28 | 984.55 | 0.84 | 0 | FAIL |
| C35 | 19 | 21.1% | 0.391 | −3.26 | −61.99 | −6.20% | 22.09% | 352d | 7.15 | 984.55 | 1.36 | 0 | FAIL |
| C36 | 19 | 15.8% | 0.326 | −3.88 | −73.76 | −7.38% | 21.25% | 352d | 6.96 | 984.55 | 1.44 | 0 | FAIL |

*Slippage column = accumulated absolute **price displacement** (reporting limitation — see §14); not dollar cost and not used in any gate. BTC has **zero** passing candidates.

## 12. ETH results (2025)
| ID | N | Win% | PF | Exp | Net P&L | Ret% | MaxDD% | MDDdur | Fee | Slippage* | Fund | Liq | Gate |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| C34 | 13 | 30.8% | 0.973 | −0.14 | −1.86 | −0.19% | 17.68% | 124d | 4.04 | 19.21 | 0.92 | 0 | FAIL |
| C35 | 13 | 46.2% | 1.614 | +2.91 | +37.85 | +3.79% | 15.69% | 124d | 3.59 | 19.21 | 1.20 | 0 | FAIL |
| C36 | 13 | 46.2% | 0.954 | −0.25 | −3.26 | −0.33% | 15.07% | 327d | 3.21 | 19.21 | 1.37 | 0 | FAIL |

ETH has **zero** passing candidates: C35 is profitable (PF 1.614, Exp +2.91) but **N=13 < 15** fails the minimum-N hard gate; C34 and C36 fail profitability/expectancy.

## 13. Dual-asset result
- `BTC pass ∩ ETH pass = ∅`. **Dual-asset survivors = NONE.** All hard gates applied unchanged; no gate loosened; positive profitability did not override a failed hard gate.

## 14. Slippage reporting caveat
- The engine **correctly applies** 0.05% adverse slippage per execution (`entry_fill = open × (1 ± 0.0005)`); P&L is computed on the real widened fill.
- The aggregate reported `slippage_impact` field accumulates absolute **price displacement** (`raw_fill × 0.0005`), **not** dollar trading cost (true cost = displacement × quantity). It overstates magnitude and is identical across the three survivors per asset because entry signals/fills are identical (candidates differ only in `atr_multiplier`).
- Execution slippage = correct; P&L treatment = correct; no double-counting = confirmed; PF / expectancy / net P&L / gates = **unaffected**.
- This is a **known reporting limitation** (metric presentation), recorded for a future controlled reporting-quality task. The engine was **not** modified. The Validation failure is **not** a slippage artifact.

## 15. Data-firewall confirmation
- Only 2025 queried; 2026/OOS never accessed; no out-of-sample result influenced Validation.

## 16. Governance violations check
- No gate altered; no candidate substituted; no retuning; no 2026 access; no OOS/robustness/Monte Carlo/paper/live execution; no engine or production-code modification; no protocol modification. **None found.**

## 17. Research interpretation (facts vs. hypotheses)
**Verified facts:**
- All three BTC candidates failed badly in 2025 (PF 0.33–0.39, negative expectancy).
- ETH C34 and C36 were negative; ETH C35 was profitable but N=13 < 15.
- No candidate passed both assets; dual-asset survivors = none.
- All hard gates applied unchanged; execution-side slippage correct; no retuning, no substitution, no 2026 access.
- Validation failure is **genuine** under the frozen protocol and forensic audit passed.

**Hypotheses only (not asserted as established causation):** possible contributors — e.g., the survivor configurations sit at the most selective grid corner (body_mult 1.70, volume_mult 1.80, ER 0.45) producing low annual signal counts; 2025 market conditions may not have favored this entry/regime profile. **No causal mechanism is claimed as proven.** Low-N outcomes on a single validation year carry substantial sampling variance.

## 18. Final disposition
`STRATEGY_08_V1_3_VALIDATION_FAILED_AND_ARCHIVED`. The strategy is archived as a fully-documented failed validation experiment. No replacement protocol is designed here.

## 19. 2026/OOS remains blind
2026 data was **not** accessed and remains completely blind/locked.

## 20. No downstream stage executed
OOS, robustness, Monte Carlo, paper trading, and live trading were **NOT** executed and are **NOT** authorized. Pipeline stopped at the human authorization gate.