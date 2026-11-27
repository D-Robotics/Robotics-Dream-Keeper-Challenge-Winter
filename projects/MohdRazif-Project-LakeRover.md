# LakeRover — AI Lake Sampling Rover on RDK X5

- **Participant:** Mohd Razif (Cikgu Siber, EDUCOGATOR)
- **Stage completed:** 2
- **Repository:** <https://github.com/educogator/lakerover-rdk>
- **Demo video:** Stage 1 evidence screenshots (see Links and Evidence below)
- **Community post:** <https://discord.com/channels/1300358874280230994/1566252507787698276>
- **License:** MIT

## Summary

Freshwater pollution increasingly threatens Malaysian lakes and reservoirs, yet location-specific pollution data is scarce. Most local studies report concentrations at a few fixed stations, which makes it hard to pinpoint hotspots, compare dry and wet seasons, or decide where to act.

LakeRover is an autonomous water-sampling rover designed as R&D for quality of life, aligned with SDG 6 (Clean Water) and SDG 14 (Life Below Water). The D-Robotics RDK X5 is the rover's brain: the RDK Stereo Camera and BPU-accelerated models give it obstacle awareness and floating-debris detection, while ROS 2 links perception and mission logic to a real-time controller for motors and failsafe. At each station the rover collects geotagged samples and sensor readings, so laboratory results finally come with a map, and repeatable survey routes make long-term monitoring possible.

Stage 1 result: I flashed RDKOS 3.5.0 Desktop with RDK Studio, connected the board over Wi-Fi, and worked over SSH from my Mac. Both stereo camera sensors were detected over MIPI CSI, StereoNet depth ran at about 16 FPS on the BPU, and YOLO object detection ran live on my own board, correctly detecting a phone, a remote and scissors. Along the way I solved three real setup issues (in-board flashing mode, USB networking on macOS, and ROS 2 log-directory permissions) and documented them in the README.

Stage 2 result: I designed the full system and published the deliverables: a proposal with measurable goals, a system architecture (module table, compute allocation and ROS 2 graph), an engineering plan (bill of materials, schedule, risks and repository structure), a roadmap, and a UART protocol specification between the RDK X5 and the controller. I also modelled the dream product and a full-scale prototype in 3D, with power and signal schematics for the build. The prototype adds a sampling system: a motorised 1 m tube is lowered into the water and a pump fills a sample bottle.

## Technical Highlights

- **RDK board / image:** RDK X5 8GB, RDKOS 3.5.0 Desktop (Ubuntu 22.04, Linux 6.1.83 aarch64)
- **AI model and runtime:** StereoNet v2.1 (`hobot_stereonet` 2.5.5); YOLOv2 via `dnn_node_example` 2.6.1; TogetheROS.Bot Humble
- **Sensors and actuators:** RDK Stereo Camera (dual SC230AI) on both MIPI CSI ports, verified with `i2cdetect` (0x30 on bus 4, 0x32 on bus 6). Stage 2 design adds two thrusters, a sampling pump, a flow sensor, a pH probe, a GPS module and a tube reel motor, all driven through a Raspberry Pi Pico 2; they are built in Stage 3.
- **ROS 2 design:** Stage 1 uses the official `mipi_cam` → `hobot_stereonet` / `dnn_node_example` → `websocket` pipeline. The LakeRover node graph is designed in Stage 2 (see the architecture document).
- **Compute allocation:** the RDK X5 runs perception and mission logic; the Pico 2 runs real-time control and owns every failsafe, over a documented UART protocol.
- **BPU evidence and performance:** StereoNet 640×352 at 15.98 FPS with BPU at 100% and SoC at 64.5 °C; YOLO camera stream at 30 FPS, SoC 65.8 °C

## Architecture

The prototype splits the work between two processors. The RDK X5 handles vision and mission logic. A Raspberry Pi Pico 2 on a Cytron Robo Pico handles motors, the pump and the failsafes (lost RC link, lost RDK X5 link, emergency stop, low battery, pump no-flow), connected to the RDK X5 over UART. Power comes from a 12.8V 24Ah LiFePO4 battery, with fuses per circuit and a small solar panel as a proof of concept.

An ArduPilot-based design with MAVLink, 4G and LoRa telemetry and isolated water-quality probes is a future extension, described in the full architecture document. The system diagram, module table, compute allocation and ROS 2 graph are in the Stage 2 architecture document linked below.

## Links and Evidence

- Stage 2 deliverables:
  - Roadmap: <https://github.com/educogator/lakerover-rdk/blob/main/ROADMAP.md>
  - Proposal: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage2/PROPOSAL.md>
  - Architecture: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage2/ARCHITECTURE.md>
  - Full architecture (future extension): <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage2/ARCHITECTURE_FULL.md>
  - Engineering plan: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage2/ENGINEERING_PLAN.md>
  - 3D design: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage2/DESIGN_3D.md>
  - UART protocol: <https://github.com/educogator/lakerover-rdk/blob/main/docs/PROTOCOL.md>
- Stage 1 evidence:
  - Flash: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage1/01-flash-success.png>
  - SSH session: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage1/02-ssh-session.png>
  - Stereo camera I2C check: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage1/03-camera-i2c.png>
  - Stereo depth (MIPI CSI, BPU): <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage1/04-stereo-depth.png>
  - YOLO object detection: <https://github.com/educogator/lakerover-rdk/blob/main/docs/stage1/05-yolo-web.png>
- Benchmarks: Stage 1 baseline table in the [README](https://github.com/educogator/lakerover-rdk#stage-1--ignite)
- Documentation: setup, commands, dependencies and troubleshooting in the [README](https://github.com/educogator/lakerover-rdk)

## Known Limitations and Safety

- Stage 1 ran on a 5.1V/3A supply; a 5V/5A supply is planned for full AI load and Stage 3 benchmarks.
- Stereo depth on a reflective water surface is unreliable; the camera is intended for objects above the water.
- No motion yet: the prototype is designed and modelled, and is built in Stage 3. The rover will have RC manual override, controller failsafes and a documented emergency stop.
- The 3D component models are approximations generated from photographs; real dimensions are measured on the physical parts before building.
- Still to confirm on hardware: the tube reel motor's stall current, the solar charge controller's lithium setting and the GPS serial adapter.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
