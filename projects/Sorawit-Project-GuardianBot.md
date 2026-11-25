# GuardianBot

- **Participant:** Sorawit Namwongsa
- **Stage completed:** 1 (RDK Explorer) · **Current submission:** Stage 2 — Build
- **Source repository:** [GuardianBot on GitHub](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter)
- **Demo evidence:** [Stage 1 USB camera and YOLOv8n evidence](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/stages/state%201/STAGE1_IGNITE.md) · [Stage 2 architecture and design evidence](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/stage2/ARCHITECTURE.md)
- **Community post:** [Stage 2 Build update on Discord](https://discord.com/channels/1300358874280230994/1569703774304608317/1575211015329550439)
- **Source license:** No license file is currently declared in the participant repository.

## Summary

GuardianBot is a planned indoor inspection robot for household members and caregivers who want to see areas outside the view of a fixed camera. The baseline demo lets a nearby operator guide a MasterPi chassis at low speed. The D-Robotics RDK X5 is planned to run YOLO detection on its BPU and track detected objects on its CPU. When a configured event is detected, the robot saves a timestamped snapshot locally. A front range sensor supports a controlled forward stop.

In Stage 1, I tested a USB camera and ran YOLOv8n object detection on the RDK X5. For Stage 2, I documented the operating scenario, measurable goals, ROS 2 interfaces, hardware inventory, risks, and roadmap. The planned Raspberry Pi and TurboPi expansion board interface handles chassis control and range sensing. Stage 3 will validate that link, measure BPU performance, and test safe stopping. Autonomous waypoint patrol, arm-based camera adjustment, and dashboard alerts are optional extensions.

## Technical Highlights

- **RDK board and runtime:** D-Robotics RDK X5 with D-Robotics Ubuntu 22.04 in Stage 1. USB camera input via V4L2 and YOLOv8n running on CPU were demonstrated.
- **Stage 2 design:** Quantized YOLO on the RDK X5 BPU, CPU tracking and motion supervision over ROS 2, and local event evidence.
- **Chassis hardware:** Four Mecanum wheels, Raspberry Pi with a TurboPi-marked expansion board, and a front ultrasonic module. Exact revisions and the chassis link are pending verification.
- **BPU performance:** Stage 3 will record the model, runtime, and measured FPS or latency. Stage 1 evidence demonstrates the CPU path.

## Architecture

See the [data flow and ROS 2 graph](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/stage2/ARCHITECTURE.md). The planned command path runs from the RDK X5 motion supervisor through the Raspberry Pi chassis host to the TurboPi expansion board. The physical motor stop is designed to act independently of the RDK X5 software.

## Links and Evidence

- [Stage 1 report and evidence](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/stages/state%201/STAGE1_IGNITE.md)
- [Stage 2 project proposal and measurable goals](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/stage2/PROJECT_PROPOSAL.md)
- [Stage 2 architecture and ROS 2 design](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/stage2/ARCHITECTURE.md)
- [Stage 2 engineering plan, BOM, and risks](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/docs/stage2/ENGINEERING_PLAN.md)
- [Roadmap through the final demo](https://github.com/Sorawit-2005/Robotics-Dream-Keeper-Challenge-Winter/blob/main/ROADMAP.md)
- [Stage 2 Discord message](https://discord.com/channels/1300358874280230994/1569703774304608317/1575211015329550439)

## Known Limitations and Safety

The Stage 2 documents describe the proposed design. The exact Raspberry Pi and expansion board revisions, power performance under load, and RDK-to-chassis communication require validation. Floor tests follow bench validation of command timeout and an independent motor stop. The range sensor covers the forward approach. Lateral and reverse motion will be tested separately in a cleared area.

---

I give the Robotics Dream Keeper Challenge organizers permission to use this Showcase document for competition promotion, judging, and program archives as described in the official README.
