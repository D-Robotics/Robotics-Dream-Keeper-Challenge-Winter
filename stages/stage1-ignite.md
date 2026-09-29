# Stage 1 — Ignite Challenge

| Field | Value |
|---|---|
| **Window** | November 1–10, 2026 |
| **Duration** | 10 days |
| **Slogan** | Power On Your AI Robot's Brain |
| **Hardware baseline** | D-Robotics RDK X5 |

## Core Objective

Go from first contact with RDK X5 to independently running an on-device AI task: flash, connect, log in, activate a sensor, and run a visible AI workload.

## Challenge 1 — Board Bring-Up

Complete the following in order and preserve evidence:

1. Flash a supported RDK X5 system image with RDK Studio or an officially documented equivalent.
2. Boot successfully and connect through Ethernet or Wi-Fi.
3. Open an SSH session from a development computer to the board.
4. Join the official challenge community and post the Stage 1 check-in in your personal Discord thread.

**Completion standard:** the board boots normally, reaches the internet, accepts SSH commands, and has a shareable community check-in link.

## Challenge 2 — Sensor Explorer

Successfully read or drive at least one supported category:

- Camera
- IMU
- GPIO
- Microphone
- Motor or actuator

**Completion standard:** provide a short log, photo, or video showing the device response and name the interface used, such as MIPI, USB, I2C, GPIO, or a ROS 2 node.

## Challenge 3 — First AI Task

Run exactly one visible on-device workload:

- YOLO object detection
- Image classification
- Face recognition
- Speech recognition

You may start from [rdk-course-demos](https://github.com/D-Robotics/rdk-course-demos), [rdk_model_zoo](https://github.com/D-Robotics/rdk_model_zoo), or official documentation, but the submitted evidence must show your own board and run.

## Required Deliverables

| # | Item | Requirement |
|---|---|---|
| 1 | Flash + SSH evidence | Legible screenshot or composite showing successful flash and an active SSH session |
| 2 | Sensor evidence | Photo, screenshot, or short clip showing the sensor or actuator working |
| 3 | AI evidence | Screenshot showing the selected AI task running on the RDK X5 |
| 4 | Personal GitHub repository | README with setup, commands, dependencies, and troubleshooting notes |
| 5 | Community post | Permalink to the participant's Stage 1 update |
| 6 | Showcase PR | Project showcase file under this repository's `projects/` directory |

Do not publish Wi-Fi passwords, tokens, private keys, or device serials.

## Completion Reward

- RDK Explorer title and Discord identity.
- Stage 2 access.
- Official recognition.
- One participant T-shirt, subject to final shipping terms.

## Previous Season Reference

- [2026 Summer Stage 1 requirements](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge/blob/develop/stages/stage1-ignite.md)
- [2026 Summer project wall](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge/blob/develop/SHOWCASE.md) — useful examples of bring-up evidence, first AI tasks, and project documentation

Use these for inspiration only; submit against the Winter requirements above.
