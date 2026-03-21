# Experiment: experts-10 (mar21)

## Hypothesis
Increase MoE experts from 6 to 10 to further explore whether more routing capacity improves val_bpb. Following the trend from experts-8 (which was slightly worse), going even more extreme.

## Results
- val_bpb: 1.356199
- peak_vram_mb: 3555.8 (~3.5 GB)
- training_seconds: 2404.5
- total_tokens_M: 147.3
- num_steps: 281
- num_params_M: 38.8
- mfu_percent: 9.26

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308, tokens=161.5M, params=34.6M
**Change:** val_bpb=+0.032 (worse), VRAM=+1.6%, steps=-9%

## Expected
Yes (confirmed worse). Clear trend: more experts = more routing overhead = fewer steps = worse val_bpb.

## Outcome
Worse. Clear confirmation that more experts hurts on this dataset/time budget. Routing overhead dominates.

## Next ideas
1. Fewer experts (N_EXPERTS=4) — opposite direction, reduce overhead
2. Combine N_EXPERTS=4 with wider model (ASPECT_RATIO 32->40) for capacity without routing penalty
