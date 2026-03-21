# Experiment: experts-2 (mar21) — NEW BEST

## Hypothesis
Decrease MoE experts from 6 to 2 to continue the trend from N_EXPERTS=4 (which was better than baseline). Fewer experts = less routing overhead = more steps in the fixed time budget.

## Results
- val_bpb: 1.300833
- peak_vram_mb: 3378.8 (~3.3 GB)
- training_seconds: 2401.4
- total_tokens_M: 167.5
- num_steps: 320
- num_params_M: 30.4
- mfu_percent: 7.28

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308, tokens=161.5M, params=34.6M
**Change:** val_bpb=-0.024 (improved!), VRAM=-3.4%, steps=+12, tokens=+6.0M, params=-4.2M

## Expected
Yes. Confirmed the trend: fewer experts = better val_bpb. The improvement from N_EXPERTS=4 (1.303690) to N_EXPERTS=2 (1.300833) shows diminishing returns but still positive.

## Outcome
**Improved.** New best result. Clear trend: 2 < 4 < 6 < 8 < 10 experts. The sweet spot is at N_EXPERTS=2.

## Next ideas
1. Try N_EXPERTS=2 with wider model (ASPECT_RATIO 32->36) to increase capacity while keeping routing overhead minimal
2. Try N_EXPERTS=2 with MATRIX_LR 0.08->0.10 to see if LR helps with fewer parameters
3. Try dense model (N_EXPERTS=0) — even fewer params, more steps
