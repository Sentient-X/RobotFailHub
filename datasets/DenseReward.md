# DenseReward

| Field | Value |
| --- | --- |
| **Date** | 2026-07 |
| **Paper** | [DenseReward: Dense Reward Learning via Failure Synthesis for Robotic Manipulation](https://arxiv.org/abs/2607.13033) |
| **Domain** | Robot+Human / Sim+Real |
| **Modality** | video, language instruction, frame-level dense reward |
| **Size** | **26,579 episodes / 7,560,942 frame-level samples** (paper table) |
| **Progress Annotation** | Yes — frame-level 0–1 dense reward |
| **Failure or Recovery Trajectory** | Yes — synthesized failures such as collision / miss grasp / drop / recover |
| **Subtask Annotation** | Yes — five stages: Reach / Grasp / Lift / Move / Place |
| **Failure Taxonomy** | Yes — failure mode annotations |

## Description

Physically realistic failure trajectories are synthesized automatically through targeted perturbation in simulation and annotated with frame-level dense reward. It covers multiple sources including DROID, Isaac Sim, RoboSuite and LIBERO, and is used to train the DenseReward models and downstream MPC / RL.

## Download

- Project page: https://dense-reward.github.io/
- Models (HF): https://huggingface.co/densereward
  - [`densereward-1frame`](https://huggingface.co/densereward/densereward-1frame)
  - [`densereward-3frame-thinking`](https://huggingface.co/densereward/densereward-3frame-thinking)
- **Full training dataset**: To be verified — the paper says the dataset will be released; as of 2026-08 there is no standalone HF dataset repo yet; watch the [densereward](https://huggingface.co/densereward) org for updates

## Notes

- Directly comparable with RoboReward on the dense reward prediction benchmark.
- Local mirror: add the `hf download` command once the official dataset repo is published.
