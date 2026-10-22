# REBOOT (REBOOT26 Recovery Trajectories)

| Field | Value |
| --- | --- |
| **Date** | 2026-05 (HF update time) |
| **Paper** | To be verified — not the CoRL 2023 dexterous RL paper [REBOOT (2309.03322)](https://arxiv.org/abs/2309.03322) |
| **Domain** | Robot / Real |
| **Modality** | video + proprio + action (LeRobot v3.0) |
| **Size** | 38 task-level datasets (HF org); about 18–60 episodes per task |
| **Progress Annotation** | No |
| **Failure or Recovery Trajectory** | Yes — includes `*_recovery_*` recovery/correction trajectories |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No |

## Description

Bimanual WidowX manipulation data released by the [Hugging Face REBOOT26](https://huggingface.co/REBOOT26) organization, in LeRobot v3.0 format. Task names distinguish stages such as **install / remove / recovery**; the recovery subsets record human recovery after a failure followed by continued execution, suitable for failure-recovery imitation / HIL fine-tuning research.

> **Name disambiguation:** the robotics community also has the CoRL 2023 paper "REBOOT: Reuse Data for Bootstrapping Dexterous Manipulation", which focuses on bootstrapping with an RL replay buffer and is different from the recovery trajectory data in this Hub entry.

## Example Datasets

- https://huggingface.co/datasets/REBOOT26/sample_recovery-demonstration
- https://huggingface.co/datasets/REBOOT26/16mm-bar_recovery_remove
- https://huggingface.co/datasets/REBOOT26/nema1-15-plug_remove
- Full list: https://huggingface.co/REBOOT26/datasets

## Download

```bash
hf download REBOOT26/sample_recovery-demonstration --repo-type dataset \
  --local-dir ../datasets/REBOOT/sample_recovery-demonstration
```

## Notes

- Robot type: `bi_widowxai_follower_robot`
- Similar to LeRobot HIL / RaC-style recovery-correction data collection protocols, but released independently
