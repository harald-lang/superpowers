---
name: tdd-task-slicing
description: Step 3 of overpowered TDD analysis phase. Use to slice the approved requirements and acceptance criteria into minimal vertical slices.
---

# Step 3: Vertical Slicing & Task Planning

Decompose the approved acceptance criteria into small, sequential, vertically sliced tasks.

<HARD-GATE>
Do NOT start implementing tests or code until your human partner has approved the task list.
</HARD-GATE>

## Checklist

You MUST complete these steps in order:

1. **Identify Preparatory Refactoring Needs** — Assess whether the codebase needs design changes or refactoring to make implementing the feature easy.
   - **THE SEPARATION RULE:** If refactoring is needed, add it as a separate, initial task. It must be implemented and committed *separately* using existing tests. It **must never** be mixed into the final feature PR/commit.
2. **Decompose into Vertical Slices** — Divide the acceptance criteria into small, independent vertical slices (one behavioral capability at a time).
   - *Good (Vertical):* Implements a simple end-to-end capability (e.g., "Step 1: Parse input & validate structure", "Step 2: Calculate basic metrics").
   - *Bad (Horizontal):* Splitting by technical layers (e.g., "Step 1: Write database schema", "Step 2: Implement API route", "Step 3: Implement frontend UI").
3. **Present the Task List** — Present the planned sequence of vertical slices and any preparatory refactoring tasks to your human partner.
4. **Obtain Explicit Approval** — Align with the user and get approval on the task list.
5. **Transition** — Once approved, ask the human partner whether they want to:
   - **Execute Inline**: You will invoke the `overpowered:tdd-cycle` skill to execute the tasks sequentially in this session.
   - **Dispatch to Agents**: You will invoke the `overpowered:tdd-agent-dispatch` skill to generate standalone prompts for fresh agents to execute the slices in isolation.

## The Separation Rule (from NOTES.md)

> "Make the change easy (warning: this might be hard), then make the easy change." — Kent Beck

If you determine that existing code needs design changes to accommodate the new feature:
- Write a task for the refactoring.
- Execute it *first* under green tests.
- Verify no regressions.
- Commit the refactoring separately (e.g., `refactor: extract X class`).
- Do **not** package this refactoring into the final feature PR. Keep it clean.

## Vertical Slicing Guidelines

| Slicing | Good (Vertical ✅) | Bad (Horizontal ❌) |
|---------|-------------------|-------------------|
| **Approach** | Build ONE small end-to-end user capability at a time. | Build the database, then the API, then the UI in bulk. |
| **Feedback** | Fast validation of design, fast feedback from tests. | Long lead time, complex debugging at the end. |
| **Quality** | Refactor as you go, keep system working. | Speculative models and mocks that don't match reality. |

## The Micro-TDD Rule (Granularity Mismatch Warning)

> [!IMPORTANT]
> **Macro-Slices vs. Micro-Tests:**
> A vertical slice defined during task slicing is NOT a single unit test. Slices are macro capabilities. When implementing a vertical slice:
> 1. Before writing any code, decompose the slice into a list of focused **micro-test cases** (e.g., `testValidateThrowsOnNullEmail`, `testValidateThrowsOnEmptyString`).
> 2. Each micro-test case must check exactly one logical concept or assertion.
> 3. Execute the Red-Green-Refactor cycle individually for each micro-test, one by one. Do not write a single test that asserts the entire slice at once.
