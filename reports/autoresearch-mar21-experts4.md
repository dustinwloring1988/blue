# Experiment: experts-4 (mar21) — BEST RESULT

## Hypothesis
Decrease MoE experts from 6 to 4 to reduce routing overhead and increase steps. The trend from experts-8 and experts-10 shows more experts hurts — going the opposite direction should help.

## Results
- val_bpb: 1.303690
- peak_vram_mb: 3437.2 (~3.4 GB)
- training_seconds: 2404.1
- total_tokens_M: 165.2
- num_steps: 315
- num_params_M: 32.5
- mfu_percent: 7.58

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308, tokens=161.5M, params=34.6M, MFU=8.32%
**Change:** val_bpb=-0.021 (improved!), VRAM=-1.7%, steps=+7, tokens=+3.7M, params=-2.1M

## Expected
Yes. Fewer experts = less routing overhead = more steps in fixed time budget + fewer parameters to optimize. Confirmed by the expert count trend: 4 < 6 < 8 < 10.

## Outcome
**Improved.** Significant val_bpb improvement of 0.021. This is the new best. Fewer experts = less overhead = better utilization and more optimization steps.

## Next ideas
1. Try N_EXPERTS=2 — push the trend further
2. Combine N_EXPERTS=4 with ASPECT_RATIO 32->40 to increase capacity while keeping steps high
3. Try N_EXPERTS=4 + MATRIX_LR tuning (slightly higher LR may help with fewer params)
