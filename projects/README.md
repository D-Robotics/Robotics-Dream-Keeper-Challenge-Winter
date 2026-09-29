# Participant Project Showcase

This directory collects one Markdown file per participant project submitted through Pull Requests. Participant source code stays in participant-owned repositories.

For examples of completed profiles, browse the [2026 Summer project wall](https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge/blob/develop/SHOWCASE.md). Previous-season profiles are references only and are not part of the Winter cohort.

## Filename Rule

```text
<ParticipantName>-Project-<ProjectSlug>.md
```

Good examples:

- `Jamie-Project-WarehousePatrol.md`
- `AlexLi-Project-HomeAssistant.md`

Avoid generic filenames, spaces, non-portable punctuation, and version suffixes such as `final-v2`.

## Required Content

| Section | Requirement |
|---|---|
| Project name | Public title |
| Participant | Name and optional registered team members |
| Stage completed | 1, 2, or 3 |
| Summary | 120–300 words covering the problem, approach, and current result |
| Source repository | Public participant-owned GitHub URL |
| Demo | Stable video or evidence URL appropriate to the completed stage |
| Community post | Permalink to the participant's challenge thread |
| Technical highlights | Models, sensors, BPU use, ROS 2 graph, and measured performance where relevant |
| Evidence checklist | Links matching the completed stage requirements |

Architecture diagrams, benchmark tables, and license information are strongly encouraged.

## Template

Copy the block below into your project file:

```markdown
# <Project Name>

- **Participant:** <Name>
- **Stage completed:** <1 | 2 | 3>
- **Repository:** <https://github.com/...>
- **Demo video:** <https://...>
- **Community post:** <https://...>
- **License:** <license used by your source repository>

## Summary

<120–300 words: problem, users, approach, and result>

## Technical Highlights

- **RDK board / image:** <...>
- **AI model and runtime:** <...>
- **Sensors and actuators:** <...>
- **ROS 2 design:** <...>
- **BPU evidence and performance:** <...>

## Architecture

<Diagram link or Mermaid diagram, plus a short explanation>

## Links and Evidence

- Stage evidence: <...>
- Benchmarks: <...>
- Documentation: <...>

## Known Limitations and Safety

<...>

---

I agree that this showcase document may be used by the Robotics Dream Keeper Challenge organizers for program promotion, judging, and archives as described in the official README.
```

See [Example-Project-SampleVision.md](./Example-Project-SampleVision.md) for a non-submission example.

## Review Rules

Maintainers review filename, completeness, link access, stage evidence, safety, and license disclosures. Maintainers merge showcase documents only; they do not merge participant source code into this repository.
