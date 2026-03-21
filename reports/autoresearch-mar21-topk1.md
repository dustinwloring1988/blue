# Experiment: topk1 (mar21)

## Hypothesis
Change TOP_K from 2 to 1 (top-1 routing) based on the comment in train.py stating "top-1 beats top-2 and top-3". Top-1 is simpler and has no weight normalization overhead.

## Results
- val_bpb: 1.333168
- peak_vram_mb: 3297.0 (~3.2 GB)
- training_seconds: 2403.7
- total_tokens_M: 163.6
- num_steps: 312
- num_params_M: 34.6
- mfu_percent: 8.44

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308
**Change:** val_bpb=+0.009 (worse), VRAM=-5.8%, steps=+4

## Expected
Partial. VRAM dropped significantly (3.4 GB -> 3.2 GB) confirming less memory from top-1. But val_bpb is worse.

## Outcome
Worse. Top-2 outperforms top-1 on this dataset. The comment in the code was wrong for this configuration.

## Next ideas
1. Stick with TOP_K=2 and focus on other changes
2. Try TOP_K=2 with N_EXPERTS=4 (best of both worlds)
