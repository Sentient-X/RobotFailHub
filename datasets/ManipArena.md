# ManipArena

| Field | Value |
| --- | --- |
| **Date** | 2026-03 |
| **Paper** | [ManipArena: Comprehensive Real-world Evaluation of Reasoning-Oriented Generalist Robot Manipulation](https://arxiv.org/abs/2603.28545) |
| **Domain** | Robot / Real + Sim (this card focuses on `real/`) |
| **Dataset Role** | benchmark-aligned expert demonstration |
| **R2 Classification** | R2-B — real-robot benchmark; the public data is mainly for training/adaptation |
| **Modality** | 3×RGB video, state, action, motor position/velocity/current, language |
| **Size** | 20 real tasks, 10,812 expert trajectories, 13.5M frames, about 188 robot-hours; plus 3 simulation tasks |
| **Progress Annotation** | No unified frame-level progress; the benchmark supports partial-credit scoring |
| **Failure or Recovery Trajectory** | No — the public `real/` data is mainly expert demonstrations |
| **Subtask Annotation** | Yes — the benchmark uses subtask-level partial credit; 15 tabletop tasks also provide three-level language descriptions |
| **Failure Taxonomy** | No |
| **License** | Apache-2.0; HF uses auto-approved gated access |

## Description

ManipArena is a standardized real-robot evaluation framework for reasoning-oriented bimanual manipulation, covering execution reasoning, semantic reasoning and mobile manipulation. The public Hugging Face data uses the LeRobot v2.1 structure; the real portion contains 20 tasks, three synchronized camera streams and 20 Hz state/action data.

The public trajectories are expert demonstrations for training or adapting competing models; physical testing of a candidate policy must be run separately following the benchmark protocol, and these demonstrations must not be labeled as evaluation rollouts.

## Dataset Layout

```text
real/
├── execution_reasoning/   # 10 tasks, about 5,000 episodes
├── semantic_reasoning/    # 5 tasks, about 2,800 episodes
└── mobile_manipulation/   # 5 tasks, about 2,900 episodes
```

Each task contains Parquet state/action, MP4 video and LeRobot metadata. Tabletop tasks use 56-D state/action; mobile manipulation tasks use 62-D state/action.

## Official Sources

- Dataset: https://huggingface.co/datasets/ManipArena/maniparena-dataset
- Paper: https://arxiv.org/abs/2603.28545

## Download

```bash
hf download ManipArena/maniparena-dataset \
  --repo-type dataset \
  --include "real/**" \
  --local-dir ../datasets/ManipArena-real
```

## Notes

- Before downloading, log in to Hugging Face and accept the auto-approved access conditions.
- The HF repository also contains sim data; for real-robot research use `--include "real/**"` rather than mirroring everything.
- The three-level language annotation covers the 15 tabletop tasks and does not yet cover mobile manipulation.
