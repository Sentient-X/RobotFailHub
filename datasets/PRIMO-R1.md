# PRIMO-R1

| Field | Value |
| --- | --- |
| **Date** | 2026-03 |
| **Paper** | [From Passive Observer to Active Critic: RL Elicits Process Reasoning for Robotic Manipulation](https://arxiv.org/abs/2603.15600) |
| **Domain** | Robot / Real + Sim |
| **Modality** | video, initial/current frame, language, CoT progress (1–100) |
| **Size** | Bench 23.7k; SFT 116.8k; RL 328.5k (row counts listed on HF) |
| **Progress Annotation** | Yes — fine-grained numeric progress + CoT |
| **Failure or Recovery Trajectory** | Yes — includes failure detection and OOD real-humanoid scenes |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No (RoboFail is a separate benchmark) |

## Description

PRIMO R1 (Process Reasoning Induced Monitoring) trains a video MLLM as an active critic, using outcome-based RL to elicit CoT progress estimation. The data covers AgiBot real environments, BEHAVIOR-1k and RoboTwin simulation, plus a **real-humanoid-ood** evaluation subset (4791 rows, the closest to real humanoid deployment scenarios).

## Download

- HF Collection: https://huggingface.co/collections/LeonOverload/primo-r1
- Model: https://huggingface.co/LeonOverload/PRIMO-R1-7B
- Benchmark JSON (annotations only): https://huggingface.co/datasets/LeonOverload/primo-bench-json
- Media (video/frames): https://huggingface.co/datasets/LeonOverload/primo-video-media
- SFT CoT data: https://huggingface.co/datasets/LeonOverload/primo-sft-json
- RL data: https://huggingface.co/datasets/LeonOverload/primo-rl-json
- Project page: https://10-oasis-01.github.io/primo-r1-website/

## Benchmark Subsets

| Subset | Rows | Description |
| --- | ---: | --- |
| `real-humanoid-ood` | 4,791 | Real humanoid OOD; first choice for G1 dense reward transfer |
| `agibot-id` / `agibot-ood` | 3,000 / 3,000 | AgiBot in-domain / out-of-domain |
| `behavior-1k-id` / `behavior-1k-ood` | 3,999 / 3,000 | BEHAVIOR-1k |
| `robotwin-id` / `robotwin-ood` | 3,000 / 2,914 | RoboTwin simulation |

## Notes

- `primo-bench-json` contains no media; pair it with a locally extracted `primo-video-media`.
- Suggested local layout for bench / media: `../datasets/PRIMO-R1/{primo-bench-json,primo-video-media}/`
