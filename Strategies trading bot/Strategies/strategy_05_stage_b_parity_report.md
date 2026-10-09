# Strategy #5 Stage-B — Project Source Parity Report

**Protocol:** PROTOCOL-STRATEGY-05-V1.0
**Actual Project Root (source of truth):** `E:\Livetrading bot\crypto_quant_terminal`
**Temporary Execution Environment:** `E:\Livetrading bot\crypto_quant_terminal\.claude\worktrees\stage05-b`

## Statement

The actual local project root is the sole source of truth. No `origin/main`, remote
branch, or committed-history state was used as authority. Files were copied **verbatim**
from the actual project root into the temporary execution environment, then verified
byte-for-byte by SHA-256.

## Parity Verification (SHA-256, worktree == actual root)

| Component | Verdict |
| :--- | :--- |
| Strategy #5 implementation (`volatility_squeeze_breakout.py`) | MATCH |
| Strategy registry (`strategies/registry.py`, `__init__.py`, `base.py`) | MATCH |
| Indicators (`indicators/atr.py`, `bollinger_bands.py`, `keltner_channel.py`, `momentum.py`, `volume_sma.py`, `__init__.py`) | MATCH |
| Metrics (`backtesting/metrics.py`) | MATCH |
| BacktestEngine (`backtesting/engine.py`, `portfolio.py`, `__init__.py`) | MATCH |
| Repository / data access (`data/repository.py`, `db/connection.py`) | MATCH |
| Execution configuration (`backtesting/execution.py`) | MATCH |
| Validation gates (`validation/optimize_window.py`) | MATCH |
| Stage-B runner (`scripts/run_stage_05_b.py`) | MATCH (before governance edit; see note) |
| SQLite database (`data/crypto_quant.db`, sha `d8ffa32d2ff37b94a8003221ffe80c15046d30a1294d65b88b6b58b0e526f681`) | MATCH |

Full recursive diff of `src/**` + `scripts/**` (`.py` and `.db`, excluding `__pycache__`):
`diff worktree.html == main.html` → **PARITY OK** (all files byte-identical).

## Governance Note on the Runner Edit

One non-result-altering governance hardening was applied to the worktree copy of
`run_stage_05_b.py`: the repository `load()` is called with
`end_ms=PRE_OOS_END_TIMESTAMP_MS (2026-01-01 00:00:00 UTC)`, so **2026 candles are never
fetched into memory** — the 2026 exclusion is enforced at the query layer rather than only
by post-hoc slicing. This changes no parameter, gate, split, or metric; it only strengthens
the auditable guarantee that zero 2026 data is accessed.

Pre-flight confirmed 0 rows at/after the 2026 boundary for all four tracks when loaded with
this bound.

## Verified Before Execution

- 48-combination grid: product(kc_mult=3, bb_std=2, volume_mult=2, atr_multiplier=2, rr=2)=48 ✓
- Baseline default (`atr_multiplier=2.0`) is by design outside the Stage-B grid `[1.8, 2.2]`; this is a protocol property, not a runner defect.
- Train/legal splits: BTC 2020–2024 / ETH 2022–2024; validation 2025 both ✓
- All five validation hard gates encoded in `ScoreMultiObjectiveFilter` ✓
- No 2026 rows accessible under the `end_ms` bound ✓

## Status

`STAGE-B READY TO EXECUTE FROM ACTUAL PROJECT SOURCE`