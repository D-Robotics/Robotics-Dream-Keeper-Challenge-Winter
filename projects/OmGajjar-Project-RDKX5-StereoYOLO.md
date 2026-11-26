# Parallax: stereo hardware-in-the-loop for the RDK X5

- **Participant:** Om Gajjar
- **Stage completed:** 2
- **Repository:** <https://github.com/omgajjar1976/rdk-x5-parallax>
- **Demo evidence:** screenshots and photos, https://github.com/omgajjar1976/rdk-x5-parallax/tree/main/docs/images
- **Community post:** Stage 2: https://discord.com/channels/1300358874280230994/1574712116047515648/1575452279417344141 · Stage 1: https://discord.com/channels/1300358874280230994/1574712116047515648/1575423831630286938
- **License:** Apache-2.0

## Summary

Most demos run YOLO on one camera and stop at a box. In Stage 1 every detection on my RDK X5 got a distance in metres:
YOLO11m runs on the BPU, and my ROS 2 node matches each box in the rectified right image of the GS130W, using the
camera's factory calibration (baseline 80.02 mm read from its EEPROM). Checked with a tape measure: 60 cm reads 60.9 cm
(+1.5 %). I found ten problems in the stock stack and opened two upstream PRs and one issue.

Stage 2 designs **Stereo HIL**. A laptop runs Webots with SUMO traffic and pedestrians and sends the board a rendered
stereo pair with the GS130W's baseline. The RDK X5 runs YOLO11m and StereoNet on the BPU, decides (adaptive cruise,
emergency brake) and drives the simulated car with Ackermann commands. Because the simulator knows the exact depth of
every pixel, every depth estimate and every brake decision is scored automatically: depth error by range, stopping gap,
collisions and latency. The real GS130W stays in the loop for tape-measure runs. The simulator worlds, the ROS 2 bridge
with a 0.5 s brake watchdog, Humble↔Jazzy messaging and a pixel-exact depth checker are already built; Stage 3 puts the
board in the loop against seven measurable targets.

## Technical Highlights

- **RDK board / image:** RDK X5 4 GB, RDK OS 3.5.0, tros-humble 2.5.2
- **AI model and runtime:** YOLO11m (Bayes-e, 640x640 NV12) on the BPU via `hbm_runtime`; StereoNet on the BPU as the second workload (Stage 3)
- **Sensors and actuators:** RDK Stereo Camera GS130W on both MIPI CSI ports (real-world runs); simulated stereo + simulated car (Ackermann, ≤ 30 km/h) for HIL
- **ROS 2 design:** `ros_bridge` (laptop) → `hil_input` → `stereo_yolo` + StereoNet → `planner` → `safety` → `/hil/cmd_drive`; ground truth goes only to the laptop scorer
- **BPU evidence and performance:** YOLO11m 40.5 ms on the BPU (`hrt_model_exec`); live pipeline 5.4–6.2 fps today, Stage 3 target ≥ 10 Hz and ≤ 150 ms image-to-command

## Architecture

![Stereo HIL data flow](https://github.com/omgajjar1976/rdk-x5-parallax/raw/main/docs/figures/hil_architecture_light.svg)

Full ROS 2 graph with message types and rates: [ARCHITECTURE.md](https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/stage2/ARCHITECTURE.md)

## Links and Evidence

- Stage 2 proposal (scenario, users, innovation, 7 targets): https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/stage2/PROPOSAL.md
- Architecture (data flow, modules and failure modes, compute allocation, ROS 2 graph): https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/stage2/ARCHITECTURE.md
- Engineering plan (BOM, top five risks, repository structure): https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/stage2/ENGINEERING_PLAN.md
- Roadmap: https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/ROADMAP.md
- Stage 1 evidence: flash + SSH https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/images/01_flash_ssh_rdkos_info.png · sensor https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/images/02_camera_init_rate_internet.png · AI with distance https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/docs/images/04_ai_bottle_30cm.jpg
- Benchmarks and accuracy: https://github.com/omgajjar1976/rdk-x5-parallax#results
- Stock-stack issues and upstream PRs: https://github.com/omgajjar1976/rdk-x5-parallax/blob/main/UPSTREAM_ISSUES.md

## Known Limitations and Safety

Stage 1 accuracy is measured up to 60 cm; transparent and textureless objects give fewer stereo matches; the Python node
runs at 5–6 fps (C++ zero-copy planned). In Stage 3 only the simulated car moves: speed and steering are clamped, the
board has an e-stop topic, and the bridge brakes fully if no command arrives for 0.5 s.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
