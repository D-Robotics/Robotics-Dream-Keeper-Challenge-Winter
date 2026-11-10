# First Vision on RDK X5

- **Participant:** Mayu (naosurobot-crypto)
- **Stage:** 1 — Ignite, submitted for review
- **Repository:** https://github.com/naosurobot-crypto/rdk-challenge-2026
- **Demo evidence:** https://github.com/naosurobot-crypto/rdk-challenge-2026/blob/main/usb_camera.png
- **Community post:** https://discord.com/channels/1300358874280230994/1566089489791590702/1569696959873421362 (Discord server access required)
- **License:** No license has been specified for the participant's repository. The demo is an existing RDK sample; consult its original terms.

## Summary

This Stage 1 project explores how to bring up an RDK X5 and run a first on-device computer vision task with a USB webcam. The aim was to establish a working foundation for future robotics experiments: boot the board, connect it to a development computer and the internet, read camera input, and run an observable AI demo.

I flashed RDK OS 3.5.0 Desktop to a microSD card with RDK Studio, booted the board, and connected it to a Mac using Type-C direct and SSH. After connecting the board to Wi-Fi, I confirmed internet access. A USB webcam was recognized and a capture test succeeded. I then ran the existing USB camera YOLO sample on the RDK X5 and observed bounding boxes and bottle labels on two bottles. The linked repository records the commands, screenshots, and troubleshooting notes. The detection program is an existing sample, not a newly trained or custom model.

During setup, image decompression initially failed due to insufficient free space on the Mac. After freeing space and restoring the image, flashing succeeded. A Raspberry Pi camera cable did not fit the RDK connector, so I used a USB webcam. This is an initial vision experiment; a complete robot and an integrated control system are future work.

## Technical Highlights

- **Board / image:** RDK X5, RDK OS 3.5.0 Desktop.
- **AI demo:** Existing `usb_camera_yolov5x.py` sample; bottle detection shown on the board's remote desktop.
- **Sensor:** USB webcam; `/dev/video0` and `/dev/video1` detected.
- **ROS 2:** Not used in this Stage 1 demo.
- **BPU / performance:** Not separately verified or benchmarked.

## Architecture

USB webcam → RDK X5 camera sample and YOLO detection → remote desktop display. The Mac provides RDK Studio and remote access.

## Links and Evidence

- [Flash completion](https://github.com/naosurobot-crypto/rdk-challenge-2026/blob/main/flash.png)
- [SSH session](https://github.com/naosurobot-crypto/rdk-challenge-2026/blob/main/ssh.png)
- [Camera and AI output](https://github.com/naosurobot-crypto/rdk-challenge-2026/blob/main/usb_camera.png)
- [Setup, commands, and troubleshooting](https://github.com/naosurobot-crypto/rdk-challenge-2026)

## Known Limitations and Safety

This is an unmodified sample demonstration, not an integrated moving robot. No actuator was used. BPU acceleration, performance, and broader detection accuracy have not been verified.

## Promotion consent

Pending participant confirmation of the organizers' showcase usage terms.
