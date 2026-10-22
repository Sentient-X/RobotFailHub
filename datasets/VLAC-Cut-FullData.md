# VLAC-Cut-FullData

| Field | Value |
| --- | --- |
| **Date** | 2026-07 (HELP paper; HF dataset created 2026-06-23) |
| **Paper** | [HELP: Human-Efficient Large-Scale Robot Post-Training with Rollout Segmentation](https://arxiv.org/abs/2607.09776) |
| **Domain** | Robot / Real + Sim, mainly real robot (full records about 96.8% Real, 3.2% Sim) |
| **Dataset Role** | Offline process-supervision data for the VLAC-Cut progress critic + Video Progress Benchmark (VPB) + raw data archive |
| **R2 Classification** | R2-C — mixed-source offline benchmark dominated by real-robot data; not an online real-robot evaluation rollout dump of candidate VLAs |
| **Modality** | video / extracted-frame paths, task language, sparse progress anchors, dense signed progress, optional grounding/action metadata |
| **Size** | HF `usedStorage` 956,063,943,607 bytes (about 956 GB / 890 GiB); the paper's full inventory is 35,230 records, 26,615 episodes, 15,206 task units, 464,446 progress points |
| **Progress Annotation** | Yes — sparse human `human_annotated_progress` + frame-level `dense_kinematic_progress` obtained by linear interpolation, ranging from -100 to 100 |
| **Failure or Recovery Trajectory** | Successes, failures and recovery behavior are all present; ARX explicitly includes really executed failures and recoveries; not every `non-expert` record ends in failure |
| **Subtask Annotation** | Yes — task stages/percentages in `task_description` + `semantic_anchors` |
| **Failure Taxonomy** | No unified discrete taxonomy; specific errors are described in free text in `error_success_analysis` |
| **License** | HF marks it as `other`; the data card gives no specific license terms |

## Key Findings

This dataset **contains both real-robot and simulation data, but real-robot data is by far the majority**. The data sources and full record composition in the paper are:

| Source | Environment | Records | Share | Main role |
| --- | --- | ---: | ---: | --- |
| ARX-data | Real robot | 17,935 | 50.9% | Targeted collection of success, failure, regression and real recovery behavior |
| DROID | Real robot | 16,181 | 45.9% | Large-scale, multi-task real manipulation video, mainly successful / near-expert demonstrations |
| LIBERO | Simulation | 545 | 1.5% | Supplements controlled task variation and simulated manipulation scenes |
| VLABench | Simulation | 569 | 1.6% | Supplements benchmark-style tasks and simulation coverage |
| **Total** | **Real + Sim** | **35,230** | **about 96.8% Real / 3.2% Sim** | Mainly real robot, simulation as a supplement |

These percentages come from Figure 7 of the HELP paper; because each is rounded, the sum may not be exactly 100%. The paper states clearly that LIBERO and VLABench are only supplementary sources, not the bulk of the dataset; all selected videos were re-annotated with a unified process-level schema, and the progress labels are not taken directly from the source datasets' original labels.

## Success, Failure and Recovery

This dataset is not purely failure data, nor is it only "success + failure" without recovery. A more accurate breakdown of the trajectories:

| Concept | Meaning in this dataset |
| --- | --- |
| **Expert** | Defined by the annotated progress curve: no decrease between adjacent progress points; it denotes a monotonic / near-expert progress pattern and is not strictly the same as "definitely succeeds in the end" |
| **Non-expert** | At least one decrease in signed progress between adjacent points; may include grasp failures, collisions, drops, interaction with the wrong object or placement errors, and may also recover afterwards and finally succeed |
| **Failure / regression** | An action moves the task state away from the goal; progress may stall, decrease, or even fall below the initial state and become negative |
| **Executed recovery** | Recovery actions that actually happened in the original trajectory. The paper explicitly shows ARX re-grasping, re-alignment and post-failure pose correction, so such recoveries do exist |
| **Correction plan** | A text suggestion in `semantic_anchors` about "how to correct next"; by itself it does not prove that a subsequent recovery action was executed |

Therefore, `expert` must not be written as "success", `non-expert` must not be written as "final failure", and not every sample containing a `correction_plan` counts as a recovery trajectory. To determine whether a trajectory truly recovers, check whether progress rises again after the failure, the subsequent actions in the video, and the final task state.

The paper also involves two kinds of data that are easily confused with public raw recovery trajectories:

1. **HELP's HITL recovery data**: in the post-training pipeline on 12 physical robots, operators took over erroneous states and performed corrections. This is a data stream of the HELP experiments and must not be assumed to be fully included in the VLAC-Cut-FullData release.
2. **Counterfactual reverse-progress augmentation**: regression-and-recovery training samples constructed from existing pairs of progress points by "playing backwards and then forwards again". The paper states clearly that this requires no new robot rollouts, so it is synthetic training augmentation, not newly collected real recovery trajectories.

## Data Size and Splits

The paper gives two different counting bases:

- **Full annotation inventory**: 35,230 records, 26,615 episodes, 15,206 task units, 464,446 progress points, corresponding to the full annotated assets.
- **Curated train/evaluation dataset**: 28,167 records, 22,978 episodes, 15,206 task units, 375,172 progress points, used for training and VPB evaluation.

A `record` is the annotation unit for a single video/view; different camera views of the same episode may correspond to multiple records, so the record count must not be taken as the number of robot executions.

| Split | Records | Tasks | Progress points | Expert / Non-expert | ARX / DROID / Sim |
| --- | ---: | ---: | ---: | ---: | ---: |
| Train | 24,652 | 13,996 | 331,762 | 15,467 / 9,185 | 10,357 / 13,457 / 838 |
| Expert seen | 1,043 | 1,043 | 11,769 | 1,043 / 0 | 356 / 641 / 46 |
| Expert unseen | 1,043 | 1,043 | 12,333 | 1,043 / 0 | 356 / 641 / 46 |
| Non-expert seen | 713 | 713 | 9,458 | 0 / 713 | 540 / 165 / 8 |
| Non-expert unseen | 716 | 716 | 9,850 | 0 / 716 | 540 / 168 / 8 |
| **Curated total** | **28,167** | **15,206** | **375,172** | **17,553 / 10,614** | **12,149 / 15,072 / 946** |

The four held-out VPB splits total 3,515 records. `seen/unseen` is split by whether the semantic task unit appears in the training instruction data; different views of the same physical execution are placed in the same split to avoid leakage.

## Annotation Schema

Each benchmark record mainly contains:

- `metadata`: data source, task instruction, task stage description, frame count, FPS, available views and `is_expert`.
- `frame_index`: target paths for each frame/view, with `__VLAC2_FRAMES_ROOT__/` as a placeholder prefix.
- `dense_kinematic_progress`: per-frame signed progress linearly interpolated from sparse human anchors, not an independent human score for each frame.
- `semantic_anchors`: human progress at key frames, action/state descriptions, progress explanations, success/failure analysis and a text correction plan.

The semantics of signed progress: `100` means completed, `0` means the initial state, and negative values mean the task state is worse than the initial setup. Annotation points correspond to semantic events, such as reaching a subgoal, failure, stalling, regression or recovery, rather than sampling at fixed time intervals.

## Boundaries with the HELP / VLAC-Cut Models

- **VLAC-Cut-FullData** is the public release of raw video, process annotations and benchmark JSON.
- **VPB** is the strictly held-out 3,515-record offline video progress evaluation set within it.
- **The VLAC-Cut model SFT corpus** is not the same as this HF repository. The paper also converts the annotated data into 4.76M selected samples and mixes in auxiliary training data such as LLaVA-style, RoboReward, RoboVQA, SpatialQA and ProgressLM CoT.
- **The HELP real-robot post-training experiment** is a system experiment in which two operators supervise 12 physical robots; the four downstream manipulation tasks and HITL takeover data in the paper must not be conflated with VPB's Real + Sim data composition.

## Repository Layout

```text
benchmark_style_all/
  train/video_progress_benchmark_file.json
  test_expert_seen/video_progress_benchmark_file.json
  test_expert_unseen/video_progress_benchmark_file.json
  test_nonexpert_seen/video_progress_benchmark_file.json
  test_nonexpert_unseen/video_progress_benchmark_file.json
  all/video_progress_benchmark_file.json
annotation_files_raw/
data/
  vlac2_release_data_part01_arx_group_a.tar.zst.part-*
  ...
  vlac2_release_data_part07_other_sources.tar.zst
scripts/
  unpack_data.sh
  extract_vlac2_release_frames.py
```

## Official Sources

- Paper: https://arxiv.org/abs/2607.09776
- Full dataset: https://huggingface.co/datasets/InternRobotics/VLAC-Cut-FullData
- Benchmark: https://huggingface.co/datasets/InternRobotics/VLAC-Cut-Benchmark
- Model: https://huggingface.co/InternRobotics/VLAC-Cut
- Code: https://github.com/InternRobotics/VLAC-cut

## Download

Download only the README, processing scripts and the four test splits (without the roughly 951 GB raw archive):

```bash
hf download InternRobotics/VLAC-Cut-FullData \
  --repo-type dataset \
  --include "README.md" "scripts/*" "benchmark_style_all/test_*/*" \
  --local-dir ../datasets/VLAC-Cut-FullData-eval
```

Download the full release (about 956 GB; unpacking needs additional space):

```bash
hf download InternRobotics/VLAC-Cut-FullData \
  --repo-type dataset \
  --local-dir ../datasets/VLAC-Cut-FullData
```

After a full download, unpack and extract only the frames needed for a given evaluation JSON:

```bash
bash ../datasets/VLAC-Cut-FullData/scripts/unpack_data.sh \
  ../datasets/VLAC-Cut-FullData/raw

python ../datasets/VLAC-Cut-FullData/scripts/extract_vlac2_release_frames.py \
  --data-root ../datasets/VLAC-Cut-FullData/raw \
  --frames-root ../datasets/VLAC-Cut-FullData/frames \
  --benchmark-json ../datasets/VLAC-Cut-FullData/benchmark_style_all/test_nonexpert_seen/video_progress_benchmark_file.json
```

## Notes

- The 7 logical archives in `data/` comprise 22 files totaling about 950.7 GB; the HF repository's total `usedStorage` is about 956.1 GB.
- The `train` and `all` benchmark JSON files are themselves about 2.04 GB and 3.06 GB; downloading only the JSON is not necessarily lightweight.
- Standard use does not require rebuilding the benchmark JSON; the frame extraction script only decodes episodes actually referenced by the JSON passed in.
- The data card's license is only marked `other`; verify the specific license scope with the publisher before use.
- A spot check of `test_nonexpert_seen` found one anchor whose `human_annotated_progress` is `-20` while its `progress_explanation` says "dropped to 10%"; validate field consistency before using the data for training/evaluation.
