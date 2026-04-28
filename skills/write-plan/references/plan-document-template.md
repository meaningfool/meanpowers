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

[Repeat this entire slice section for each slice from the spec. If the spec has one slice, include only Slice 1.]

**Behavioral delta from spec:**

[Copied or summarized from spec.]

**Acceptance Gates From Spec**

[Copy every acceptance gate for this slice unchanged. A slice may have one gate or many gates.]

### Gate 1: [Name copied unchanged]

**Why this gate matters:**
[Copied unchanged.]

**Criteria:**
- [Copied unchanged.]

**Proof approach:**
[Copied unchanged.]

**Expected evidence:**
[Copied unchanged.]

### Gate 2: [Name copied unchanged, if this slice has another gate]

[Repeat the same gate fields. Omit this example when the slice has only one gate.]

**Gate Execution**

- Gate 1:
  - Command/procedure: `[exact command, browser procedure, replay, static inspection, or manual procedure]`
  - Expected result: `[evidence that satisfies the spec's expected evidence]`
- Gate 2, if present:
  - Command/procedure: `[exact command, browser procedure, replay, static inspection, or manual procedure]`
  - Expected result: `[evidence that satisfies the spec's expected evidence]`

**Supporting Verification**

- [Useful check] - `...`

**Checkpoint**

Do not begin Slice 2 until every acceptance gate for Slice 1 has passed.

### Task 1.1: [Smallest coherent implementation increment]

[Include as many tasks as needed for this slice. Number tasks by slice: Task 1.1, Task 1.2, and so on. For Slice 2, use Task 2.1, Task 2.2, and so on.]

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

### Task 1.2: [Next smallest coherent implementation increment, if needed]

[Repeat the same task structure. Omit this example when Slice 1 has only one task.]

---

## Slice 2: [Name, if present]

[Repeat the full Slice 1 structure for each additional slice from the spec. Omit this section when the spec has only one slice.]
