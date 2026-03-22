# Experiment: experts2-wd (mar21)

## Hypothesis
Combine N_EXPERTS=2 with WEIGHT_DECAY 0.2->0.1 to reduce regularization. With fewer parameters (30.4M), less regularization might help the model fit the data better.

## Results
- val_bpb: 1.360654
- peak_vram_mb: 3378.8 (~3.3 GB)
- training_seconds: 2400.1
- total_tokens_M: 173.0
- num_steps: 330
- num_params_M: 30.4
- mfu_percent: 6.97

**Baseline (N_EXPERTS=2):** val_bpb=1.300833, VRAM=3.3 GB, steps=320
**Change:** val_bpb=+0.060 (worse), VRAM=-0.0%, steps=+10

## Expected
Partial. Surprisingly worse despite more steps. The baseline WD=0.2 appears well-tuned — less regularization hurts more than it helps, likely causing overfitting on this small dataset.

## Outcome
 Worse. Weight decay=0.2 is already optimal. Less regularization leads to worse generalization.

## Next ideas
1. Try N_EXPERTS=2 with warmup (WARMUP_RATIO > 0)
2. Try different WINDOW_PATTERN
3. The current N_EXPERTS=2 config appears well-optimized — incremental gains may be small
