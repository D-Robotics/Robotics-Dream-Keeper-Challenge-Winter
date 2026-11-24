# AURA-X5: Embodied Proactive Desktop AI Co-Pilot

<!--
  OFFICIAL SHOWCASE SUBMISSION FILE (WAREHOUSE B)
  ===================================================================
  Before opening your Pull Request to:
    https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter

  1. Rename this file to match the mandatory naming rule:
       projects/<ParticipantName>-Project-AURA-X5.md
     (No spaces, no version suffixes like -v2 or -final.)
  2. Replace every <...> placeholder below with your real public URLs.
  3. Update "Stage completed" as you advance from 1 -> 2 -> 3.
  4. Delete this HTML comment block before committing.
-->

- **Participant:** `147qaz258-ead`
- **Stage completed:** `2` *(update to `3` upon Stage 3 completion)*
- **Repository:** `https://github.com/147qaz258-ead/AURA-X5`
- **Demo video:** `https://<YOUR_PUBLIC_DEMO_VIDEO_URL>`
- **Community post:** `https://discord.com/channels/<YOUR_DISCORD_THREAD_PERMALINK>`
- **License:** MIT

## Summary

AURA-X5 is a desktop embodied proactive AI co-pilot powered by the **D-Robotics RDK X5 (10 TOPS BPU)**, designed for developers and engineers who want continuous workspace assistance without sacrificing host compute, focus, or hardware privacy. Pure-software desktop agents consume host GPU/CPU for vision, disrupt workflow with pop-ups, and inject simulated keystrokes without a physical emergency stop. AURA-X5 moves visual perception, multi-sensor presence detection, and safety gating onto an external 15-degree desktop console tethered to the workstation over USB-C and ROS 2. On the host side, a validated 12 FPS screen-change observer filters idle frames and streams compact desktop context to the RDK X5. On the board, a ROS 2 node graph coordinates continuous `hbm_runtime` BPU inference, desk presence and environmental telemetry (HLK-LD2410C mmWave radar, SHT40, VL53L1X, INA219), a non-intrusive secondary display (60 FPS HDMI kiosk UI or 3.5-inch SPI touchscreen), and a strict hardware safety gate. Crucially, no USB-C HID keyboard/mouse macro can execute without explicit physical confirmation via the EC11 rotary encoder or touch panel, a dedicated Kill-Switch aborts active queues and releases all HID keys in under 50 ms, and a DPDT toggle physically severs the 3.3V power rail to the microphone and camera. We deliver both a DRC-clean custom KiCad carrier HAT with watertight 3D-printed enclosure files and a solderless HDMI + DuPont build path for rapid community replication.

## Technical Highlights

- **RDK board / image:** D-Robotics RDK X5 (Linux 6.1.83, Ubuntu 22.04 official RDK OS, TogetherROS / ROS 2 Humble).
- **AI model and runtime:** `hbm_runtime 1.24.5` (HBRT `3.15.55.0`) executing quantized INT8 `.bin`/`.hbm` models (`mobilenetv2_224x224_nv12.bin`, extensible to YOLOv8 / tiled 640×640 PP-OCRv5) on the 10 TOPS Bayes BPU with strict fail-fast enforcement (zero silent CPU fallback).
- **Sensors and actuators:** HLK-LD2410C 24 GHz mmWave presence radar (UART `/dev/ttyS1`), SHT40 / VL53L1X / INA219 (I2C-5), EC11 rotary encoder, hardware Kill-Switch (GPIO Pin 7), DPDT hardware privacy switch (`V_PRIVACY_3V3` + Pin 29 sense), USB-C OTG Composite Gadget (`/dev/hidg0` keyboard + `/dev/hidg1` mouse), 60 FPS HDMI UI / 3.5" ILI9486+XPT2046 SPI touchscreen, WS2812B RGB status ring, and 5V PWM cooling fan.
- **ROS 2 design:** Four-node ROS 2 Humble graph (`aura_sensor_node`, `aura_bpu_perception_node`, `aura_safety_gate_node`, `aura_actuator_ui_bridge_node`) with unified launch (`aura_x5.launch.py`), typed JSON/Bool topics, `/aura/reset_kill_latch` recovery service, and timestamp-synchronized multi-sensor correlation.
- **BPU evidence and performance:** Pre-verified `hbm_runtime` BPU bring-up on live RDK X5 (`scripts/test_bpu_on_rdk.py`), host 12.00 FPS / 0.00% drop 20-minute capture, DRC=0 custom PCB, and automated concurrent BPU benchmark harness (`scripts/benchmark_bpu_concurrent.py`) for Stage 3 continuous ≥30s metrics.

## Architecture

```mermaid
flowchart LR
  PC["Host PC Observer\n(Screen Diff + Window Context)"] -->|"USB-C ECM / WS :8765"| UI["/aura_actuator_ui_bridge_node\n(HDMI 60FPS / 3.5in SPI + USB HID)"]
  UI -->|"/aura/desktop_frame"| BPU["/aura_bpu_perception_node\n(10 TOPS Bayes BPU hbm_runtime)"]
  SENS["/aura_sensor_node\n(Radar + I2C + EC11 + Kill-Switch + DPDT)"] -->|"/aura/radar_presence & /aura/kill_switch"| GATE["/aura_safety_gate_node\n(Physical-Only Approval Gate)"]
  BPU -->|"/aura/perception_result"| GATE
  GATE -->|"Physical Approval Only: /aura/hid_command"| UI
  UI -->|"Hardware USB-C HID (/dev/hidg0)"| PC
```

Full module tables, compute allocation, ROS 2 topic rates, and data-flow specs are documented in [`docs/ARCHITECTURE.md`](https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ARCHITECTURE.md).

## Links and Evidence

- Stage 1 Ignite report & evidence: `https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/STAGE1_IGNITE.md`
- Stage 2 Proposal: `https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/PROPOSAL.md`
- Stage 2 Architecture & ROS 2 graph: `https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ARCHITECTURE.md`
- Stage 2 Engineering plan (BOM, schedule, risks): `https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/ENGINEERING_PLAN.md`
- Public roadmap: `https://github.com/147qaz258-ead/AURA-X5/blob/main/ROADMAP.md`
- Benchmarks & safety manual: `https://github.com/147qaz258-ead/AURA-X5/blob/main/docs/BENCHMARKS_AND_SAFETY.md`
- Hardware CAD / PCB manufacturing files: `https://github.com/147qaz258-ead/AURA-X5/tree/main/electronics`

## Known Limitations and Safety

- **Actuator Safety:** Because AURA-X5 injects real USB-C HID keyboard/mouse events via `/dev/hidg0`, all automated software/remote approval paths are rejected (`PermissionError`). Only explicit local physical approval triggers actuation, and pressing the hardware Kill-Switch (`GPIO Pin 7`) latches the safety gate, aborts all pending macros, and immediately writes an 8-byte all-zero HID release packet to prevent stuck keys.
- **Privacy Guarantee:** Flipping the front-panel DPDT switch physically disconnects the 3.3V supply (`V_PRIVACY_3V3`) to the microphone/camera rail independently of OS/software state.
- **Current Limitations:** Full Stage 3 continuous ≥30s concurrent BPU benchmarks and 8-step physical HIL test logs (`verification/physical_test_plan.csv`) are scheduled for completion during the Stage 3 window (Nov 27 – Dec 15, 2026) and will be linked in the Stage 3 update of this showcase file.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
