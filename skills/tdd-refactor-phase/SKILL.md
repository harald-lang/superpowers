---
name: tdd-refactor-phase
description: Step 4 of overpowered TDD sequence. Use to clean up code and tests while keeping tests green.
---

# TDD REFACTOR Phase: Clean Up Code and Tests

Refactoring is the process of improving the design of existing code without changing its external behavior. It is done **only** when all tests are green.

```
REFACTOR PRODUCTION CODE AND TEST CODE SEPARATELY
```

Never add new features or write new tests while refactoring.

## Checklist

You MUST complete these steps in order:

1. **Identify refactoring targets** — Look for duplication, poor naming, long methods, high coupling, or leftover hardcoded values from "Fake It".
2. **Refactor production code** — Improve design, naming, structure of implementation.
3. **Verify green** — Run tests. They must pass.
4. **Refactor test code** — Clean up test duplication, extract helpers, improve test readability, simplify setups. Test code is first-class code.
5. **Verify green** — Run tests. They must pass.
6. **Commit** — Commit the refactoring changes separately (e.g., `refactor: extract user validation helper`).
7. **Transition** — Once code is clean and green, invoke the `overpowered:tdd-verification` skill.

## Separating Concerns in Refactoring

It is crucial to refactor implementation code and test code in separate cycles:

```dot
digraph refactoring_flow {
    Start [shape=box, label="Start (All Green)"];
    RefactorProd [shape=box, label="Refactor production code"];
    VerifyProdGreen [shape=diamond, label="Verify green?"];
    RefactorTest [shape=box, label="Refactor test code"];
    VerifyTestGreen [shape=diamond, label="Verify green?"];
    CommitRefactor [shape=box, label="Commit refactoring"];

    Start -> RefactorProd;
    RefactorProd -> VerifyProdGreen;
    VerifyProdGreen -> |No| RefactorProd;
    VerifyProdGreen -> |Yes| RefactorTest;
    RefactorTest -> VerifyTestGreen;
    VerifyTestGreen -> |No| RefactorTest;
    VerifyTestGreen -> |Yes| CommitRefactor;
}
```

If you refactor both the implementation and the tests at the same time and a test fails, you won't know if the production code changed its behavior or if the test itself became broken.

## Smells to Watch Out For

- **Duplication** — Same logic duplicated in multiple places.
- **Magic numbers / hardcoding** — Leftovers from the Green phase. Generalize them.
- **Poor naming** — Variable or function names that don't reveal intent.
- **High coupling** — Classes or modules that know too much about each other's internals.
- **Large test setup** — Complex, massive `beforeEach` or setup blocks in tests. Extract helpers or simplify dependencies.

## Verification Checklist (REFACTOR)

Before finishing, check off:

- [ ] Production code is cleaner, more readable, and conforms to design standards.
- [ ] Test code is clean, readable, and free of duplication.
- [ ] All tests are passing successfully.
- [ ] Changes are committed with a prefix of `refactor:`.
