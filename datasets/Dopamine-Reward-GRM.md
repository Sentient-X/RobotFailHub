# Dopamine-Reward / GRM (Robo-Dopamine)

| Field | Value |
| --- | --- |
| **Date** | 2025-12 |
| **Paper** | [Robo-Dopamine: General Process Reward Modeling for High-Precision Robotic Manipulation](https://arxiv.org/abs/2512.23703) |
| **Domain** | Robot+Human / Sim+Real |
| **Modality** | multi-view image, language, BEFORE/AFTER pairs |
| **Size** | **34,601,209 samples** (`json_all`); 3,400+ h / 100k+ trajectories / 350 tasks; HF images ~239 GB + JSON ~6.1 GB |
| **Progress Annotation** | Yes — hop-based relative progress (BEFORE/AFTER) |
| **Failure or Recovery Trajectory** | Yes — mix of real / simulated / human video |
| **Subtask Annotation** | Yes — step-wise discretization |
| **Failure Taxonomy** | No (hop-based relative progress, no separate failure taxonomy) |

## Description

Large-scale relative-progress (GRM) training data that learns task progress from BEFORE/AFTER image pairs and language descriptions. Suitable for generalist reward models, progress critics and long-horizon manipulation.

## Download

- Hugging Face (**gated**, access must be requested): https://huggingface.co/datasets/tanhuajie2001/Robo-Dopamine-GRM-Dataset

## Notes

- Before downloading, accept the license and request access on the Hugging Face page.
- The dataset is very large; download shards as needed, or fetch only the JSON metadata for indexing.
- Local mirror: `hf download tanhuajie2001/Robo-Dopamine-GRM-Dataset --repo-type dataset --local-dir .../Dopamine-GRM`
