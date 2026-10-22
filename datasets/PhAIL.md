# PhAIL

| Field | Value |
| --- | --- |
| **Date** | 2026-05 |
| **Paper** | [PhAIL: A Real-Robot VLA Benchmark and Distributional Methodology](https://arxiv.org/abs/2605.29710) |
| **Domain** | Robot / Real |
| **Dataset Role** | evaluation rollout + benchmark-aligned demonstration |
| **R2 Classification** | R2-A — real policy evaluation artifacts have been published |
| **Modality** | synchronized multi-view video, robot state/action telemetry, task/config metadata, outcome and timing |
| **Size** | v1.0: 594 model evaluation runs; 352 VR-teleoperated fine-tuning demonstrations (about 12 GB) |
| **Progress Annotation** | Yes — run-level metrics such as completion, successful items, elapsed time and UPH |
| **Failure or Recovery Trajectory** | Yes — failed, timed-out and safety-stop evaluation runs are released in full; no corrective takeover action |
| **Subtask Annotation** | No — only per-item completion counts and run-level events |
| **Failure Taxonomy** | Yes (coarse-grained) — Success / Fail / Safety, with definitions of timeout and unrecoverable controller errors |
| **License** | To be verified — the official statement says the fine-tuning data uses a non-commercial license; the data license cannot be inferred from the Apache-2.0 code license |

## Description

PhAIL is a real-robot VLA evaluation run on a Franka Research 3, a Robotiq 2F-85 and two ZED cameras. v1.0 runs blind, randomized evaluations of OpenPI, GR00T, SmolVLA and ACT on bin-to-bin order picking of four kinds of objects.

The evaluation data is itself an auditable real rollout artifact: the official release publishes synchronized multi-camera video, robot state and action logs, scene configuration, timing, completion counts and outcome labels. The only intervention available to a human during a run is to trigger a safety stop and terminate the run, so it must not be labeled as a takeover dataset containing corrective actions after takeover.

## Official Sources

- Release v1.0: https://phail.ai/releases/v1.0
- Leaderboard / run explorer: https://phail.ai/
- Frozen v1.0 white paper: https://phail.ai/whitepaper.pdf
- Data: `s3://positronic-public/phail/v1.0/dataset/`
- Evaluation framework: https://github.com/Positronic-Robotics/positronic

## Download / Browse

```bash
uv run --with positronic positronic-server @positronic.cfg.phail.v1_0.ds.rollouts
```

Or install it and then browse:

```bash
pip install positronic
positronic-server @positronic.cfg.phail.v1_0.ds.rollouts
```

## Notes

- The frozen v1.0 release contains 594 model evaluation runs; the website's current total episode count grows as human, teleoperation and new evaluation results are added, and must not be mixed with the fixed release counts.
- The 352 fine-tuning demonstrations are benchmark-aligned training data, not model evaluation rollouts.
- A safety stop is a risk-intervention signal; it does not include a sequence of human corrective actions after the intervention.
