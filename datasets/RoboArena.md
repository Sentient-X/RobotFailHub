# RoboArena

| Field | Value |
| --- | --- |
| **Date** | 2025-06 (DataDump 2026-07-17) |
| **Paper** | [RoboArena: Distributed Real-World Evaluation of Generalist Robot Policies](https://arxiv.org/abs/2506.18123) |
| **Domain** | Robot / Real |
| **Dataset Role** | evaluation rollout |
| **R2 Classification** | R2-A — real policy evaluation artifacts have been published |
| **Modality** | multi-view video, proprioception/action NPZ, session YAML, preference, task-success, long-form feedback |
| **Size** | 3,883 evaluation sessions; 10,783 policy episodes; 27,148 MP4; 10,783 NPZ; 21.7 GB |
| **Progress Annotation** | Yes — task-success score |
| **Failure or Recovery Trajectory** | Yes — multi-policy rollouts include successes and failures |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No |
| **License** | MIT |

## Description

A distributed real-robot policy evaluation platform and data dump. It collects double-blind, multi-policy evaluation rollouts on the DROID robot platform, including pairwise preference, task-success, long-form evaluator feedback and action/proprioceptive state. Reward models such as RoboReward also cite its real failure samples for training.

## Download

- Hugging Face DataDump: https://huggingface.co/datasets/RoboArena/DataDump_07-17-2026
- Website: https://robo-arena.github.io/
- Paper: https://arxiv.org/abs/2506.18123

## Notes

- The DataDump is a periodic snapshot; newer versions may follow.
- In the 2026-07-17 snapshot, `metadata.yaml` stores the instruction, preference, feedback, timestamps and each policy's outcome; `global_metadata.yaml` stores aggregate statistics and the policy index.
- Preference/failure-rich rollouts are not the same as data with human corrective takeover actions.
- Local mirror: `hf download RoboArena/DataDump_07-17-2026 --repo-type dataset --local-dir .../RoboArena`
