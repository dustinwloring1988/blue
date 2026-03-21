# Experiment: increase-depth (mar21)

## Hypothesis
Increase model depth from 8 to 10 to better utilize the GPU's compute capacity. With only 8.32% MFU at baseline, there's significant headroom — a deeper model processes more FLOPs per step, potentially improving convergence speed and final val_bpb within the fixed time budget.

## Results
- val_bpb: 1.485841
- peak_vram_mb: 4750.3 (~4.6 GB)
- training_seconds: 2410.9 (~40 min)
- total_tokens_M: 113.8
- num_steps: 217
- num_params_M: 70.6
- depth: 10
- mfu_percent: 13.16
- train_batch_size: 16
- eval_batch_size: 8
- activation_checkpointing: disabled

**Baseline for comparison:**
- val_bpb: 1.324657, VRAM: 3.4 GB, steps: 308, tokens: 161.5M, params: 34.6M, MFU: 8.32%

**Change: val_bpb = +0.161 (worse), VRAM = +35% (exceeds 20% budget)**

## Expected
Partial. MFU improved (8.32% -> 13.16%) confirming better GPU utilization. But val_bpb degraded significantly because fewer steps (217 vs 308) and fewer total tokens (113.8M vs 161.5M) outweighed the per-step compute gains. The fixed time budget means fewer steps = less optimization signal.

## Outcome
 Worse. The model is now deeper but has fewer optimization steps, which hurts more than the additional capacity helps. Going deeper without increasing batch size or steps is counterproductive.

## Next ideas
1. Increase MATRIX_LR from 0.08 to 0.12 to compensate for fewer steps — hyperparameter tuning for the fixed time budget
2. Try increasing ASPECT_RATIO from 32 to 48 instead (wider rather than deeper) — wider models may converge faster per step
3. Try reducing N_EXPERTS from 6 to 4 — fewer experts means less routing overhead, more throughput
