# [Spec Title] Implementation Plan

> Execution default: use `superpowers:executing-plans`.

## Spec Contract

**Spec:** `docs/meanpowers/.../011_spec_x.md`

**Non-goals from spec:**

- [Copied from spec.]

**Design constraints from spec:**

- [Copied from spec.]

**Acceptance gate rule:**

Acceptance gates are copied from the spec. This plan may operationalize them with commands/procedures, but must not weaken, rename, or silently change them.

---

## Slice 1: [Name]

**Behavioral delta from spec:**

[Copied or summarized from spec.]

**Acceptance Gates From Spec**

### Gate 1: [Name copied unchanged]

**Why this gate matters:**
[Copied unchanged.]

**Criteria:**
- [Copied unchanged.]

**Proof approach:**
[Copied unchanged.]

**Expected evidence:**
[Copied unchanged.]

**Gate Execution**

- Gate 1:
  - Command/procedure: `[exact command, browser procedure, replay, static inspection, or manual procedure]`
  - Expected result: `[evidence that satisfies the spec's expected evidence]`

**Supporting Verification**

- [Useful check] - `...`

**Checkpoint**

Do not begin Slice 2 until every acceptance gate for Slice 1 has passed.

### Task 1: [Component Name]

**Purpose:**

[Why this task exists.]

**Files:**

- Create:
- Modify:
- Test:

**Supports:**

- Acceptance Gate: Gate 1
- Supporting Verification:

- [ ] **Step 1: Write the failing test**

Run or add the smallest test that proves the intended behavior for this task.

Expected: the test fails for the missing behavior.

- [ ] **Step 2: Run test to verify it fails**

Run: `[focused test command]`
Expected: FAIL because `[specific missing behavior]`

- [ ] **Step 3: Implement minimal code**

Modify only the files listed for this task unless the implementation reveals a necessary dependency.

- [ ] **Step 4: Run focused verification**

Run: `[focused test command]`
Expected: PASS

- [ ] **Step 5: Run acceptance gate if this task completes it**

Run/procedure: `[gate command or procedure]`
Expected: `[copied expected result]`

- [ ] **Step 6: Commit checkpoint if appropriate**

Use a commit only when the user requested commits or the execution workflow calls for it.
