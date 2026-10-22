# RoboDojo Real-World Benchmark

| Field | Value |
| --- | --- |
| **Date** | 2026-07 |
| **Paper** | [RoboDojo: A Unified Sim-and-Real Benchmark for Comprehensive Evaluation of Generalist Robot Manipulation Policies](https://arxiv.org/abs/2607.04434) |
| **Domain** | Robot / Real + Sim (this card covers only the real benchmark) |
| **Dataset Role** | evaluation framework, task/config assets, result artifacts |
| **R2 Classification** | R2-B — real-robot benchmark and remote evaluation system; a public bulk real rollout dump is not confirmed |
| **Modality** | task/scene/robot/camera configs, policy result artifacts; real rollouts are produced by RealEval |
| **Size** | 18 real tasks, 3 embodiments; plus 42 simulation tasks |
| **Progress Annotation** | Yes (evaluation-result level) — task-specific score / leaderboard result |
| **Failure or Recovery Trajectory** | Existence of a bulk-downloadable complete real rollout dataset not confirmed |
| **Subtask Annotation** | Task configs and scoring rules are available; per-trajectory subtask annotation to be verified |
| **Failure Taxonomy** | No unified public taxonomy |
| **License** | Code MIT; a unified license for the data and remote real-robot result artifacts is to be verified |

## Description

RoboDojo unifies 42 Isaac Sim tasks and 18 real-robot tasks, and through RoboDojo-RealEval provides standard hardware, scene reset, an evaluation protocol and remote cloud evaluation. The real portion covers three embodiments: Piper X, Piper and ARX X5.

The official repository states clearly that the current release is `eval-only`: it opens the simulator client, benchmark tasks, asset/config validation and result artifacts, while policy integration/server is managed by XPolicyLab. This does not mean a complete bulk real rollout dump like RoboArena's has been released.

## Official Sources

- Project: https://robodojo-benchmark.com/
- Code: https://github.com/RoboDojo-Benchmark/RoboDojo
- Real task catalog: https://robodojo-benchmark.com/doc/real-tasks/
- Installation and assets: https://robodojo-benchmark.com/doc/usage/install-and-download/
- Paper: https://arxiv.org/abs/2607.04434

## Notes

- Worth monitoring for updates to real task definitions, camera/robot configs, the leaderboard and result artifacts.
- Until the official release states a real rollout partition, its size and license, do not mirror the mixed sim+real data sources wholesale.
- `eval-only` describes the scope of the software release; it does not mean "contains only public real evaluation trajectories".
