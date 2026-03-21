# Experiment: increase-lr (mar21)

## Hypothesis
Increase MATRIX_LR from 0.08 to 0.12 to accelerate convergence within the fixed 40-minute time budget.

## Results
- val_bpb: 1.339816
- peak_vram_mb: 3496.3 (~3.4 GB)
- training_seconds: 2401.9
- total_tokens_M: 161.0
- num_steps: 307
- num_params_M: 34.6
- mfu_percent: 8.31

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308
**Change:** val_bpb=+0.015 (worse), VRAM=-0.1%, steps=-1

## Expected
Partial. LR 0.12 is too aggressive — the model likely overshoots optimal parameters.

## Outcome
Worse. LR was too high. The Muon optimizer is sensitive to learning rate.

## Next ideas
1. Try MATRIX_LR=0.06 instead — smaller decrease
2. Instead of changing LR, focus on model architecture (N_EXPERTS=4 was the winning direction)
