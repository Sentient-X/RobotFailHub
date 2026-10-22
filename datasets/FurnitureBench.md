# FurnitureBench

| Field | Value |
| --- | --- |
| **Date** | 2023-05 |
| **Paper** | [FurnitureBench: Reproducible Real-World Benchmark for Long-Horizon Complex Manipulation](https://arxiv.org/abs/2305.12821) |
| **Domain** | Robot / Real (FurnitureSim also available) |
| **Dataset Role** | benchmark-aligned successful demonstration |
| **R2 Classification** | R2-B — real-robot benchmark; the public data is mainly demonstrations |
| **Modality** | wrist/front RGB, EEF pose/velocity, joints, torque, gripper, 8-D action, reward, skill flags |
| **Size** | 5,100 successful demonstrations, 219.6 hours; raw PKL about 1,179 GB in total |
| **Progress Annotation** | Yes — assembly reward and skill-completion flags |
| **Failure or Recovery Trajectory** | No — the official public listing describes them as successful demonstrations |
| **Subtask Annotation** | Yes — skill completion flags |
| **Failure Taxonomy** | No |
| **License** | Data license to be verified; it cannot be inferred from the code repository license |

## Description

FurnitureBench is a real-robot long-horizon furniture assembly benchmark with 9 kinds of 3D-printed furniture and three levels of initialization randomness: low / medium / high. The public data consists of successful demonstrations collected by teleoperation with an Oculus Quest 2 and a keyboard, suitable for imitation learning, offline RL, and research on long-horizon progress and skill boundaries.

Each PKL trajectory stores wrist/front RGB, robot state, 8-D action, assembly reward and skill completion flags. Actually evaluating a candidate policy requires the physical Franka setup; the demonstration corpus must not be labeled as test rollouts.

## Official Sources

- Project: https://clvrai.github.io/furniture-bench/
- Dataset documentation: https://clvrai.github.io/furniture-bench/docs/tutorials/dataset.html
- Code: https://github.com/clvrai/furniture-bench
- Paper: https://arxiv.org/abs/2305.12821

## Download

```bash
python furniture_bench/scripts/download_dataset.py \
  --untar \
  --randomness low \
  --furniture lamp \
  --out_dir ../datasets/FurnitureBench
```

## Notes

- Raw PKL size: low 457 GB, medium 499 GB, high 223 GB.
- When the Google Drive quota is limited, the official docs provide an rclone download method.
- Download selectively by furniture and randomness.
