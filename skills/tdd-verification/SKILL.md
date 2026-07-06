---
name: tdd-verification
description: Step 5 of overpowered TDD sequence. Use to run the complete test suite, check for anti-patterns, and verify final status.
---

# TDD Verification & Final Walkthrough

This is the final phase of the TDD cycle. Before presenting your changes to your human partner, you must run the entire test suite and verify that the implementation is clean, robust, and free of testing anti-patterns.

## Checklist

You MUST complete these steps:

1. **Run full test suite** — Verify all tests in the codebase pass.
2. **Anti-patterns audit** — Load and read [testing-anti-patterns.md](references/testing-anti-patterns.md). Verify your code does not violate any of the iron laws.
3. **Verify Checklist** — Check off each item in the Final Verification Checklist.
4. **Draft the Walkthrough** — Create a `walkthrough.md` artifact detailing what was modified, how it was verified, and the test run outputs.
5. **Present results** — Share the walkthrough with your human partner.

## Final Verification Checklist

Ensure you can check off every single box:

- [ ] Every new or modified behavior has an automated test.
- [ ] You watched each new test fail before implementing the code to pass it (TDD proof).
- [ ] Each test failed for the expected reason, not due to compilation errors or bad syntax.
- [ ] You wrote the minimal code to pass the test (YAGNI).
- [ ] The entire test suite passes cleanly with no warnings or console errors.
- [ ] Tests assert real behavior, not the existence or configuration of mocks.
- [ ] No test-only methods were added to production code classes.
- [ ] All mocks are fully specified and complete compared to the real interfaces they mock.
- [ ] Edge cases, boundary inputs, empty inputs, and error states are covered by tests.

If any check fails, you must return to the appropriate phase of the TDD loop (Red, Green, or Refactor) and resolve the issue.

## Testing Anti-Patterns Audit

Load and audit your code against [testing-anti-patterns.md](references/testing-anti-patterns.md):
- Did we mock something we didn't fully understand?
- Are we asserting on mock element existence?
- Did we add cleanups or helpers to production classes that are only used in tests?
- Are our mock API payloads missing fields that could break downstream code?

If any of these are present, refactor them immediately in the Refactor phase and verify green before continuing.
