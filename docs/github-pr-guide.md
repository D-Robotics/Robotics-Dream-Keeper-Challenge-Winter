# How to Submit a Project Showcase Pull Request

This guide takes you from a personal project repository to a showcase Markdown file submitted under this official repository's `projects/` directory.

<!-- VISUAL PLACEHOLDER
Approved screenshots will be added later under docs/images/github-pr-guide/.
Do not add Summer screenshots or temporary visuals to the Winter repository.
-->

## Prerequisites

- A GitHub account.
- Git installed locally.
- A public participant repository containing the current project artifacts.
- The required stage deliverables listed under [`stages/`](../stages/).

## 1. Fork the Official Winter Repository

Open the canonical repository URL announced by the organizers and select **Fork**. Do not use an unofficial mirror.

The planned repository name is:

```text
D-Robotics/Robotics-Dream-Keeper-Challenge-Winter
```

Confirm the published URL in [README.md](../README.md) before cloning.

## 2. Clone Your Fork

```bash
git clone https://github.com/<YOUR_USERNAME>/Robotics-Dream-Keeper-Challenge-Winter.git
cd Robotics-Dream-Keeper-Challenge-Winter
git remote add upstream https://github.com/D-Robotics/Robotics-Dream-Keeper-Challenge-Winter.git
```

## 3. Create a Submission Branch

```bash
git switch -c showcase/<github-username>-<stage>
```

Example: `showcase/alex-stage2`.

## 4. Add or Update Your Showcase File

Use this mandatory filename format:

```text
<ParticipantName>-Project-<ProjectSlug>.md
```

Examples:

- `Tom-Project-RobotVision.md`
- `AlexLi-Project-HomePatrolBot.md`

Copy the template from [projects/README.md](../projects/README.md). Keep one showcase file per project and update the same file as the project advances.

## 5. Validate Before Committing

- The file is directly under `projects/`.
- Every required section is present.
- Repository, demo, and community links open without login or expiration.
- The stated stage matches the evidence.
- No token, password, private key, personal address, or private Discord screenshot is included.
- Large videos are linked, not committed.

## 6. Commit and Push

```bash
git add projects/<ParticipantName>-Project-<ProjectSlug>.md
git commit -m "Add showcase: <ParticipantName> <ProjectName>"
git push -u origin showcase/<github-username>-<stage>
```

## 7. Open the Pull Request

Target the official repository's published default branch.

Recommended title:

```text
[Showcase] <ParticipantName> — <ProjectName> (Stage X)
```

Include this checklist in the description:

```markdown
- [ ] Participant name matches the filename
- [ ] Current stage is stated
- [ ] Source repository is public
- [ ] Required evidence links are included
- [ ] Demo link is stable
- [ ] I agree that this showcase document may be used for program promotion, judging, and archives
```

## 8. Respond to Review

Maintainers may request changes. Edit the same branch, commit, and push again; the Pull Request updates automatically.

```bash
git add projects/<your-file>.md
git commit -m "Address showcase review"
git push
```

## Common Problems

| Problem | Resolution |
|---|---|
| Push permission denied | Push to your fork, not the official repository; configure an SSH key or approved HTTPS credential |
| Branch is behind | Fetch `upstream` and merge or rebase the published default branch |
| File is in the wrong folder | Move it directly under `projects/` |
| Video is too large | Host it on YouTube or another stable service and add the link |
| Link requires reviewer access | Change visibility or use the organizer-approved private upload path |

For unresolved issues, see [faq.md](./faq.md) or ask in the official Discord challenge channel.
