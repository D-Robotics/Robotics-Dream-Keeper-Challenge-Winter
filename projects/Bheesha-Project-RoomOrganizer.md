# RDK X5 Room Organizer

**Participant:** Bheesha Kumari  
**GitHub Username:** bheesha  
**Challenge:** Robotics Dream Keeper Winter 2026  
**Current Stage:** Stage 1 — Ignite (Completed)  
**Development Board:** D-Robotics RDK X5

## 1. Project Summary

RDK X5 Room Organizer is an intelligent mobile robotics project designed to help people organize cluttered living spaces.

The goal is to develop an autonomous mobile robot equipped with a robotic arm and computer vision capabilities. The robot will navigate indoor environments, identify misplaced household objects such as clothing and small personal belongings, pick them up, and place them into designated baskets or storage locations.


## 2. Stage 1 — Ignite Results

### Challenge 1: Board Bring-Up

**Status: Completed**

- Flashed RDKOS 3.5.0 Desktop (Ubuntu 22.04).
- Successfully booted the RDK X5.
- Established SSH communication from a MacBook using the USB-C network interface.
- Verified the system using `uname -a` and `cat /etc/os-release`.

### Challenge 2: Sensor Explorer

**Status: Completed**

- Interface: GPIO
- Library: Hobot.GPIO
- Connected physical GPIO pins 31 (output) and 37 (input) using a jumper wire.
- Implemented a Python loopback test using alternating HIGH and LOW signals.
- **Result: 4/4 tests passed.**

### Challenge 3: First AI Task

**Status: Completed**

- Task: Image classification
- Model: MobileNetV2
- Execution: RDK X5 BPU, core 0
- Input: Sample image provided with the official demo
- **Result: Zebra detected with 99.36% confidence.**

The inference completed successfully. A model-builder/runtime version warning was observed and documented.

## 3. Source Code and Evidence

**Public GitHub Repository:**

https://github.com/bheesha/RDK-X5-Room-Organizer

The repository includes:
- System flashing evidence
- SSH connection evidence
- GPIO test results and Python script
- MobileNetV2 AI inference screenshots
- Project README and technical setup documentation

## 4. Community Update

**Stage 1 Discord Post:**

https://discord.com/channels/1300358874280230994/1565929397658058862/1569942246512533604

## 5. Next Steps — Stage 2

The next stage will focus on:

- Designing the mobile robotic platform and arm.
- Selecting compatible cameras, motors, sensors, and controllers.
- Developing the ROS 2 architecture.
- Planning object detection, navigation, grasping, and sorting.
- Identifying a feasible technical contribution involving pickup verification and failure recovery.
- Establishing a development and testing roadmap for Stage 3.

## 6. Current Project Status

Stage 1 technical experiments are complete. The autonomous mobile robot remains a planned system and has not yet been built or demonstrated.

The project will advance through Stage 2 system design and Stage 3 prototype development.
