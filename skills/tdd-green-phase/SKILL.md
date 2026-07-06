---
name: tdd-green-phase
description: Step 3 of overpowered TDD sequence. Use to write the minimal code to pass the failing test and verify all tests pass.
---

# TDD GREEN Phase: Write Minimal Code to Pass

The goal of the GREEN phase is to get the test to pass as quickly as possible. Do not write a complete, elegant solution yet — write just enough code to make the failing test pass.

```
WRITE THE MINIMAL CODE TO PASS THE TEST
```

## Checklist

You MUST complete these steps in order:

1. **Write minimal code** — Implement code using one of the three classic TDD strategies (Fake It, Obvious Implementation, Triangulation).
2. **Run the test runner** — Execute the test suite to verify the test passes.
3. **Verify GREEN** — Confirm:
   - The new test passes.
   - All existing tests still pass.
   - There are no compiler, linter, or console warnings.
4. **Commit** — Commit the green state.
5. **Transition**:
   - If there are remaining tests on your Test List: Invoke `overpowered:tdd-red-phase` for the next test.
   - If the Test List is complete: Invoke `overpowered:tdd-refactor-phase` to clean up the code.

## Three Classic TDD Strategies

### 1. Fake It ('til you make it)
Return a hardcoded constant first. This verifies that your test assertion works and that the test suite is hook-connected without introducing logic bugs.
*Example:*
```typescript
// Test expects: getActiveUsers() to return [{ id: 1, active: true }]
function getActiveUsers(users: User[]): User[] {
  return [{ id: 1, active: true }]; // Hardcoded fake to pass first test
}
```

### 2. Obvious Implementation
If the implementation is completely trivial and obvious, write it immediately.
*Example:*
```typescript
function add(a: number, b: number): number {
  return a + b; // Trivial implementation
}
```

### 3. Triangulation
If you aren't sure how to generalize the implementation, do not guess or write speculative code. Instead, write another test with different inputs/outputs (forces triangulation) which will narrow down and dictate the general implementation.
*Example:*
- Test 1: `expect(square(2)).toBe(4)` -> Fake it by returning `4`.
- Test 2: `expect(square(3)).toBe(9)` -> Now you must generalize to `return x * x`.

## YAGNI (You Aren't Gonna Need It)

Do not over-engineer. Do not add:
- Vague "future-proof" options
- Extra parameters
- Unused helper methods
- Theoretical error handling not covered by a test

If it doesn't serve the current failing test, it doesn't belong in the production code.

## Verification Checklist (GREEN)

Before moving to refactoring or the next test, check off the following:

- [ ] The new test passes successfully.
- [ ] No other tests in the codebase are broken.
- [ ] You committed the change.
