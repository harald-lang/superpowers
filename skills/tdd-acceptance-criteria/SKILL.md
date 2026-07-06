---
name: tdd-acceptance-criteria
description: Step 2 of overpowered TDD analysis phase. Use to interactively define and document acceptance criteria and scenarios with the human partner.
---

# Step 2: Defining Acceptance Criteria Interactively

Translate the agreed-upon requirements into concrete, actionable, and testable **Acceptance Criteria** before deciding how to split the task.

<HARD-GATE>
Do NOT begin coding or structuring vertical slices until your human partner has explicitly approved the acceptance criteria.
</HARD-GATE>

## Checklist

You MUST complete these steps:

1. **Draft Acceptance Criteria** — Write a clear list of what the system must do to satisfy the request. Organize by:
   - **Happy Path Scenarios:** Normal inputs, standard flows, successful outcomes.
   - **Validation Scenarios:** Invalid inputs, formatting checks, missing fields.
   - **Edge Cases:** Null/empty values, boundaries, extreme data sizes.
   - **Error Handling Scenarios:** Downstream failures, system exceptions, state conflicts.
2. **Focus on Behavior (Outcome-Oriented)** — Describe what the code should do from a consumer or user perspective. Avoid coupling criteria to implementation details (like classes, SQL queries, or specific library calls).
3. **Present and Refine** — Present the drafted criteria to your human partner. Ask them for feedback and make any necessary adjustments interactively.
4. **Obtain Explicit Approval** — Ask the user if the list is correct and covers all expected outcomes.
5. **Transition** — Once approved, invoke the `overpowered:tdd-task-slicing` skill.

## Example format to present:

> ### Draft Acceptance Criteria
> 
> **Happy Path:**
> - [ ] Given valid email `test@example.com`, `validateEmail` returns `true`.
> - [ ] Given email with uppercase characters, validation normalizes to lowercase and returns `true`.
> 
> **Validation & Boundaries:**
> - [ ] Given an empty string, returns `false` with error "Email is required".
> - [ ] Given email without `@`, returns `false` with error "Invalid email format".
> - [ ] Given email longer than 254 characters, returns `false` with error "Email exceeds maximum length".
