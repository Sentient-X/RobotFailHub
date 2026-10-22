# Guardian FailCoT / RoboFail

| Field | Value |
| --- | --- |
| **Date** | 2025-12 (Guardian) / 2023-11 (RoboFail) |
| **Paper** | [Guardian / FailCoT (2512.01946)](https://arxiv.org/abs/2512.01946) · [REFLECT / RoboFail (2306.15724)](https://arxiv.org/abs/2306.15724) |
| **Domain** | Robot / Sim + Real |
| **Modality** | multi-view image, language, CoT failure reasoning |
| **Size** | FailCoT **30,876 train** (RLBench 18,166 + BDV2 12,710 exec/plan samples); RoboFail **130 scenarios** (100 sim + 30 real) |
| **Progress Annotation** | No (mainly failure verification) |
| **Failure or Recovery Trajectory** | Yes — planning + execution success/failure with reasoning traces |
| **Subtask Annotation** | Yes — subtask-level execution/planning verification |
| **Failure Taxonomy** | Yes — planning vs execution; Guardian includes fine-grained categories |

## Description

**FailCoT** synthesizes planning/execution failures by perturbing successful trajectories and uses a VLM to generate step-by-step reasoning traces, training **Guardian**, a multi-view failure detector.

**RoboFail** (REFLECT, CoRL 2023) is a classic real-robot failure benchmark: 100 simulated failures in AI2THOR + 30 real teleoperated failures on a UR5e, with a failure taxonomy. Guardian re-exports it in a unified schema and uses it, together with UR5-Fail and RoboVQA, for OOD evaluation.

## Download

### Guardian / FailCoT (training + synthetic data)

- HF Collection: https://huggingface.co/collections/paulpacaud/robotic-failure-detection-dataset-and-model-guardian
- Model: https://huggingface.co/paulpacaud/guardian-thinking
- GitHub: https://github.com/paulpacaud/Guardian-FailCot
- Project page: https://www.di.ens.fr/willow/research/guardian/

### OOD evaluation bundle (includes RoboFail)

- https://huggingface.co/datasets/paulpacaud/Guardian-FailCoT-OOD-datasets
  - `robofail` — 153 execution + 30 planning samples (single view)
  - `ur5fail_test` — 140 + 140 (three views, new Guardian benchmark)
  - `robovqa` — 357 execution VQA

### RoboFail original data (REFLECT)

- Project page: https://robot-reflect.github.io/
- Data: https://www.cs.columbia.edu/~liuzeyi/reflect_data
- GitHub: https://github.com/real-stanford/reflect

## Notes

- PRIMO-R1 reports SOTA 67.0% accuracy on RoboFail (failure detection).
- FailCoT simulation source: RLBench → `rlbenchfail`; real sources: BridgeData V2 → `bdv2fail`, UR5 autonomous rollouts → `ur5fail`
