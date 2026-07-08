# Overpowered — TDD Agent Skills

A suite of agent skills that applies strict **Test-Driven Development (TDD)** principles to AI-assisted software development. 

This workflow enforces a structured, interactive analysis phase between the AI agent and the human partner before any production or test code is written, ensuring alignment on requirements, acceptance criteria, and task decomposition.

---

## Workflow Flowchart

The following diagram illustrates the sequential execution of skills defined in this repository:

```mermaid
graph TD
    Start[Conversation Start] --> UOP[1. being-overpowered<br/>Entry Point]
    UOP --> Req[2. tdd-requirements<br/>Explore requirements & ask clarifying questions]
    Req --> AC[3. tdd-acceptance-criteria<br/>Define concrete acceptance criteria]
    AC --> Slice[4. tdd-task-slicing<br/>Vertical slicing & refactoring check]
    
    Slice --> |Refactoring Needed| Refactor[Execute & commit refactoring separately]
    Refactor --> |Run existing tests| Slice
    
    Slice --> |Approved Task List| Choice{Execution Choice}
    Choice --> |Inline| TDD[5. tdd-cycle<br/>Execute TDD loop per slice]
    Choice --> |Dispatch| Dispatch[5. tdd-agent-dispatch<br/>Generate Subagent Prompts]
    
    subgraph TDD Loop (Step 5)
        TDD --> Red[RED: Write minimal failing test]
        Red --> Green[GREEN: Write minimal code to pass]
        Green --> RefactorStep[REFACTOR: Clean code & tests separately]
        RefactorStep --> |Next Slice| Red
        RefactorStep --> |All Slices Green| Verify[Verify Anti-Patterns & Complete]
    end
```

---

## Skill Descriptions

### 1. `overpowered:being-overpowered`
* **Purpose:** The entry point controller.
* **Function:** Establishes the rules of engagement and dictates the sequential execution of the TDD skill pipeline. It requires the agent to invoke the relevant skill at each phase before responding or taking action.

### 2. `overpowered:tdd-requirements`
* **Purpose:** Requirements exploration.
* **Function:** Explores the project context, existing code, and requirements. The agent asks clarifying questions one at a time and utilizes interactive methods (such as `/grill-me` for complex tasks) to align with the human partner. **No coding is allowed.**

### 3. `overpowered:tdd-acceptance-criteria`
* **Purpose:** Defining success boundaries.
* **Function:** Translates requirements into a concrete list of happy paths, validation rules, edge cases, and error handling states. Requires explicit approval from the human partner before moving forward.

### 4. `overpowered:tdd-task-slicing`
* **Purpose:** Designing vertical slices.
* **Function:** Decomposes the approved acceptance criteria into independent, small vertical slices (implementing a single behavior end-to-end).
* **The Separation Rule:** If preparatory refactorings are needed to simplify implementation, they must be planned and executed *separately* using existing tests. They **must never** be part of the final feature PR/commit.

### 5. `overpowered:tdd-cycle`
* **Purpose:** TDD execution loop.
* **Function:** The original monolithic TDD engine. Runs the Red-Green-Refactor loop iteratively for each vertical slice:
  - **RED:** Write one failing test showing the behavior. Verify it fails correctly.
  - **GREEN:** Write the minimal code to pass (using Fake It, Obvious Implementation, or Triangulation).
  - **REFACTOR:** Clean up code and test code in separate cycles while keeping tests green.
  - **Verification:** Audits the code against the testing anti-patterns reference document.

### 6. `overpowered:tdd-agent-dispatch`
* **Purpose:** Agent handoff.
* **Function:** Generates isolated task briefings (prompts) for fresh subagents. Each prompt encapsulates the global context, relevant acceptance criteria, and a specific vertical slice, instructing the new agent to execute the `tdd-cycle` skill in isolation.

---

## Core Rules

1. **The Iron Law:** No production code is written without a failing test first. If you write code without a test, you must delete it and start over.
2. **The Beyonce Rule:** If the behavior is important enough to exist, it must have an explicit test.
3. **The Separation Rule:** Keep design refactorings and feature implementation in separate commits/PRs.
4. **No Mock Testing Anti-Patterns:** Never assert on the existence or structure of mocks. Mock actual external boundaries only when necessary and mirror real API completeness.
