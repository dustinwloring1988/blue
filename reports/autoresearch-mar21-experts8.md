# Experiment: experts-8 (mar21)

## Hypothesis
Increase MoE experts from 6 to 8 to give the model more specialized routing capacity. More experts allow finer-grained token routing, potentially improving model quality.

## Results
- val_bpb: 1.326090
- peak_vram_mb: 3520.5 (~3.4 GB)
- training_seconds: 2401.1
- total_tokens_M: 153.6
- num_steps: 293
- num_params_M: 36.7
- mfu_percent: 8.80

**Baseline:** val_bpb=1.324657, VRAM=3.4 GB, steps=308, tokens=161.5M, params=34.6M
**Change:** val_bpb=+0.001 (worse), VRAM=+0.6%, steps=-5%

## Expected
Partial. More experts should enable finer routing but the slight increase in parameters (34.6M -> 36.7M) and routing overhead reduced steps (308 -> 293) without compensating quality gains.

## Outcome
 Worse. More experts = more routing overhead = fewer steps, and no quality benefit to compensate.

## Next ideas
1. Fewer experts (N_EXPERTS=4) to reduce routing overhead and increase steps
2. Combine N_EXPERTS=4 with increased ASPECT_RATIO for more capacity without routing penalty
