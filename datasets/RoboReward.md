# RoboReward

| Field | Value |
| --- | --- |
| **Date** | 2026-01 |
| **Paper** | [RoboReward: General-Purpose Vision-Language Reward Models for Robotics](https://arxiv.org/abs/2601.00675) |
| **Domain** | Robot / Real |
| **Modality** | video, language, discrete episode-level reward (1–5) |
| **Size** | **54,135 examples** (45,072 train / 6,232 val / 2,831 test RoboRewardBench) |
| **Progress Annotation** | Yes — episode-level 1–5 progress score |
| **Failure or Recovery Trajectory** | Yes — synthesized negatives/near-misses + real RoboArena failures |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No |

## Description

A large-scale progress-scoring dataset of real-robot rollouts, used to train vision-language robotic reward models. RoboRewardBench provides a standardized evaluation protocol and is comparable with DenseReward, Dopamine-GRM and others on the same progress prediction task.

## Download

- Hugging Face Dataset: https://huggingface.co/datasets/teetone/RoboReward
- Benchmark: https://crfm.stanford.edu/helm/robo-reward-bench/
- Models: https://huggingface.co/teetone (RoboReward-4B/8B etc. to be verified)

## Notes

- The discrete 1–5 score can be mapped to coarse progress; complementary to frame-level dense reward datasets.
- Local mirror: `hf download teetone/RoboReward --repo-type dataset --local-dir .../RoboReward`
