# AURA-X5: Embodied Proactive Desktop AI Co-Pilot

- **Participant:** 147qaz258-ead
- **Stage completed:** Stage 1 — Ignite; Stage 2 — Build (`2`)
- **Repository:** https://github.com/147qaz258-ead/AURA-X5
- **Demo video:** Stage 1 live board evidence and Stage 2 complete design documents are linked below; the 3–7 minute 1080p full-system demo video comes with Stage 3.
- **Community post:** https://discord.com/channels/1300358874280230994/1569684675004334110
- **License:** MIT

## Summary

AURA-X5 is a desktop embodied proactive AI co-pilot powered by the **D-Robotics RDK X5 (10 TOPS BPU)**, designed for developers and engineers who want continuous workspace assistance without sacrificing host compute, focus, or hardware privacy. Software-only desktop agents consume host GPU/CPU for vision, disrupt workflow with pop-ups, and inject simulated keystrokes without a physical emergency stop. AURA-X5 moves visual perception, multi-sensor presence detection, and safety gating onto an external 15-degree desktop console tethered to the workstation over USB-C and ROS 2. On the host side, a validated 12 FPS screen-change observer filters idle frames and streams compact desktop context to the RDK X5. On the board, a four-node ROS 2 graph coordinates continuous `hbm_runtime` BPU inference, desk presence and environmental telemetry (HLK-LD2410C mmWave radar, SHT40, VL53L1X, INA219, ES8326 I2S mic), a non-intrusive secondary display (60 FPS HDMI kiosk UI or 3.5-inch SPI touchscreen), and a strict hardware safety gate. Crucially, no USB-C HID keyboard/mouse macro can execute without explicit physical confirmation via the EC11 rotary encoder or local panel, a dedicated Kill-Switch aborts active queues and releases all HID keys in under 50 ms, and a DPDT toggle physically severs the 3.3V power rail to the microphone and camera. Stage 1 verified live RDK OS 3.5.0 SSH/RDK Studio bring-up, ES8326 I2S microphone capture, and on-device YOLO11n BPU detection; Stage 2 delivers the full ROS 2 package, DRC-clean custom KiCad HAT, watertight 3D STLs, and solderless HDMI build path.

## Technical Highlights

- **RDK board / image:** D-Robotics RDK X5 (`RDK OS 3.5.0`, `Ubuntu 22.04.5 LTS`, `Linux 6.1.83 aarch64`, TogetherROS / ROS 2 Humble), verified online in RDK Studio and SSH.
- **AI model and runtime:** `hbm_runtime 1.24.5` (`HBRT 3.15.55.0`, `BPU Platform 1.3.6`) verified on-device with **YOLO11n** (`yolo11n_detect_bayese_640x640_nv12.bin`, `bpu_cores: [0]`), extensible to tiled 640×640 PP-OCRv5 with strict fail-fast enforcement (zero silent CPU fallback).
- **Sensors and actuators:** Verified on-board ES8326 I2S microphone (`plughw:1,0`, 16 kHz capture), SPI/I2C/UART/USB interfaces; planned Stage 3 integration with HLK-LD2410C 24 GHz mmWave radar (UART `/dev/ttyS1`), SHT40/VL53L1X/INA219 (I2C-5), EC11 rotary encoder, hardware Kill-Switch (GPIO Pin 7), DPDT privacy switch (`V_PRIVACY_3V3` + Pin 29), USB-C OTG Composite HID (`/dev/hidg0`/`/dev/hidg1`), 60 FPS HDMI / 3.5" SPI UI, WS2812B ring, and 5V PWM cooling fan.
- **ROS 2 design:** Four-node ROS 2 Humble package (`aura_x5_ros`: `aura_sensor_node`, `aura_bpu_perception_node`, `aura_safety_gate_node`, `aura_actuator_ui_bridge_node`) with unified launch (`aura_x5.launch.py`), typed JSON/Bool topics, `/aura/reset_kill_latch` recovery service, and timestamp-synchronized multi-sensor correlation.
- **BPU evidence and performance:** Verified Stage 1 YOLO11n BPU detection on live RDK X5 (`03_first_ai_yolo11_bpu.png` + `yolo11_bpu_run.log`), host 12.00 FPS / 0.00% drop 20-minute capture baseline, 90-line controlled 4K OCR tiling study for 640×640 BPU input, DRC=0 custom PCB (`electronics/validation.json`), and automated ≥35s continuous concurrent BPU benchmark harness (`scripts/benchmark_bpu_concurrent.py`) prepared for Stage 3 measurement.

## Architecture

```mermaid
flowchart LR
  PC["Host PC Observer\n(Screen Diff + Window Context)"] -->|"USB-C ECM / WS :8765"| UI["/aura_actuator_ui_bridge_node\n(HDMI 60FPS / 3.5in SPI + USB HID)"]
  UI -->|"/aura/desktop_frame"| BPU["/aura_bpu_perception_node\n(10 TOPS Bayes BPU hbm_runtime)"]
  SENS["/aura_sensor_node\n(Radar + I2C + I2S Mic + EC11 + Kill-Switch + DPDT)"] -->|"/aura/radar_presence & /aura/kill_switch"| GATE["/aura_safety_gate_node\n(Physical-Only Approval Gate)"]
  BPU -->|"/aura/perception_result"| GATE
  GATE -->|"Physical Approval Only: /aura/hid_command"| UI
  UI -->|"Hardware USB-C HID (/dev/hidg0)"| PC
```

Full module responsibilities, failure modes, compute allocation, and ROS 2 topic/service rates are documented in [docs/ARCHITECTURE.md](https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ARCHITECTURE.md).

## Links and Evidence

### Stage 1 — Ignite Evidence (Verified on Live RDK X5, 2026-11-24)
- Stage 1 full report: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/STAGE1_IGNITE.md
- Flash + RDK Studio + SSH & internet screenshot: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/evidence/stage1/01_flash_and_ssh.png
- Sensor / ES8326 I2S microphone waveform & hardware interfaces: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/evidence/stage1/02_sensor_mic_i2s.png
- On-device YOLO11n BPU object detection output & runtime log: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/evidence/stage1/03_first_ai_yolo11_bpu.png
- Raw BPU runtime log: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/evidence/stage1/yolo11_bpu_run.log

### Stage 2 — Build Deliverables
- Stage 2 Proposal (concept, users, innovation, measurable targets): https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/PROPOSAL.md
- Stage 2 Architecture (data-flow, modules, compute plan, ROS 2 graph): https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ARCHITECTURE.md
- Stage 2 Engineering Plan (full BOM, schedule, top-5 risks, repo layout): https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ENGINEERING_PLAN.md
- Public Project Roadmap: https://github.com/147qaz258-ead/AURA-X5/blob/main/ROADMAP.md
- ROS 2 Package (`aura_x5_ros` + launch + params): https://github.com/147qaz258-ead/AURA-X5/tree/main/ros2_ws/src/aura_x5_ros
- Stage 3 Benchmarks & Safety Manual: https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/BENCHMARKS_AND_SAFETY.md
- Custom KiCad PCB (0 DRC errors, Gerber & BOM) + Watertight 3D STLs: https://github.com/147qaz258-ead/AURA-X5/tree/main/electronics

## Known Limitations and Safety

- **Actuator Safety:** Because AURA-X5 injects real USB-C HID keyboard/mouse events via `/dev/hidg0`, all automated software/remote approval paths are rejected (`PermissionError`). Only explicit local physical confirmation triggers actuation, and pressing the hardware Kill-Switch (`GPIO Pin 7`) latches the safety gate, aborts all pending macros, and immediately writes an 8-byte all-zero HID release packet (`0x00 * 8`) to prevent stuck modifier keys.
- **Privacy Guarantee:** Flipping the front-panel DPDT switch physically disconnects the 3.3V supply (`V_PRIVACY_3V3`) to the microphone/camera rail independently of OS or software state.
- **Next Stage (Stage 3):** Continuous ≥30s concurrent BPU benchmarks (`scripts/benchmark_bpu_concurrent.py`), live ROS 2 `rqt_graph` integration, 8-step physical HIL logs (`verification/physical_test_plan.csv`), and the 3–7 min 1080p demo video will be added before December 15, 2026.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
