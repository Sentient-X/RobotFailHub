# RobotFailHub

A continuously updated index of embodied-AI datasets, focused on data with **progress annotations**, **failure trajectories**, **failure-recovery trajectories** and **subtask annotations**, for research on failure detection, progress estimation, reinforcement-learning reward design and long-horizon task decomposition.

> Maintenance note: this repository **only records dataset metadata and download entry points**; it does not host raw video or large trajectory files. Size fields cite the official release page first; fields that could not be verified are marked `To be verified`.

## Dataset List

| Dataset | Date | Description | Domain | Modality | Size | Progress Annotation | Failure or Recovery Trajectory | Subtask Annotation | Failure Taxonomy | Download Link |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Robo-ValueRL](datasets/Robo-ValueRL.md) | 2026-07 | 240 h offline + 3k+ online rollouts; chip insertion, block disassembly; LeRobot v2.1 + value/quality | Robot / Real | video + state + action + language | 79.4k rows / 431 GB | Yes (remain_time / quality) | Yes (mix of success / suboptimal / corrected / failed) | No | No | [HF](https://huggingface.co/datasets/X-Humanoid/Robo-ValueRL) · [GitHub](https://github.com/Open-X-Humanoid/Robo-ValueRL) |
| [DenseReward](datasets/DenseReward.md) | 2026-07 | 26.6k episodes, 7.56M frames of dense reward; failures synthesized in simulation | Robot+Human / Sim+Real | video + language + dense reward | 26,579 episodes / 7.56M frames | Yes (frame-level 0–1) | Yes (collision/miss/fall/recover) | Yes (five-stage manipulation) | Yes | [Project](https://dense-reward.github.io/) · [Models HF](https://huggingface.co/densereward) |
| [VLAC-Cut-FullData](datasets/VLAC-Cut-FullData.md) | 2026-06 | Full VLAC-Cut release; expert/nonexpert × seen/unseen evaluation splits | Robot / Real + Sim | video/frame path + language + dense progress | ~956 GB (HF usedStorage) | Yes (frame-level dense progress + semantic anchors) | Yes (nonexpert/bad failures; text correction plan, no executed recovery) | Yes (stage descriptions + semantic anchors) | No unified taxonomy | [HF](https://huggingface.co/datasets/InternRobotics/VLAC-Cut-FullData) |
| [RoboReward](datasets/RoboReward.md) | 2026-01 | 45k train + RoboRewardBench; episode-level 1–5 progress score | Robot / Real | video + language + discrete reward | 54,135 examples (45,072 train) | Yes (episode-level 1–5 score) | Yes (synthesized negatives/near-misses + real RoboArena failures) | No | No | [HF Dataset](https://huggingface.co/datasets/teetone/RoboReward) · [Bench](https://crfm.stanford.edu/helm/robo-reward-bench/) |
| [Dopamine-Reward / GRM](datasets/Dopamine-Reward-GRM.md) | 2025-12 | 34.6M samples, 3400+ h, 100k+ trajectories; BEFORE/AFTER relative progress | Robot+Human / Sim+Real | multi-view image + language | 34.6M samples (json_all); ~239 GB images + 6.1 GB JSON | Yes (hop-based relative progress) | Yes (mix of real / sim / human video) | Yes (step-wise discretization) | No | [HF Dataset (gated)](https://huggingface.co/datasets/tanhuajie2001/Robo-Dopamine-GRM-Dataset) |
| [RoboArena](datasets/RoboArena.md) | 2025-06 | Distributed double-blind real-robot policy evaluation; includes preference, feedback and successful/failed rollouts | Robot / Real | video + proprio/action + YAML | 3,883 sessions; 10,783 policy episodes; 21.7 GB | Yes (task-success) | Yes (public evaluation rollouts) | No | No | [HF DataDump](https://huggingface.co/datasets/RoboArena/DataDump_07-17-2026) · [Website](https://robo-arena.github.io/) |
| [PhAIL](datasets/PhAIL.md) | 2026-05 | Franka FR3 real-robot VLA evaluation; public video, telemetry, results and safety-stop runs | Robot / Real | multi-view video + state/action + events | v1.0: 594 eval runs; 352 demos (~12 GB) | Yes (completion / time / UPH) | Yes (failure / timeout / safety stop; no corrective action) | No | Yes (coarse-grained outcome) | [Release](https://phail.ai/releases/v1.0) · [Paper](https://arxiv.org/abs/2605.29710) |
| [ManipArena](datasets/ManipArena.md) | 2026-03 | 20 reasoning-oriented real-robot tasks; public expert demonstrations | Robot / Real + Sim | 3×RGB + state/action + motor + language | 10,812 trajectories; 13.5M frames; ~188 h | No unified frame-level progress | No (public real data are expert demos) | Yes (partial-credit + three-level language descriptions) | No | [HF (gated)](https://huggingface.co/datasets/ManipArena/maniparena-dataset) · [Paper](https://arxiv.org/abs/2603.28545) |
| [RoboChallenge Table30 v2](datasets/RoboChallenge-Table30v2.md) | 2026-05 | Companion data for an online real-robot benchmark with 30 tasks and 4 embodiments | Robot / Real | multi-view video + robot state + metadata | ~1.01 TB | Yes (task score / grading points) | To be verified (not a unified eval rollout dump) | Yes (grading points) | No | [HF](https://huggingface.co/datasets/RoboChallenge/Table30v2) · [Website](https://robochallenge.ai/) |
| [VLA-REPLICA](datasets/VLA-REPLICA.md) | 2026-05 | Low-cost, reproducible SO-101 real-robot VLA benchmark; ID/OOD reference scenes | Robot / Real | top/wrist RGB + state/action + language | 10 tasks; 500 demos; 90 scene refs; ~1.97 GB | No | No public unified test rollout dump | No | No | [HF](https://huggingface.co/datasets/HenryZhang/VLAReplica_SFT_data) · [GitHub](https://github.com/IRVLUTD/VLAReplica) |
| [RoboDojo Real](datasets/RoboDojo-Real.md) | 2026-07 | 18 real-robot tasks, 3 embodiments; RealEval remote evaluation | Robot / Real + Sim | task/config assets + result artifacts | 18 real tasks; bulk rollouts to be verified | Yes (evaluation-result level) | Public bulk real rollouts not confirmed | To be verified | No | [Website](https://robodojo-benchmark.com/) · [GitHub](https://github.com/RoboDojo-Benchmark/RoboDojo) |
| [FurnitureBench](datasets/FurnitureBench.md) | 2023-05 | Long-horizon real-world furniture assembly benchmark; public successful demonstrations | Robot / Real | RGB + robot state + action + reward/skill | 5,100 demos; 219.6 h; ~1.18 TB | Yes (reward / skill flags) | No (successful demos) | Yes (skill flags) | No | [Dataset](https://clvrai.github.io/furniture-bench/docs/tutorials/dataset.html) · [GitHub](https://github.com/clvrai/furniture-bench) |
| [TriFinger RL](datasets/TriFinger-RL.md) | 2023-05 | Push/Lift real-robot offline RL data; behavior policies of varying quality | Robot / Real + Sim | Zarr state/action/reward + optional RGB | >100 h; a single real image dataset is 46–100 GB | Yes (reward / return) | Suboptimal behavior (no recovery labels) | No | No | [Data (DOI)](https://doi.org/10.17617/3.DXZ7TL) · [Docs](https://webdav.tuebingen.mpg.de/trifinger-rl/docs/datasets/index.html) |
| [PRIMO-R1](datasets/PRIMO-R1.md) | 2026-03 | Process reasoning critic; 116.8k SFT + 328.5k RL; 23.7k bench | Robot / Real + Sim | video + init/current frame + CoT progress | Bench 23.7k; media ~78 GB | Yes (1–100 + CoT) | Yes (failure detection + real-humanoid OOD) | No | No | [HF Collection](https://huggingface.co/collections/LeonOverload/primo-r1) · [Bench JSON](https://huggingface.co/datasets/LeonOverload/primo-bench-json) |
| [AgiBot World 2026](datasets/AgiBotWorld2026.md) | 2026-03 | G2 real-world scenes; Task Frame / skill / bbox / failure-recovery key frames | Robot / Real | multi-view video + state + action + language | ~2,976 h / 13.2 TB; sample ~7 GB | Yes (step/success_frame) | Yes (Error/Intervention + recovery) | Yes (Task Frame + instruction_segments) | Yes (error_cause) | [HF](https://huggingface.co/datasets/agibot-world/AgiBotWorld2026) · [Site](https://agibot-world.com) |
| [REBOOT](datasets/REBOOT.md) | 2026-05 | REBOOT26 bimanual WidowX recovery trajectories; LeRobot v3.0 | Robot / Real | video + state + action | 38 task datasets (HF org) | No | Yes (recovery / remove / install) | No | No | [HF Org](https://huggingface.co/REBOOT26) |
| [Guardian FailCoT / RoboFail](datasets/Guardian-FailCoT-RoboFail.md) | 2025-12 | FailCoT synthetic failure reasoning; RoboFail OOD evaluation | Robot / Sim + Real | multi-view image + CoT | FailCoT 30.9k train; RoboFail 130 scenarios | No | Yes (planning + execution failures) | Yes | Yes | [Guardian HF](https://huggingface.co/collections/paulpacaud/robotic-failure-detection-dataset-and-model-guardian) · [RoboFail OOD](https://huggingface.co/datasets/paulpacaud/Guardian-FailCoT-OOD-datasets) |

### Real-robot evaluation data roles (R2)

To avoid describing "the training set of a real-robot benchmark" as "test rollouts of a candidate policy", entries related to real-robot evaluation use the following classification:

| Class | Definition | Current entries |
| --- | --- | --- |
| **R2-A** | Real policy evaluation rollouts / logs have been published; the data itself is the evaluation result | RoboArena, PhAIL |
| **R2-B** | Real-robot benchmark, but the public download is mainly demonstrations, task/config assets or reference scenes; test rollouts must be produced by running the benchmark yourself or through remote evaluation | ManipArena, RoboChallenge Table30 v2, VLA-REPLICA, RoboDojo Real, FurnitureBench |
| **R2-C** | Offline benchmark based mainly on real robots (may include supplementary simulation sources), kept separate from modern online VLA evaluation | VLAC-Cut-FullData, TriFinger RL |

Each detail card states this explicitly with `Dataset Role` and `R2 Classification`. A `safety stop` only indicates a risk-intervention signal; it is not the same as a `corrective takeover action` in which an operator takes over and continues.

Although VLAC-Cut-FullData is classed as R2-C, it is not purely real-robot data: the paper reports that about **96.8% of its full annotations come from real robots** (ARX, DROID) and about **3.2% from simulation** (LIBERO, VLABench).

### Field descriptions

| Column | Meaning |
| --- | --- |
| Dataset | Dataset name (see the card under `datasets/` for details) |
| Date | Year and month of the paper / official release |
| Description | Robot types, tasks and annotation characteristics covered |
| Domain | Robot/Human + Real/Sim |
| Modality | Observations / state / action / language, etc. |
| Size | Official size or snapshot size |
| Dataset Role | Data role such as evaluation rollout, training demonstration or benchmark asset (detail card field) |
| R2 Classification | R2-A / R2-B / R2-C real-robot evaluation class (detail card field) |
| Progress Annotation | Whether there are progress / value / dense reward annotations |
| Failure or Recovery Trajectory | States separately whether there are successes, failures, actually executed recoveries, and text-only correction plans; `non-expert`, final failure and recovery are not interchangeable |
| Subtask Annotation | Whether there are subtask / stage annotations |
| Failure Taxonomy | Whether there is a taxonomy of failure types |
| Download Link | Official download entry point |

## Local mirror (optional)

This repository only stores metadata. To cache HF data locally, a relative directory is recommended:

```text
../datasets/<DatasetName>/
```

Example (run `huggingface-cli login` first; run from the repository root):

```bash
hf download X-Humanoid/Robo-ValueRL --repo-type dataset --local-dir ../datasets/Robo-ValueRL
hf download teetone/RoboReward --repo-type dataset --local-dir ../datasets/RoboReward
hf download RoboArena/DataDump_07-17-2026 --repo-type dataset --local-dir ../datasets/RoboArena
# VLAC-Cut-FullData is about 956 GB in total; this example downloads only the scripts and the four test splits
hf download InternRobotics/VLAC-Cut-FullData --repo-type dataset --include "README.md" "scripts/*" "benchmark_style_all/test_*/*" --local-dir ../datasets/VLAC-Cut-FullData-eval
hf download ManipArena/maniparena-dataset --repo-type dataset --include "real/**" --local-dir ../datasets/ManipArena-real
hf download HenryZhang/VLAReplica_SFT_data --repo-type dataset --local-dir ../datasets/VLA-REPLICA/SFT-data
# Dopamine is a gated dataset; request access on HF first
hf download tanhuajie2001/Robo-Dopamine-GRM-Dataset --repo-type dataset --local-dir ../datasets/Dopamine-GRM
hf download LeonOverload/primo-bench-json --repo-type dataset --local-dir ../datasets/PRIMO-R1/primo-bench-json
hf download agibot-world/AgiBotWorld2026 --repo-type dataset --local-dir ../datasets/AgiBotWorld2026
hf download paulpacaud/Guardian-FailCoT-OOD-datasets --repo-type dataset --local-dir ../datasets/Guardian-OOD
```

## Contributing and maintenance

- Mark uncertain information as `To be verified` or `Unknown`.
- To add a dataset: add a card under `datasets/` and add a row to the table above.
- Prefer links to the **paper / project page / Hugging Face / GitHub**; avoid linking only to secondary reposts.
