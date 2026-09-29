# Stage 3 — Launch Challenge

| Field | Value |
|---|---|
| **Window** | November 27–December 15, 2026 |
| **Duration** | 20 days |
| **Slogan** | Bring Your Robot to Life |
| **Hardware baseline** | RDK X5 plus the sensors and actuators defined in Stage 2 |

## Core Objective

Deliver a working, demonstrable, and shareable AI or robotics project with integrated hardware, ROS 2 communication, BPU-accelerated real-time inference, and reproducible documentation.

## Challenge 1 — Prototype Integration

Integrate:

- One or more AI models running on the board.
- ROS 2 communication between the relevant modules.
- Motor or actuator control with documented safety limits when applicable.
- Sensor fusion or a documented multi-sensor timing approach.

Provide a Quick Start with clone, build, launch, stop, and recovery commands. Document an emergency stop or safe shutdown whenever physical motion is involved.

## Challenge 2 — Real-Time AI Inference

The demo must show:

- BPU acceleration for at least one significant model.
- Continuous real-time inference rather than a single-frame run.
- Two concurrent workloads, such as detection plus tracking or speech recognition plus UI update.
- A benchmark table with model, input size, FPS or latency, and relevant CPU/BPU notes.

## Challenge 3 — Final Demo and Packaging

Prepare:

- A public demo video.
- A public GitHub repository with a clear README and license.
- Technical documentation covering architecture, interfaces, calibration, known issues, and failure recovery.
- A live or recorded walkthrough as announced by the organizers.

## Required Deliverables

| # | Item | Requirement |
|---|---|---|
| 1 | Demo video | 3–7 minutes; 1080p preferred; show the hardware, visible output, and at least 30 seconds of continuous AI operation |
| 2 | Source repository | Public; reproducible setup and launch; dependency versions pinned where practical |
| 3 | Technical documentation | Architecture, interfaces, calibration, safety, known issues, and recovery |
| 4 | Benchmark evidence | Model/runtime name plus BPU-path proof and measured performance |
| 5 | Community post | Final announcement with stable links |
| 6 | Showcase PR | Final project profile under `projects/` linking every required artifact |

Final submissions close **December 15, 2026**. Keep every link accessible through the judging period.

## Completion Reward

- RDK Creator title and Discord identity.
- USD 150, e-certificate, physical Robotics Dream Keeper medal, and official exposure, subject to final eligibility terms.
- Eligibility for TOP Creator judging.

## References

- [RDK course demos](https://github.com/D-Robotics/rdk-course-demos)
- [RDK Model Zoo](https://github.com/D-Robotics/rdk_model_zoo)
