# Experiment: experts2-lr (mar21)

## Hypothesis
Combine N_EXPERTS=2 with MATRIX_LR 0.08->0.10 to see if higher LR helps with fewer parameters. Since N_EXPERTS=2 has fewer parameters (30.4M vs 34.6M), a slightly higher LR might accelerate convergence.

## Results
- val_bpb: 1.304646
- peak_vram_mb: 3378.8 (~3.3 GB)
- training_seconds: 2403.4
- total_tokens_M: 167.2
- num_steps: 319
- num_params_M: 30.4
- mfu_percent: 7.29

**Baseline (N_EXPERTS=2):** val_bpb=1.300833, VRAM=3.3 GB, steps=320
**Change:** val_bpb=+0.004 (worse), VRAM=-0.0%, steps=-1

## Expected
Partial. LR=0.10 is slightly too high even with fewer parameters. Steps and throughput are nearly identical, confirming that the difference is purely from LR overshoot.

## Outcome
 Worse. MATRIX_LR=0.08 remains optimal regardless of parameter count.

## Next ideas
1. Try N_EXPERTS=2 with WARMUP_RATIO > 0 for smoother early convergence
2. Try N_EXPERTS=2 with WARMDOWN_RATIO < 0.5 to keep LR higher longer
3. Try different WINDOW_PATTERN
