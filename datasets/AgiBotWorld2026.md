# AgiBot World 2026

| Field | Value |
| --- | --- |
| **Date** | 2026-03 |
| **Paper / Release** | [AGIBOT WORLD 2026 open-source release](https://www.agibot.com/article/231/detail/54.html) |
| **Domain** | Robot / Real (with companion GenieSim simulation data) |
| **Modality** | multi-view video + depth + state + action + language |
| **Size** | Full set about **2,976 h / 13.2 TB** (HF); official sample `task_3777` ~7 GB; HF `size_categories` lists 1K–10K episodes |
| **Progress Annotation** | Yes — `instruction_segments` include `success_frame_index`; step/skill-level progress, not a numeric dense reward |
| **Failure or Recovery Trajectory** | Yes — error-recovery trajectories are kept; `Error Frame` / `Intervention Frame` / `Success Frame` |
| **Subtask Annotation** | Yes — `Task Frame` subtask segments + `instruction_segments` atomic skills (Pick/Place, etc.) |
| **Failure Taxonomy** | Yes — fields such as `frame_detail.error_cause` and `restorable` |

## Description

**AGIBOT WORLD 2026** is a real-world embodied-AI dataset released by AgiBot, collected on the **AgiBot G2** dual-arm platform and covering commercial, household and other scenes. The data is organized as **LeRobot v2.1** and extends the standard schema with three layers of annotation:

1. **Task Frame** — subtask segments within a long-horizon episode (natural language + frame range)
2. **2D Bounding Box** — boxes around interacted objects + category + camera
3. **Instruction Segments** — finer-grained step/skill annotations (including `success_frame_index`)

In addition, `key_frame` supports failure / intervention / success key frames, with fields including `error_cause` and `restorable`, which suits failure mining, recovery imitation and hierarchical policy research. The official `split_episode.py` splits long-horizon trajectories into single-instruction LeRobot episodes.

## Annotation Highlights

| Type | Field / Name | Use |
| --- | --- | --- |
| Subtask | `Task Frame` | Long-horizon segmentation, single-instruction training |
| Skill step | `instruction_segments[].skill` | Atomic operations (Pick/Place, etc.) |
| Object | `2D Bounding Box` | object-conditioned / grounding |
| Failure | `Error Frame` + `error_cause` | failure detection / taxonomy |
| Intervention/recovery | `Intervention Frame`, `take_over`, `restorable` | HIL / recovery |
| Success | `Success Frame`, `is_result_succeed` | success verification |

## Download

- Hugging Face: https://huggingface.co/datasets/agibot-world/AgiBotWorld2026
- Official site: https://agibot-world.com
- Challenge subset: https://huggingface.co/datasets/agibot-world/AgiBotWorldChallenge-2026
- Sample: `task3777/380098_380609.tar.gz` (~7 GB)

```bash
# Fetch only the sample task (recommended to check the structure first)
GIT_LFS_SKIP_SMUDGE=1 git clone https://huggingface.co/datasets/agibot-world/AgiBotWorld2026
cd AgiBotWorld2026
git sparse-checkout init
git sparse-checkout set task3777
git pull origin main
```

## Notes

- License: **CC BY-NC-SA 4.0** (commercial use requires a separate license)
- The dataset is released in stages (research tracks such as ImitationLearning / ReinforcementLearning)
- Related to the `agibot-id/ood` bench subsets of PRIMO-R1, but this entry points to the official full AgiBotWorld2026 data release
- Suggested local mirror: `../datasets/AgiBotWorld2026/`
