# RDK X5 Quick Guide

This guide maps the minimum practical skills to the three challenge stages. Follow the linked official repositories and documentation for the exact commands that match your current RDK X5 system image.

## Official Starting Points

- [RDK course demos](https://github.com/D-Robotics/rdk-course-demos) — guided examples and course material required by the Winter program plan.
- [RDK Model Zoo](https://github.com/D-Robotics/rdk_model_zoo) — model and inference examples.
- [RDK Studio](https://developer.d-robotics.cc/en/rdkstudio) — image flashing and board setup.
- [D-Robotics documentation](https://developer.d-robotics.cc/en/documentation) — platform documentation.
- [D-Robotics GitHub organization](https://github.com/D-Robotics) — official source repositories.

## Stage 1 — Bring-Up and First AI Task

### Flash and First Boot

1. Install the current RDK Studio release on the development computer.
2. Select a supported RDK X5 system image from the official source.
3. Connect power and the documented flash/debug interface.
4. Flash the image, wait for verification, and reboot.
5. Preserve a legible screenshot showing the successful result.

### Network and SSH

Use the address assigned to your board:

```bash
ping <board-ip>
ssh <user>@<board-ip>
```

After login, record the image and kernel information used by the project:

```bash
uname -a
cat /etc/os-release
```

### Sensor Sanity Check

Exact commands depend on the image, driver, and sensor. For a V4L2 camera, a useful first check may be:

```bash
ls /dev/video*
v4l2-ctl --list-devices
```

Use the corresponding official demo or ROS 2 driver for your device, then capture visible evidence.

### First AI Demo

Choose an example from `rdk-course-demos`, `rdk_model_zoo`, or the official documentation. Record:

- Exact repository and commit or release.
- Model name and input size.
- Setup and run commands.
- Screenshot of the visible on-device result.

## Stage 2 — Architecture on RDK Constraints

Your design should state:

- Which models run on the BPU and which logic runs on the CPU.
- Sensor resolutions and target rates.
- ROS 2 nodes, topics/services/actions, message types, and QoS choices.
- Power, thermal, memory, and latency assumptions.
- Failure modes and a safe fallback for every actuator path.

## Stage 3 — Performance and Reliability

Measure the project in the state shown in the final demo:

| Field | Example value |
|---|---|
| Model and runtime | `<model / runtime>` |
| Input resolution | `<width x height>` |
| End-to-end latency | `<ms>` |
| Throughput | `<FPS or Hz>` |
| Concurrent workloads | `<task A + task B>` |
| CPU / BPU notes | `<measured observation>` |
| Thermal condition | `<fan / ambient / duration>` |

Do not report desktop-only performance as RDK X5 performance. Explain the measurement method and capture logs where practical.

## Evidence Checklist

- System image and software versions.
- Exact launch command.
- Visible AI output.
- Sensor or actuator proof.
- Benchmark log or table.
- Safety and failure-recovery notes.
- Stable public links with no secrets.

For submission help, see [github-pr-guide.md](./github-pr-guide.md) and [faq.md](./faq.md).
