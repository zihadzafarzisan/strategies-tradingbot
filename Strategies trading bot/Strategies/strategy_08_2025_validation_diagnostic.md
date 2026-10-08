# Strategy #8 V1.3 — 2025 Validation Diagnostic

**Protocol:** PROTOCOL-STRATEGY-08-V1.3
**Protocol SHA:** `3446ea12673fc26d4c2cf5481d19e753a3be5857c35af5279626ff3cd192e08a`
**Implementation SHA:** `f02850c51b9cba7a48b15ba23bc2d9fc4ec9c7a344a7c15fa0450f4d073e3bde`
**Stage-A SHA:** `6362f611997cd631008ffa614101d1c206bcde696d87bfb3c576908858057538`  **Stage-B SHA:** `bc1451e300ee0b28d753ace383fc93b9afeda2838f2ad3ff0830c6b203f9fc4b`
**Validation window:** 2025-01-01 → <2026-01-01 UTC. **2026 OOS blind.**
**Validation gate:** `N>=15 AND PF>=1.0500 AND Exp>0 AND MaxDD<=30% AND Liq==0` (frozen Stage-B gate §9.2, reused)
**Survivors:** C34, C35, C36 (dual-asset Stage-B intersection), frozen, no tuning.

## BTC Results
| ID | N | W% | PF | EXP | GrossP | GrossL | Net | Ret% | MDD% | MDDdur(d) | Fee | Slip | Fund | Liq | PASS |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C34 | 19 | 0.211 | 0.3733 | -2.8525 | 32.29 | 86.49 | -54.20 | -5.42% | 22.20% | 352.46 | 7.28 | 984.55 | 0.84 | 0 | ✗ PF=0.3733<1.0500; EXP=-2.8525<=0 |
| C35 | 19 | 0.211 | 0.3909 | -3.2624 | 39.77 | 101.76 | -61.99 | -6.20% | 22.09% | 352.46 | 7.15 | 984.55 | 1.36 | 0 | ✗ PF=0.3909<1.0500; EXP=-3.2624<=0 |
| C36 | 19 | 0.158 | 0.3264 | -3.8822 | 35.74 | 109.51 | -73.76 | -7.38% | 21.25% | 352.46 | 6.96 | 984.55 | 1.44 | 0 | ✗ PF=0.3264<1.0500; EXP=-3.8822<=0 |

## ETH Results
| ID | N | W% | PF | EXP | GrossP | GrossL | Net | Ret% | MDD% | MDDdur(d) | Fee | Slip | Fund | Liq | PASS |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| C34 | 13 | 0.308 | 0.9729 | -0.1433 | 66.91 | 68.77 | -1.86 | -0.19% | 17.68% | 124.46 | 4.04 | 19.21 | 0.92 | 0 | ✗ N=13<15; PF=0.9729<1.0500; EXP=-0.1433<=0 |
| C35 | 13 | 0.462 | 1.6141 | 2.9118 | 99.50 | 61.64 | 37.85 | 3.79% | 15.69% | 124.46 | 3.59 | 19.21 | 1.20 | 0 | ✗ N=13<15 |
| C36 | 13 | 0.462 | 0.9543 | -0.2508 | 68.07 | 71.33 | -3.26 | -0.33% | 15.07% | 327.0 | 3.21 | 19.21 | 1.37 | 0 | ✗ N=13<15; PF=0.9543<1.0500; EXP=-0.2508<=0 |

## Pass Sets
- **BTC validation pass:** (empty)
- **ETH validation pass:** (empty)
- **DUAL-asset validation pass:** (empty)
- **Independent gate recompute mismatches:** 0

## Firewall / Downstream
- 2026 OOS accessed: NO
- OOS executed: NO
- Robustness executed: NO
- Monte Carlo executed: NO
- Paper trading executed: NO
- Live trading executed: NO
- Parameters tuned on 2025: NO