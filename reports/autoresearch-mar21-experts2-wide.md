# Experiment: experts2-wide (mar21)

## Hypothesis
Combine N_EXPERTS=2 with ASPECT_RATIO 32->34 to increase model width while keeping routing overhead minimal. The freed VRAM from fewer experts should allow a wider model without exceeding the VRAM budget.

## Results
- val_bpb: 1.412321
- peak_vram_mb: 4058.0 (~4.0 GB)
- training_seconds: 2403.6
- total_tokens_M: 114.7
- num_steps: 219
- num_params_M: 42.5
- mfu_percent: 12.79

**Baseline (N_EXPERTS=2):** val_bpb=1.300833, VRAM=3.3 GB, steps=320, tokens=167.5M, params=30.4M
**Change:** val_bpb=+0.111 (much worse), VRAM=+20%, steps=-101, tokens=-52.8M

## Expected
Partial. Width increase boosted MFU (7.28% -> 12.79%) but the dramatic step reduction (320 -> 219) overwhelmed any per-step quality gains. More FLOPs per step is not helpful when total optimization steps drop significantly.

## Outcome
 Worse. Model width changes hurt because they reduce steps in the fixed time budget. The lesson: within the fixed-time regime, throughput (steps/token throughput) matters more than per-step FLOPs.

## Next ideas
1. Stick with N_EXPERTS=2 — it's the sweet spot for this time budget
2. Try N_EXPERTS=2 with warmup (WARMUP_RATIO 0.0 -> 0.02) for smoother convergence
3. Try different window pattern (WINDOW_PATTERN tuning)
