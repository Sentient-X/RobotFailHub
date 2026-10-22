# TriFinger RL Datasets

| Field | Value |
| --- | --- |
| **Date** | 2023-05 (corrected data release) |
| **Paper** | [Benchmarking Offline Reinforcement Learning on Real-Robot Hardware](https://openreview.net/forum?id=3k5CUGDLNdd) |
| **Domain** | Robot / Real + Sim (this card focuses on the `real` variants) |
| **Dataset Role** | real-robot offline RL benchmark dataset |
| **R2 Classification** | R2-C — real-robot offline benchmark |
| **Modality** | Zarr state/action/reward/timeout/terminal; optional three-camera RGB |
| **Size** | Over 100 hours; each full Push set about 2.88 million transitions, each full Lift set about 3.6 million transitions; a single image-variant set about 46–100 GB |
| **Progress Annotation** | Yes — dense/sparse reward, return, success metrics |
| **Failure or Recovery Trajectory** | Suboptimal behavior present — expert, weak-and-expert, half-expert, mixed policy proficiency; no explicit recovery labels |
| **Subtask Annotation** | No |
| **Failure Taxonomy** | No |
| **License** | Data CC BY 4.0; code BSD-3-Clause |

## Description

TriFinger RL Datasets provide Push and Lift data on real and simulated TriFingerPro robots, for offline reinforcement learning, imitation learning, dynamics learning and representation learning. The real versions contain transitions collected by behavior policies of varying quality, and come in Zarr variants with and without camera images.

This is a real-robot offline benchmark, not a modern language-conditioned online VLA evaluation. The weak/mixed data contains suboptimal behavior, but there is no official unified failure taxonomy or recovery label per trajectory.

## Dataset Families

- Task: `push` / `lift`
- Source: `real` / `sim`
- Quality: `expert` / `smooth-expert` / `weak-n-expert` / `half-expert` / `mixed`
- Image variant: name contains `-image`

Naming format:

```text
trifinger-cube-<task>-<sim/real>-<dataset_type>[-image]-v0.zarr
```

## Official Sources

- Documentation: https://webdav.tuebingen.mpg.de/trifinger-rl/docs/datasets/index.html
- Data repository: https://doi.org/10.17617/3.DXZ7TL
- Loader: https://github.com/rr-learning/trifinger_rl_datasets
- Paper: https://openreview.net/forum?id=3k5CUGDLNdd

## Download

After installing the loader, the first call downloads on demand to `~/.trifinger_rl_datasets`:

```bash
pip install trifinger_rl_datasets
```

```python
import gymnasium as gym
import trifinger_rl_datasets

env = gym.make("trifinger-cube-push-real-expert-v0")
dataset = env.get_dataset()
```

## Notes

- Before 2023-05-15, some weak/half-expert and lift-sim data contained errors; use the official corrected versions.
- The image variants are more than an order of magnitude larger than the state-only variants; download a state-only variant first.
