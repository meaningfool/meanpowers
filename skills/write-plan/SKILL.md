---
name: write-plan
description: Use when creating an implementation plan from an approved Meanpowers spec, before handing execution to Superpowers
---

# Writing Plans

`write-plan` turns an approved Meanpowers spec into detailed implementation tasks.

It does not decide what done means. Done is defined by the spec's `Acceptance Gates`, including their criteria, proof approaches, and expected evidence. This skill copies those gates unchanged, operationalizes proof approaches with commands or procedures, adds supporting verification, and organizes implementation into TDD-friendly tasks.

**Announce at start:** "I'm using the write-plan skill to operationalize the approved spec into an implementation plan."

## Input

`write-plan` requires an approved Meanpowers spec.

If no spec is provided, ask which spec to use. Do not create a plan without a matching spec.

If the spec is not approved or has unresolved acceptance gates, stop and return to `meanpowers:write-spec`.

Approval must be explicit in the spec or conversation. Do not infer approval from the fact that a draft spec exists.

## Non-Negotiable Gate Rule

Acceptance gates are copied from the spec, including gate names, criteria, proof approaches, and expected evidence. The plan may add exact commands, scripts, browser procedures, or manual procedures for proving them, but it must not weaken, rename, invent, or silently change them.

If a gate cannot be operationalized, stop and revise the spec before planning.

## Output

Write an implementation plan that includes:

- spec contract
- non-goals and design constraints from the spec
- acceptance gates copied from the spec, including criteria and expected evidence
- gate execution commands or procedures
- supporting verification
- detailed tasks with files and steps
- per-task `Supports` links to gates or supporting verification
- checkpoint rule before moving to the next slice
- Superpowers execution handoff

## Plan Creation Principles

Before defining tasks, map out which files will be created or modified and what each one is responsible for. This is where decomposition decisions get locked in.

- Design units with clear boundaries and well-defined interfaces.
- Prefer smaller, focused files over large files that do too much.
- Files that change together should live together.
- Follow established codebase patterns.
- Include targeted refactoring when it directly supports the current work.

## Acceptance Gates And Supporting Verification

Acceptance gates sit above TDD. They prove the slice is complete.

Supporting verification helps implementation confidence but does not define completion.

Each slice must include:

- `Acceptance Gates From Spec`, copied unchanged
- `Gate Execution`, with exact commands or procedures mapped to the spec's proof approaches and expected evidence
- `Supporting Verification`, with exact commands or procedures when known
- `Checkpoint`, requiring all slice gates to pass before the next slice begins

## Task Structure

Keep tasks detailed and TDD-friendly. A task should be self-contained enough to execute without guessing.

Each task must include:

- purpose
- files to create, modify, or test
- what acceptance gate or supporting verification it supports
- bite-sized steps
- commands and expected results where relevant

Use exact code when it materially reduces ambiguity. Do not use placeholders like "add appropriate validation" or "handle edge cases."

## Task Template

````markdown
### Task N: [Component Name]

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

- [ ] **Step 3: Implement minimal code**

```python
def function(input):
    return expected
```

- [ ] **Step 4: Run focused verification**

Run: `pytest tests/path/test.py::test_name -v`
Expected: PASS

- [ ] **Step 5: Run acceptance gate if this task completes it**

Run: `...`
Expected: ...

- [ ] **Step 6: Commit checkpoint if appropriate**

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
