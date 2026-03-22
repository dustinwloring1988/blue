# Experiment: experts2-deeper (mar21)

## Hypothesis
Combine N_EXPERTS=2 with DEPTH=10 to add more layers while keeping routing overhead minimal. With only 2 experts, the step reduction from depth increase should be less severe than with 6 experts.

## Results
- val_bpb: 1.476086
- peak_vram_mb: 4512.9 (~4.4 GB)
- training_seconds: 2401.4
- total_tokens_M: 97.1
- num_steps: 185
- num_params_M: 57.5
- mfu_percent: 16.93

**Baseline (N_EXPERTS=2):** val_bpb=1.300833, VRAM=3.3 GB, steps=320, tokens=167.5M, params=30.4M
**Change:** val_bpb=+0.175 (much worse), VRAM=+34%, steps=-135, tokens=-70.4M

## Expected
Partial. Depth still hurts even with fewer experts. The step reduction (320 -> 185) is too severe — fewer optimization steps dominate regardless of expert count.

## Outcome
 Worse. Confirmed: depth increases always hurt in the fixed-time regime. The fewer-steps problem is fundamental.

## Next ideas
1. Focus on throughput improvements that don't reduce steps (e.g., different attention backend, reduced MoE overhead)
2. Try N_EXPERTS=2 with warmup for better convergence within the available steps
3. Try different WINDOW_PATTERN
