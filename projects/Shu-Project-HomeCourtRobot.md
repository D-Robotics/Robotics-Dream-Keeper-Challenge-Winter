# Home Court Robot

- **Participant:** Shu
- **Stage completed:** 2 (Build design)
- **Repository:** [Home Court Robot](https://github.com/shoujiki-panman/rdk-x5-home-court-robot)
- **Demo evidence:** [Stage 1 BPU and USB camera evidence](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter/pull/5) · [Stage 2 design](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/docs/stage2/proposal.md)
- **Community post:** [Stage 2 update in Shu’s Discord challenge thread](https://discord.com/channels/1300358874280230994/1566820028366585957)
- **License:** [MIT License](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/LICENSE)

## Summary

Home Court Robot adds a walking judge and a camera that can recognize physical evidence to my existing Japanese parent–child game, おうち裁判. Two players tell their sides, explain what their evidence shows, and hear a verdict. In the tabletop design, they can show a real object when the game asks for evidence. RDK X5 recognizes the object locally and adds the confirmed observation to the existing case record. The players still explain how the object supports what they said.

When the game accepts the request for a verdict, a StackChan wearing a printed judge's robe and gavel enters on Yeq6X's four-legged Strider base. It takes a short walk during the existing deliberation. Speech and the gavel sound keep their usual order, independent of the success of the walk.

Stage 1 verified USB camera capture and official YOLO11n inference on the BPU. Stage 2 defines the two integration points, ROS 2 interfaces, compute allocation, and test targets. It includes printable costume CAD. Stage 3 will measure evidence recognition, movement timing, and complete two-player sessions.

## Technical Highlights

- **RDK board / image:** RDK X5, RDK OS 3.5.0.
- **AI model:** YOLO11n verified on BPU in Stage 1. Stage 3 will measure it on books and scissors in the evidence area.
- **Sensors and actuators:** Fixed C270 USB camera and one K151 StackChan on the open-source Strider. The pilot uses the existing game's audio near the robot.
- **ROS 2:** A camera topic, evidence service, and cancellable walking action connect to the current game.
- **Stage 1 BPU performance:** The DUG Tokyo loaner recorded 28.4 FPS at 640 × 480. The November 10 C270 retest used still images.

## Architecture

[Data flow, compute allocation, and ROS 2 interfaces](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/docs/stage2/architecture.md)

## Links and Evidence

- [Stage 2 proposal and success targets](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/docs/stage2/proposal.md)
- [Stage 2 architecture](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/docs/stage2/architecture.md)
- [Stage 2 engineering plan, BOM, and risks](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/docs/stage2/engineering-plan.md)
- [Public roadmap](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/ROADMAP.md)
- [Stage 1 hardware and inference evidence](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/tree/main/evidence) · [Stage 1 Discord check-in](https://discord.com/channels/1300358874280230994/1566820028366585957/1569393185879228456)

## Known Limitations and Safety

The camera frames the evidence area and keeps the images on the RDK. The fixed lane separates walking from hands and the table edge. The gavel is a display prop. The costume has been checked against the published geometry, with physical fit and walking tests planned. The game can finish with a stationary judge after a motion fault.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
