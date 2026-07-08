---
name: tdd-agent-dispatch
description: Use to dispatch TDD task slices to fresh subagents. Generates self-contained prompts for each slice to be executed in isolation.
---

# TDD Agent Dispatch

Use this skill when your human partner chooses to dispatch task slices to isolated agents rather than executing them inline in the current session. 

## The Goal
Instead of one agent working through a monolithic list of tasks and accumulating excessive context, this skill packages each vertical slice (from `tdd-task-slicing`) into a highly focused, independent prompt. These prompts are then handed off to fresh agents whose sole purpose is to implement that specific slice using the `overpowered:tdd-cycle` skill.

## Procedure

For each approved vertical slice, create a self-contained markdown file containing the prompt for the subagent.

1. **Create the Prompt Files:**
   Create a prompt file for each slice in a dedicated directory (e.g., `docs/overpowered/dispatch-prompts/<feature-name>/slice-N.md`).

2. **Prompt Anatomy:**
   Every generated prompt MUST include:
   - **Role & Directive:** Explicit instruction to act as a TDD implementer and strictly follow the `overpowered:tdd-cycle` skill.
   - **Global Context:** A brief summary of the overarching feature and requirements to provide necessary grounding.
   - **Acceptance Criteria:** The specific AC relevant to this slice.
   - **The Slice Details:** The exact vertical slice steps to be implemented.
   - **The Command:** An explicit instruction to invoke the skill, e.g., "Begin by invoking the `overpowered:tdd-cycle` skill."

3. **Provide Execution Instructions:**
   Once the prompt files are generated, tell your human partner where they are located. Depending on their setup, they can either copy-paste these prompts into fresh agent sessions or use an automated runner script to dispatch them.

## Prompt Template

Use the following structure for the prompt files:

```markdown
# Agent Task Briefing: [Slice Title]

You are an expert TDD implementation agent. Your task is to implement a specific vertical slice of a larger feature. You MUST strictly follow the `overpowered:tdd-cycle` skill for this implementation.

## 1. Feature Context
[Brief summary of what we are building overall]

## 2. Acceptance Criteria
[Relevant AC for this specific slice]

## 3. Your Specific Task Slice
[Detailed steps for this vertical slice]

## 4. Execution Rules
- Do NOT implement any out-of-scope features (YAGNI).
- Write minimal failing tests first (RED), pass them (GREEN), and clean up (REFACTOR).
- Your very first action MUST be to invoke the `overpowered:tdd-cycle` skill.
```

## Completion

Once you have generated all prompts, confirm with the user. The current session has now completed its planning and dispatching duties!
