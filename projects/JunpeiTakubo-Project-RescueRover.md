# Rescue Rover — Retrieving Lost Items from Under Furniture

**Participant:** Junpei Takubo  
**Challenge:** Robotics Dream Keeper Challenge Winter 2026  
**Platform:** D-Robotics RDK X5  
**Current Stage:** Stage 2 — Build (Design in Progress)  
**Project Status:** Prototype Design / Hardware Validation Pending

## 1. Project Overview

**Tagline: Bringing lost items back from hard-to-reach spaces.**

Have you ever dropped your smartphone, cosmetics, or another small item under a bed or sofa, only to find it impossible to reach without moving the furniture?

**Rescue Rover** is a compact, low-profile mobile robot designed to retrieve everyday objects from narrow spaces beneath furniture.

The goal is to build a robot that can:

1. **Reach** — Enter low-clearance spaces under beds and sofas.
2. **Find** — Locate lost objects using onboard AI vision.
3. **Retrieve** — Grasp and bring objects back to an accessible location.

Unlike a conventional object-detection demo, Rescue Rover aims to connect AI perception with physical interaction to solve a practical household problem.

The project is currently in the design and prototyping phase. A complete autonomous retrieval demonstration has not yet been achieved.

---

## 2. Stage 1 — Ignite: Board Bring-Up and First AI Task

**Status: Initial Hardware and AI Tests Completed**

### Board Bring-Up

I flashed an official Ubuntu-based RDK X5 system image using RDK Studio and established SSH access from a MacBook Air M1 via USB Type-C.

One issue was configuring the USB virtual Ethernet interface on macOS.

The RDK X5 was recognized as `sunrise5`, but the host network interface did not initially have a working IPv4 configuration.

The issue was resolved by manually assigning an IP address:

```bash
sudo ifconfig en7 inet 192.168.128.100 netmask 255.255.255.0 up
ssh sunrise@192.168.128.10
```

The interface name `en7` is specific to this environment and may differ on other computers.

### Sensor Explorer — IMX219 MIPI Camera

**Hardware:** Sony IMX219  
**Interface:** MIPI CSI / I2C  
**Resolution:** 1920 × 1080

I connected an IMX219 camera to the RDK X5 and tested it with the official camera API.

The camera was successfully identified:

```text
Found sensor name: imx219-1920x1080-30fps
on mipi rx csi 0, i2c addr 0x10
```

This experiment also helped me understand how `hobot_vio`, native shared libraries, I2C sensor identification, and the MIPI CSI pipeline work together.

### First AI Task — YOLOv5s

I ran the official YOLOv5s object-detection sample using the RDK X5 BPU.

```bash
cd /app/pydev_demo/08_mipi_camera_sample
python3 01_mipi_camera_yolov5s.py
```

The camera and inference pipeline ran continuously at approximately 26–31 FPS.

```text
Frame#195 (30 fps)
Frame#255 (31 fps)
Frame#362 (27 fps)
Frame#421 (29 fps)
```

The sample reported a model/runtime version mismatch warning. Visual validation of detection accuracy and saved detection images is being prepared.

Because the board was accessed via SSH without a local display, the application ran without an on-screen preview.

### Stage 1 Evidence

- Public source repository: [TODO — GitHub URL]
- OS flashing and SSH screenshot: [TODO]
- IMX219 detection evidence: [TODO]
- YOLOv5s execution screenshot: [TODO]
- Stage 1 Discord submission: [TODO — Permalink]

---

## 3. Stage 2 — Build: Rescue Rover Design

**Status: Mechanical Design Prepared / System Integration Planned**

### 3.1 Problem and Target Users

Small items often fall into narrow spaces under furniture.

Retrieving them may require moving heavy furniture, kneeling, or reaching into dusty and difficult-to-access areas.

Rescue Rover aims to make retrieval easier for everyday users, particularly people who have difficulty bending or reaching into confined spaces.

**Initial target scenario:** Retrieving a smartphone from under a bed on a relatively flat floor.

Future target objects include small cosmetic items and remote controls, subject to successful grasping tests.

### 3.2 Mechanical Design — Rescue Rover v12

I have prepared a preliminary mechanical design using parametric CAD generation and 3D-printable components.

The current design includes:

- A compact chassis designed for low-clearance access
- A differential-drive mechanism
- Two drive servos
- A front, servo-actuated two-jaw gripper
- A gear-linked mechanism allowing both jaws to move using one servo
- A front-facing camera mount angled approximately 25 degrees downward
- 3D-printable chassis, wheel, gripper, and mounting components

**Actuators:** Feetech STS3215 × 3

- Servo ID 1: Left drive wheel
- Servo ID 2: Right drive wheel
- Servo ID 3: Gripper open/close mechanism

The gripper is inspired by the opposing jaws of a stag beetle.

Rather than lifting the object, the current design aims to hold it from both sides and drag it out of the confined space.

### 3.3 Gripper Design

The v12 CAD design uses a geared two-jaw mechanism.

Preliminary design parameters include:

- Jaw opening angle: 0–25 degrees
- Approximate inner jaw gap: 53–105 mm
- Target object: Smartphone approximately 75 mm wide
- Approximate jaw contact angle for the target object: 19.5 degrees
- Initial software grip-torque limit: 35% of the configured maximum

These are design and simulation parameters, not verified real-world grasping performance.

The current design requires physical tests to confirm gripping force, slip resistance, gear backlash, and clearance from the floor.

### 3.4 Preliminary Design Validation

The v12 package contains:

- STEP and STL mechanical models
- 3MF print-plate layouts
- Assembly and wiring documentation
- Servo-control Python code
- CAD interference and motion-check results
- Mock-bus software test results

The supplied design-validation records indicate that the jaw mechanism was checked across its planned motion range without modeled interference.

Real hardware testing remains necessary before treating the mechanism as validated.

### 3.5 Planned AI and ROS 2 Architecture

The proposed control pipeline is:

```text
IMX219 MIPI Camera
        |
        v
RDK X5 Camera / ISP Pipeline
        |
        v
BPU Object Detection
        |
        v
ROS 2 Perception Node
        |
        v
Target Localization / Decision Logic
        |
        v
ROS 2 Motion Controller
        |
        v
Feetech STS3215 Servo Interface
        |
        +-- Left Drive Motor
        +-- Right Drive Motor
        +-- Gripper
```

**Planned compute allocation:**

- **BPU:** Object detection
- **CPU:** Camera integration, ROS 2 communication, decision logic, and motion control
- **Motor bus interface:** Low-level servo commands and status monitoring

This architecture is proposed and has not yet been integrated end to end.

### 3.6 Engineering Roadmap

| Milestone | Goal | Status |
|---|---|---|
| 1 | RDK X5 setup and camera bring-up | Tested |
| 2 | YOLOv5s inference pipeline | Running; output validation pending |
| 3 | Mechanical CAD and gripper design | Prepared |
| 4 | 3D printing and assembly | Planned |
| 5 | Servo control on real hardware | Planned |
| 6 | ROS 2 perception and control integration | Planned |
| 7 | Smartphone retrieval demonstration | Planned |

### 3.7 Major Engineering Risks

| Risk | Mitigation |
|---|---|
| Insufficient clearance beneath furniture | Measure the assembled robot height and test with representative furniture gaps |
| Smartphone slipping out of the gripper | Tune torque and jaw shape; evaluate friction pads |
| Poor visibility in dark spaces | Evaluate lighting and camera exposure |
| Robot becoming stuck beneath furniture | Implement manual recovery and motion limits |
| Unsafe actuator behavior or communication loss | Implement watchdog handling, speed limits, and an independent emergency-stop strategy |

The existing mock-bus software tests provide an initial foundation for the motor-control implementation, but safety must be verified with actual hardware.

### 3.8 Stage 2 Deliverables

- Mechanical design and CAD files: [TODO — GitHub URL]
- Assembly and wiring documentation: [TODO]
- Robot concept and proposal: [TODO]
- System architecture and ROS 2 node design: [TODO]
- BOM and engineering plan: [TODO]
- Development roadmap: [TODO]
- Stage 2 Discord submission: [TODO — Permalink]

---

## 4. Stage 3 — Launch: Integrated Robot Demonstration

**Status: Planned / Not Yet Implemented**

The goal of Stage 3 is to demonstrate Rescue Rover retrieving an everyday object from beneath furniture.

### Planned Demo Scenario

1. Place a smartphone under a bed or similar low-clearance structure.
2. Drive Rescue Rover into the space.
3. Detect and locate the smartphone using onboard AI.
4. Approach the target using the mobile base.
5. Close the gripper around the smartphone.
6. Reverse out of the confined space while holding the object.
7. Return the smartphone to an accessible location.

### Planned Technical Validation

- ROS 2 integration and node-level testing
- Real-time BPU-accelerated inference
- Camera-to-control latency measurements
- Servo communication and emergency stopping
- Gripper success and failure testing
- Object retrieval success rate
- Continuous operation demonstration

### Stage 3 Evidence

- Final robot photographs: [TODO]
- Demo video: [TODO]
- ROS 2 source code: [TODO]
- Performance measurements: [TODO]
- Final Discord submission: [TODO]

---

## 5. Source Code and Resources

- **Public GitHub Repository:** [TODO]
- **Stage 1 Documentation:** [TODO]
- **Stage 2 Design and CAD:** [TODO]
- **Stage 3 Results:** [TODO]
- **Discord Project Thread:** [TODO]

## 6. Acknowledgments

Thanks to D-Robotics and the Robotics Dream Keeper Challenge community for providing the RDK X5 platform, technical documentation, and example applications.

This project is an ongoing hands-on exploration of how embedded AI can be translated into useful physical robotic systems.