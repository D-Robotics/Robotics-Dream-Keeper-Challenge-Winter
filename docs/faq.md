# Frequently Asked Questions

## Registration and Schedule

### What are the main dates?

Registration runs **September 30–October 31, 2026**. Stage 1 runs **November 1–10**, Stage 2 runs **November 11–26**, and Stage 3 runs **November 27–December 15**. Judging follows in late December, with Show & Tell planned for **January 7, 2027**. See [TIMELINE.md](../TIMELINE.md).

### Where are the registration, Discord, and webinar links?

They will be added to [README.md](../README.md) after organizer confirmation. Do not use links copied from a previous season unless the organizer explicitly re-confirms them.

### Can I work ahead?

Yes. You may prepare later-stage work early, but titles and rewards require the evidence and submission steps for each stage.

## Repository and Access

### Do I need both a personal repository and a fork of this repository?

Yes. Your code, logs, and project documentation live in your personal repository. Your fork is used only to submit or update the showcase Markdown file under this official repository's `projects/` directory.

### Does the official repository take ownership of my code?

No. Participant code remains in participant-owned repositories under the participant's selected license. The showcase document submitted here may be used by organizers for judging, promotion, and archives.

## Pull Requests

### What should I submit to this repository?

Submit one Markdown project profile under `projects/`. Do not submit a full codebase or a large video file.

### My Pull Request has conflicts. What should I do?

```bash
git fetch upstream
git switch <your-branch>
git merge upstream/<published-default-branch>
# resolve only the relevant project Markdown conflicts
git add projects/<your-file>.md
git commit -m "Resolve showcase conflict"
git push
```

### Can I update my showcase after Stage 1?

Yes. Update the same showcase file and Pull Request path as you progress through Stages 2 and 3.

## Tasks and Hardware

### Do I need ROS 2 in Stage 1?

Not unless the selected sensor or demo requires it. Stage 2 architecture and Stage 3 integration require a clear ROS 2 design.

### Can I use a sensor not listed in the task?

Ask the organizer before the deadline. Provide the board revision, system image, sensor model, interface, and the evidence you plan to submit.

### Can I start from an official demo?

Yes, but the submission must show your own run. Later stages must add substantive system design and integration beyond a stock example.

### My model runs on the CPU. Does that satisfy Stage 3?

Stage 3 requires BPU acceleration for at least one significant inference workload. Document the model, runtime, and evidence of the accelerated path.

## Awards and Shipping

### When are prizes distributed?

The plan targets distribution within one month after the program ends. Final tax, identity, location, shipping, and eligibility terms will be announced by the organizers.

### Are external posts counted for RDK Advocator recognition?

They must be public, published outside D-Robotics-owned communities, mention D-Robotics/RDK/RDK Challenge, and include an official referral link. Keep a list with URLs and platform analytics.

## Getting Help

When asking for technical help, include:

- Current stage and intended result.
- Board and system image version.
- Sensor or accessory model.
- Commands run and complete error text.
- Photos of wiring when relevant, with private information removed.
