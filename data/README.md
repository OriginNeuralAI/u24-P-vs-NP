# Data Dictionary

All data files are JSON format, produced by the Isomorphic Engine v0.15.0 with fixed seeds for reproducibility.

## P vs NP (`data/p-vs-np/`)

| File | Description | Key Fields |
|------|-------------|------------|
| `barrier_scaling.json` | Barrier heights n=10–100 | `results[].mean_barrier`, `fit_mean.alpha` |
| `rsb_ogp_sweep.json` | OGP + RSB at n=100–10,000 (GPU) | `ogp_results[].forbidden_mass`, `q_ea_convergence` |
| `stability_comparison.json` | 15 solvers, stable vs unstable | `stable_mean_energy`, `unstable_mean_energy`, `energy_gap` |
| `minima_count.json` | Basin counts n=10–50,000 | `[(n, avg_minima, avg_E0)]` |
| `basin_structure.json` | g_macro cycle structure | `g_macro_cycle_type`, `omega_product`, `reeds_match_l2` |
| `reeds_analysis.json` | Reeds endomorphism Ω=24 | `cycle_type`, `order`, `omega_product` |
| `gue_analysis.json` | GUE at local minima | `mean_ks_distance`, `mean_p_value` |
| `rigidity_sweep.json` | U₂₄ rigidity at n=50–500 | `mean_omega`, `fraction_omega_24` |
| `rsb_analysis.json` | RSB at n=10,000 | `q_ea`, `mean_overlap`, `overlap_variance` |
| `verification_summary.json` | All automated checks | `total_checks`, `passed_checks`, `checks[]` |

## BSD (`data/bsd/`)

| File | Description | Key Fields |
|------|-------------|------------|
| `bsd_verification.json` | H_D^E verification for 4 curves | `checks[]`, `curve_results[]` |

## Verification Summary (`data/verification-summary/`)

Consolidated cross-paper verification data.

## Reproducibility

All results are deterministic with seed=42. To reproduce:

```bash
cd engine/p_vs_np_engine
cargo run --release -- verify-all --seed 42
cargo run --release -- rsb-sweep --sizes 100,500,1000,5000,10000 --seed 42
cargo run --release -- stability-compare --sizes 20,50,100 --seed 42
```
