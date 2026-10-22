# Robo-ValueRL

| Field | Value |
| --- | --- |
| **Date** | 2026-07 |
| **Paper** | [Robo-ValueRL: Reliable Value Estimation for Offline-to-Online RL](https://arxiv.org/abs/2607.09866) |
| **Domain** | Robot / Real |
| **Modality** | video, proprioception, action, language instruction |
| **Size** | 79,439 rows / **431 GB** (HF); 240 h offline + 3,000+ online rollouts |
| **Progress Annotation** | Yes — remain_time / value-derived quality labels |
| **Failure or Recovery Trajectory** | Yes — mix of successful, suboptimal, corrected and failed |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No |

## Description

A real-robot value-guided RL dataset released by X-Humanoid, covering long-horizon manipulation such as chip insertion and block disassembly. The data is organized in LeRobot v2.1 format, contains offline demonstrations and online policy rollouts, and comes with value/quality annotations; it can be used for progress critics, dense reward and failure-aware policy learning.

## Tasks

- Chip insertion
- Block disassembly

## Download

- Hugging Face: https://huggingface.co/datasets/X-Humanoid/Robo-ValueRL
- GitHub: https://github.com/Open-X-Humanoid/Robo-ValueRL
- Project: https://gewu-lab.github.io/Robo-ValueRL/

## Notes

- Together with DenseReward and RoboReward, one of the high-priority 2026 datasets in the dense/progress reward direction.
- Suggested local mirror path: `../datasets/Robo-ValueRL`
