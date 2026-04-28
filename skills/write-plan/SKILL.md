---
name: write-plan
description: Use when creating an implementation plan from an approved Meanpowers spec, before handing execution to Superpowers
---

# Writing Plans

**Announce at start:** "I'm using the write-plan skill to operationalize the approved spec into an implementation plan."

## Input

`write-plan` requires a Meanpowers spec:
- If no spec is provided, ask which spec to use.
- Do not create a plan without a matching spec.

## Non-Negotiable Gate Rule

Acceptance gates are copied from the spec, including gate names, criteria, proof approaches, and expected evidence. The plan may add exact commands, scripts, browser procedures, or manual procedures for proving them, but it must not weaken, rename, invent, or silently change them.

If a gate cannot be operationalized and automated, stop and notify the user.

## Output

`write-plan` turns an approved Meanpowers spec into detailed implementation tasks.

Its role is to make the approved spec executable. It preserves the spec's `Acceptance Gates` as the completion contract, translates proof approaches into exact commands or procedures, adds supporting verification, and organizes the work into TDD-friendly tasks that can be handed to Superpowers execution.

Assume the plan will be handed to an engineer that has zero context for our codebase and questionable taste.

Document everything they need to know: which files to touch for each task, code, testing, docs they might need to check, how to test it. Give them the whole plan as bite-sized tasks. DRY. YAGNI. TDD. Frequent commits.

Assume they are a skilled developer, but know almost nothing about our toolset or problem domain. Assume they don't know good test design very well.

## Plan Creation Principles

Before defining tasks, map out which files will be created or modified and what each one is responsible for. This is where decomposition decisions get locked in.

- Design units with clear boundaries and well-defined interfaces. Each file should have one clear responsibility.
- Prefer smaller, focused files over large files that do too much.
- Files that change together should live together. Split by responsibility, not by technical layer.
- Follow established codebase patterns.
- Include targeted refactoring when it directly supports the current work.

This structure informs the task decomposition. Each task should produce self-contained changes that make sense independently.

## Acceptance Gates And Supporting Verification

Acceptance gates sit above TDD. They prove the slice is complete.

Supporting verification helps implementation confidence but does not define completion.

Each slice must include:

- `Acceptance Gates From Spec`, copied unchanged
- `Gate Execution`, with exact commands or procedures mapped to the spec's proof approaches and expected evidence
- `Supporting Verification`, with exact commands or procedures when known
- `Checkpoint`, requiring all slice gates to pass before the next slice begins

## Task Structure

- Tasks are the smallest implementation increments that can be identified while still leaving the codebase coherent after the task is complete.
- Number tasks by slice: `Task 1.1`, `Task 1.2`, then `Task 2.1`, `Task 2.2`, and so on.
- When a task changes testable behavior, use strict TDD: write the failing test, run it to confirm the expected failure, implement the smallest change, and run focused verification.
- For non-behavioral tasks, keep the same small-increment discipline and make the verification step explicit.
- Use exact code when it materially reduces ambiguity.
- Do not use placeholders like "add appropriate validation" or "handle edge cases."

**Each step is one action (2-5 minutes):**
- "Write the failing test" - step
- "Run it to make sure it fails" - step
- "Implement the minimal code to make the test pass" - step
- "Run the tests and make sure they pass" - step
- "Commit" - step

## Task Template

````markdown
### Task S.N: [Smallest coherent implementation increment]

**Purpose:**
[Why this task exists]

**Files:**
- Create:
- Modify:
- Test:

**Supports:**
- Acceptance Gate: Gate 1
- Supporting Verification:

- [ ] **Step 1: Write the failing test**

```python
def test_specific_behavior():
    result = function(input)
    assert result == expected
```

- [ ] **Step 2: Run test to verify it fails**

Run: `pytest tests/path/test.py::test_name -v`
Expected: FAIL because ...

- [ ] **Step 3: Write minimal implementation**

```python
def function(input):
    return expected
```

- [ ] **Step 4: Run test to verify it passes**

Run: `pytest tests/path/test.py::test_name -v`
Expected: PASS

- [ ] **Step 5: Run acceptance gate if this task completes it**

Run: `...`
Expected: ...

- [ ] **Step 6: Commit**

```bash
git add ...
git commit -m "..."
```
````

## Self-Review

Before saving the plan, verify:

- every acceptance gate from the spec appears unchanged, including criteria and expected evidence
- every gate has a command or procedure mapped to the spec's proof approach
- every command or procedure is realistic for the current project
- supporting verification is separate from acceptance gates
- tasks support the gates or verification they claim to support
- no placeholders remain
- file paths are exact
- commands have expected results
- no next slice begins before current slice gates pass
- the plan can be handed to `superpowers:executing-plans` without reinterpreting the spec

Fix issues inline before presenting the plan.

## File Operations

Follow the canonical Meanpowers file-management rules from `meanpowers:use-meanpowers`.

For this skill:
- create the matching plan file for the selected spec
- replace `_spec_` with `_plan_` in the filename
- do not change the spec file unless a gate must be revised

## Execution Handoff

After saving the plan, offer the default handoff:

```text
REQUIRED HANDOFF: superpowers:executing-plans
```

If the environment supports it well, this is also allowed:

```text
OPTIONAL HANDOFF: superpowers:subagent-driven-development
```
