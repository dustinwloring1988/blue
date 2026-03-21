# Experiment: increase-lr-small (mar21)

## Hypothesis
Increase MATRIX_LR from 0.08 to 0.10 — a smaller increase than the failed 0.12 attempt, hoping for faster convergence without overshooting.

## Results
- val_bpb: 1.337096
- peak_vram_mb: 3494.6 (~3.4 GB)
- training_seconds: 2404.5
- total_tokens_M: 160.4
- num_steps: 306
- num_params_M: 34.6
- mfu_percent: 8.27

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308
**Change:** val_bpb=+0.012 (worse), VRAM=-0.1%, steps=-2

## Expected
Partial. LR 0.10 is still too high — any increase over 0.08 seems to hurt.

## Outcome
Worse. The baseline LR=0.08 is already near-optimal for this architecture.

## Next ideas
1. Focus on model architecture instead — N_EXPERTS=4 is the winning direction
2. Try MATRIX_LR=0.08 with other changes (ASPECT_RATIO, depth with adjusted batch)
