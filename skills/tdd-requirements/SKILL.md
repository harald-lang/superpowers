---
name: tdd-requirements
description: Step 1 of overpowered TDD analysis phase. Use to interactively explore and understand requirements through collaborative brainstorming or grilling before defining acceptance criteria.
---

# Step 1: Understanding Requirements Interactively

Before defining test cases or implementation steps, you must establish a deep, shared understanding of what you are building with your human partner.

<HARD-GATE>
Do NOT write any production or test code, scaffold files, or make edits during this phase. Focus entirely on dialogue and context gathering.
</HARD-GATE>

## Checklist

You MUST complete these steps:

1. **Explore project context** — Analyze existing code, documentation, and run current tests to verify the suite runs successfully.
2. **Interact with your human partner** — Present questions and listen to their requirements.
   - Ask clarifying questions **one at a time** (avoid overwhelming lists of questions).
   - Use multiple-choice options when possible.
   - For complex, ambiguous, or architectural changes, recommend the `/grill-me` slash command so you can align via an interactive interview.
3. **Propose 2-3 approaches** — Present alternative designs with trade-offs and make a clear recommendation.
4. **Transition** — Once requirements and approaches are agreed upon, invoke the `overpowered:tdd-acceptance-criteria` skill.

## Key Principles

- **One question at a time** — Keep conversation focused and step-by-step.
- **Understand the "Why"** — Clarify user intent, business value, constraints, and success criteria.
- **YAGNI (You Aren't Gonna Need It)** — Actively push back against speculative or out-of-scope requirements. Simplify the scope to the absolute minimum needed to deliver value.
- **No code yet** — Keep the conversation at a conceptual and design level. Do not draft signatures or classes in source files.
