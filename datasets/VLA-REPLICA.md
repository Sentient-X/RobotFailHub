# VLA-REPLICA

| Field | Value |
| --- | --- |
| **Date** | 2026-05 |
| **Paper** | [VLA-REPLICA: A Low-Cost, Reproducible Benchmark for Real-World Evaluation of Vision-Language-Action Models](https://arxiv.org/abs/2605.20774) |
| **Domain** | Robot / Real |
| **Dataset Role** | benchmark-aligned demonstration + reference scene |
| **R2 Classification** | R2-B — real-robot benchmark; test rollouts must be generated on SO-101 hardware |
| **Modality** | top/wrist RGB, LeRobot-compatible state/action, language, reference scene images |
| **Size** | 10 tasks; 50 demonstrations per task (500 in total); 90 ID/OOD test-scene references; HF files about 1.97 GB |
| **Progress Annotation** | No; uses task-specific binary success conditions |
| **Failure or Recovery Trajectory** | No public unified test rollout dump; the evaluation script asks the operator to record success/failure behavior |
| **Subtask Annotation** | No unified subtask annotation |
| **Failure Taxonomy** | No |
| **License** | Data CC BY 4.0; code MIT |

## Description

VLA-REPLICA is a low-cost, reproducible real-robot VLA benchmark based on the SO-101 with a fixed workspace and top and wrist cameras. The official release provides 10 manipulation tasks, 500 adaptation demonstrations and 90 test-scene reference images, for reproducing ID/OOD real-robot evaluation across labs.

The 22 rows shown by the Hugging Face viewer are display units from automatic conversion, not the total number of robot episodes; the demonstration total should be taken from the project page: "50 per task, 500 in total".

## Evaluation Protocol

- Each task variant is run 5 times.
- Each run lasts at most 90 seconds.
- ID: 10 tasks × 5 variants, 50 runs in total.
- OOD: 8 tasks × 5 variants, 40 runs in total.
- Success conditions are defined per task; for example, stacking requires stable contact for more than 2 seconds, and the oven door must stay open for more than 2 seconds.

## Official Sources

- Project: https://irvlutd.github.io/VLAReplica/
- Dataset: https://huggingface.co/datasets/HenryZhang/VLAReplica_SFT_data
- Code and reference scenes: https://github.com/IRVLUTD/VLAReplica
- Paper: https://arxiv.org/abs/2605.20774

## Download

```bash
hf download HenryZhang/VLAReplica_SFT_data \
  --repo-type dataset \
  --local-dir ../datasets/VLA-REPLICA/SFT-data
```

## Notes

- The public download is training/adaptation demonstrations and scene references, not a collection of candidate-policy test rollouts.
- Best used to set up a repeatable local real-robot evaluation and actively collect new failure/takeover data.
