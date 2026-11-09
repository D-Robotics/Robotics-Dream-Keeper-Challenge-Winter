# Home Court Robot

- **Participant:** Shu
- **Stage completed:** 1
- **Repository:** https://github.com/shoujiki-panman/rdk-x5-home-court-robot
- **Demo video:** Stage 1 evidence images in the repository (see Links and Evidence)
- **Community post:** Discord thread "RDK Challenge - 11/02/2026 - Shu" in #robotics-dream-keeper-challenge (link to be added)
- **License:** [MIT License](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/LICENSE)

## Summary

Home Court Robot is a home robot that settles small family arguments, such as who ate the last snack, by looking at evidence instead of taking sides. RDK X5 is the brain: it watches the living room with a camera and detects events on the BPU, so family video never leaves the house. My StackChan desktop robot is the body: it turns to the person speaking, shows the logged evidence, and nods down like a gavel to announce a verdict.

For Stage 1, I brought up an RDK X5 at DUG Tokyo #1 in Akihabara on 2026-10-31. I connected it to a Mac with RDK Studio (RDK Type-C direct), logged in over SSH with a dedicated key, and recorded the system image and kernel. I attached a USB camera (ELECOM UCAM-C0220F), which appeared as `/dev/video0`, and captured frames with ffmpeg. Then I ran the official YOLO11n detection sample on the BPU, first on the sample image and then on live camera frames. A small script streams the live detections to a browser, and it ran at about 28 FPS with about 25 ms per frame.

The board was a loaner at the venue. I will repeat the same steps on my own sample kit and replace the evidence.

## Technical Highlights

- **RDK board / image:** RDK X5, Ubuntu 22.04.5 LTS, kernel 6.1.83, RDK OS 3.5.0
- **AI model and runtime:** `yolo11n_detect_bayese_640x640_nv12.bin` (COCO 80 classes) with the official `pydev_demo` YOLO11 sample (`hbm_runtime`)
- **Sensors and actuators:** USB camera (ELECOM UCAM-C0220F, `/dev/video0`); no actuators yet
- **ROS 2 design:** Not yet (planned for Stage 2)
- **BPU evidence and performance:** YOLO11n on the BPU with the live USB camera at 640×480: 28.4 FPS, about 25 ms per frame (pre-process, inference and post-process)

## Architecture

Stage 1 setup. The Mac reaches the board over the Type-C USB network, and the camera frames go through YOLO11 on the BPU.

```mermaid
flowchart LR
    Mac["Mac + RDK Studio"] -- "USB Type-C network<br/>192.168.128.10" --> X5["RDK X5"]
    Cam["USB camera<br/>/dev/video0"] --> X5
    X5 --> BPU["YOLO11n on BPU"]
    BPU --> Web["Browser view<br/>(MJPEG, port 8080)"]
```

## Links and Evidence

- Flash and SSH evidence: [01-ssh-system-info.txt](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/evidence/01-ssh-system-info.txt)
- Sensor proof: [02-camera-capture-blurred.jpg](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/evidence/02-camera-capture-blurred.jpg)
- AI output: [03-yolo11-kite.jpg](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/evidence/03-yolo11-kite.jpg), [04-yolo11-camera-blurred.jpg](https://github.com/shoujiki-panman/rdk-x5-home-court-robot/blob/main/evidence/04-yolo11-camera-blurred.jpg)
- Documentation: [README](https://github.com/shoujiki-panman/rdk-x5-home-court-robot#readme)

## Known Limitations and Safety

- The Stage 1 evidence was taken on a board lent at the venue. It will be replaced with runs on my own sample kit.
- People's faces in the camera shots are pixelated before publishing.
- There are no moving parts yet. When StackChan is added in Stage 3, its head motion will have speed limits and a stop command.

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
