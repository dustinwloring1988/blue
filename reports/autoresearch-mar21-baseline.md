# Baseline: Daily Baseline (mar21)

## Hypothesis
Establish the daily starting point by running `train.py` as-is with no modifications.

## Results
- val_bpb: 1.324657
- peak_vram_mb: 3498.2 (~3.4 GB)
- training_seconds: 2407.2 (~40 min)
- total_tokens_M: 161.5
- num_steps: 308
- num_params_M: 34.6
- depth: 8
- mfu_percent: 8.32
- train_batch_size: 16
- eval_batch_size: 8
- activation_checkpointing: disabled
- dataset: ultrafineweb

## Expected
Establish daily baseline — no hypothesis to test.

## Outcome
Baseline established. Every experiment today must beat **1.324657**.

## Next ideas
1. Try increasing learning rate (MATRIX_LR 0.08 → 0.12) — hyperparameter tuning first per exploration order
2. Try increasing depth (8 → 10) with adjusted batch size — architecture change
