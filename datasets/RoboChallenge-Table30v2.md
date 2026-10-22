# RoboChallenge Table30 v2

| Field | Value |
| --- | --- |
| **Date** | 2026-05 (Table30 v2 data release) |
| **Paper** | [RoboChallenge: Large-scale Real-robot Evaluation of Embodied Policies](https://arxiv.org/abs/2510.17950) |
| **Domain** | Robot / Real |
| **Dataset Role** | benchmark support / training data |
| **R2 Classification** | R2-B — real-robot benchmark; the public repository is not a unified test rollout dump of candidate policies |
| **Modality** | multi-view H.264 video, robot state JSONL, joint/EEF/gripper state, task and episode metadata |
| **Size** | 30 tasks, 4 embodiments; HF files total about 1.01 TB |
| **Progress Annotation** | Yes (task level) — grading points, task score, success rate |
| **Failure or Recovery Trajectory** | To be verified — the public repository is positioned as training/benchmark support data; unified failure rollout annotations not confirmed |
| **Subtask Annotation** | Yes (grading points) — some tasks are scored on multiple grading points |
| **Failure Taxonomy** | No unified taxonomy |
| **License** | To be verified — the HF dataset card does not declare a unified data license |

## Description

RoboChallenge is a large-scale online real-robot evaluation system; Table30 v2 provides 30 real-robot manipulation tasks covering four embodiments: ARX5, UR5, ALOHA and DOS-W1. The public data repository stores multi-camera video, robot state and episode metadata per task, and provides an example of converting to LeRobot.

The public repository is mainly benchmark-aligned training/support data; official model test results are produced through RoboChallenge real-robot evaluation and the leaderboard, so the 1.01 TB of data as a whole must not be labeled as evaluation rollouts.

## Official Sources

- Benchmark: https://robochallenge.ai/
- Table30 v2 dataset: https://huggingface.co/datasets/RoboChallenge/Table30v2
- Technical report: https://robochallenge.ai/robochallenge_techreport_V2.pdf
- Paper: https://arxiv.org/abs/2510.17950

## Download

The full repository is about 1.01 TB; select files by task rather than downloading everything:

```bash
hf download RoboChallenge/Table30v2 \
  --repo-type dataset \
  --include "arrange_flowers*" \
  --local-dir ../datasets/Table30v2/arrange_flowers
```

## Notes

- Check the HF file tree and the size of each task before downloading.
- The data card provides a LeRobot conversion example, but other embodiments need their own adaptation.
- Code license, paper license and data license are not interchangeable; keep `To be verified` until the official dataset license is published.
