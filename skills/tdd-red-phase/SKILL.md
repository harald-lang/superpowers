---
name: tdd-red-phase
description: Step 2 of overpowered TDD sequence. Use to write a single minimal failing test and verify it fails with the expected error.
---

# TDD RED Phase: Write a Failing Test

The goal of the RED phase is to write a single, focused test that defines a small piece of desired behavior, run it, and watch it fail.

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

If you write production code before the test, delete it immediately. Start over.

## Checklist

You MUST complete these steps in order:

1. **Select one item** — Pick exactly one test scenario from your approved Test List.
2. **Write the test** — Implement the test case asserting the desired outcome. Do NOT modify any production code yet.
3. **Run the test runner** — Execute the test command (e.g., `npm test`, `pytest`, `cargo test`).
4. **Verify the failure (Verify RED)** — Ensure the test fails, and fails for the expected reason (e.g., a missing method, a mismatch in return values, or an assertion failure).
5. **Transition** — Once the expected failure is verified, invoke the `overpowered:tdd-green-phase` skill to implement the code.

## The Beyoncé Rule

> "If you liked it, then you should have put a test on it."

If a behavior is important enough to exist, it must have an explicit test covering it. Do not assume any behavior is safe without direct coverage.

## Verification Checklist (RED)

Before proceeding, confirm the following:

- [ ] Only test code has been added/modified. No production code has been touched.
- [ ] The test runner successfully executed the test suite.
- [ ] The new test failed.
- [ ] You can explain the exact failure message.
- [ ] The failure is due to missing behavior/implementation, not syntax errors, incorrect imports, or test setup crashes.

If the test passes immediately, either:
- The behavior is already implemented (remove/change the test or cross it off the list).
- The test is not asserting the right thing (fix the test so it fails).

## Examples

### Good: Single Assert, Clear Intent

```typescript
test('should return a list of active users', () => {
  const users = [{ id: 1, active: true }, { id: 2, active: false }];
  const active = getActiveUsers(users);
  expect(active).toEqual([{ id: 1, active: true }]);
});
```
*Why it's good:* Tests one specific behavior, uses real data structure, makes a clean assertion.

### Bad: Testing Multiple Things At Once

```typescript
test('user lifecycle', () => {
  const user = createUser('Alice');
  expect(user.name).toBe('Alice');
  
  const active = toggleActive(user);
  expect(active.status).toBe('active');
  
  deleteUser(user.id);
  expect(getUser(user.id)).toBeNull(); // ❌ Too many assertions and behaviors in one test!
});
```
*Why it's bad:* Violates the "one thing" rule. If it fails, it's hard to know which part failed. It forces you to write a massive block of production code to make it pass.
