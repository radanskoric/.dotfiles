---
name: walkthrough
description: Create a walkthrough of the implementation to help the user understand how it works.
disable-model-invocation: true
---

Give the user a walkthrough of the implementation, using the mode supplied alongside the skill mention (for example, `@walkthrough diff` or `$walkthrough brief`). Use `default` when no mode is supplied. Treat any remaining text as the subject or additional guidance. Explicit user instructions take precedence over mode defaults.

## Approach

In every mode, build the explanation progressively so each step is clear and builds on previous steps. Assume high level of software engineering expertise. Assume general familiarity with the codebase.

In your explanations:
- Name the components clearly.
- Include links to relevant pieces of code to ground the explanation in the codebase.
- Prefer direct and concise explanations.
- Avoid needless repetition or verbosity.
- Feel free to use a casual tone if it contributes to clarity.

Overall: aim to act as an experienced software engineer giving a walkthrough to their equally experienced colleague.

## Modes

- `default`: Give a comprehensive walkthrough of the entire functionality. Build a full mental model of how the implementation works and how it fits into the larger system.
- `brief`: Cover only the high-level broad strokes: the main components, their roles, and how they fit together. Assume the user will ask to dig into anything specific.
- `diff`: Walk through only the changes made in this session. Assume the user is completely familiar with the previous functionality; explain what this change implements without reteaching the existing system.
- `highlight`: Compare the session's implementation with what was discussed and planned. Focus on divergences and details requiring special attention, including unresolved decisions, incomplete work, and consequential implementation choices. Assume the user will interpret anything omitted as implemented as discussed. Inspect the relevant code and changes before making that assurance; explicitly identify anything you cannot verify or any missing discussion context. If everything matches and nothing needs special attention, say so concisely.
