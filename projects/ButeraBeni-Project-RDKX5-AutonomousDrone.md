# Lawn Scout — AI Lawn-Health Scanner on an RDK X5 Drone

* **Participant:** ButeraBeni
* **Stage completed:** 2
* **Repository:** [https://github.com/buterabeni-web/rdk-x5-autonomous-drone](https://github.com/buterabeni-web/rdk-x5-autonomous-drone)
* **Demo video:** [https://github.com/user-attachments/assets/206f594d-c7a0-4acc-b9b2-ef0c5b23fccf](https://github.com/user-attachments/assets/206f594d-c7a0-4acc-b9b2-ef0c5b23fccf) (Stage 1)
* **Community post:** <https://discord.com/channels/1300358874280230994/1568536611594174534/1575892307897618542>
* **License:** MIT

## Summary

Lawns, school grounds, sports fields and small farm plots in Rwanda are checked by walking them, so dry grass and bare soil are noticed late and water is spread evenly instead of where it is needed. Many of these places have weak GPS and no reliable internet. Lawn Scout finds these problems with AI running entirely on the RDK X5, mounted on a drone.

In Stage 2 I moved the project to this agriculture use case, partly because of Rwanda's drone rules. I built and tested a classic HSV lawn-health method on the board (grid, outlined problem areas and a live browser view at 640 × 480), designed the hardware (a printed deck for the RDK X5 over the flight-controller stack and a window plate for the MTF-01 optical-flow and lidar sensor), and wrote the full system design.

The final demo is a handheld scan of a real lawn using the drone hardware with the propellers removed. A custom YOLO11n-seg model on the BPU segments stressed grass and bare soil live, while a second BPU model detects plastic bottles. The MTF-01 measures height so each problem is reported in square metres, and the frames are combined into a map of the lawn. Results will be measured on the board: speed, accuracy, area accuracy, and a comparison with the classic HSV method. Pilot-flown and then autonomous scanning come after the demo.

## Technical Highlights

* **RDK board / image:** RDK X5 (8 GB), RDKOS 3.5.0 Desktop, TogetheROS.Bot (ROS 2 Humble)
* **AI model and runtime:** custom YOLO11n-seg (INT8) on the BPU for `stressed\_patch` and `bare\_spot`; stock COCO YOLO on the BPU for bottles and people; HSV baseline on the CPU (implemented)
* **Sensors and actuators:** USB camera 640 × 480 @ 30 fps; MicoAir MTF-01 ToF lidar + optical flow over UART; LED alert on GPIO 37
* **ROS 2 design:** camera → codec → two BPU models → lawn analyzer (fused with MTF-01 height) → mapper and web UI; time-synchronised camera and lidar; per-topic QoS
* **BPU evidence and performance:** Stage 1 YOLOv5 on the BPU with `/image` at \~30 Hz; Stage 3 targets ≥ 15 FPS segmentation, mask mAP50 ≥ 0.60, area within ± 20 %

## Architecture

```mermaid
flowchart LR
    C\[USB camera] --> D\[hobot\_codec]
    D --> S\[\[BPU: lawn segmentation]]
    D --> B\[\[BPU: COCO bottles / people]]
    M\[MTF-01 height + flow] --> A
    S --> A\[lawn\_analyzer<br/>% and m²]
    B --> A
    A --> MAP\[lawn\_mapper]
    M --> MAP
    A --> UI\[web UI :8080]
    MAP --> UI
    A --> L\[LED alert]
```

Everything runs on the RDK X5; the phone or laptop only views the results. Full details, module table, compute allocation and ROS 2 graph are in the architecture document.

## Links and Evidence

* Proposal: [https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/PROPOSAL.md](https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/PROPOSAL.md)
* Architecture: [https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/ARCHITECTURE.md](https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/ARCHITECTURE.md)
* Engineering plan (BOM, risks, repo structure): [https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/ENGINEERING\_PLAN.md](https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/docs/ENGINEERING_PLAN.md)
* Roadmap: [https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/ROADMAP.md](https://github.com/buterabeni-web/rdk-x5-autonomous-drone/blob/main/ROADMAP.md)
* Stage 1 evidence: [https://github.com/buterabeni-web/rdk-x5-autonomous-drone#stage-1--ignite](https://github.com/buterabeni-web/rdk-x5-autonomous-drone#stage-1--ignite)

## Known Limitations and Safety

* The segmentation model is not trained yet; current results use the HSV method, which needs camera-specific thresholds.
* The final demo is handheld; flight follows only with a licensed pilot and authorization under Rwanda RCAA rules.
* Propellers are removed for all handheld and bench work, and the RDK is powered through a BEC checked with a multimeter.

\---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.

