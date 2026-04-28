# Spec: [Title]

## Source

- Work item:
- Shaping doc/slice/subset, if any:

## Objective

[What change this spec introduces. State the intended outcome, not the implementation task list.]

## Non-Goals

[What this spec explicitly does not change.]

- In scope:
- Out of scope:
- Existing behavior to preserve:

## Baseline

[What the system does now, only as much as needed to explain why this change matters.]

- Current behavior/workflow/interface:
- Current data shape or internal structure, if relevant:
- Current limitation, risk, or user/operator pain:

## Target System

[What the target system must do or become after this work. Be specific enough that an implementation plan can preserve the contract without reinterpreting intent.]

- User/operator/API/maintainer-visible behavior:
- Internal structure, module boundaries, or data contracts:
- Error handling and edge cases:
- Compatibility, migration, observability, or operational constraints:

## Design And Implementation Constraints

[Decisions that affect implementation but belong in the contract.]

- Must preserve:
- Must use or reuse:
- Must not introduce:
- Constraints inherited from shaping, if any:

## Slices

[Use only if sequencing is needed. For small work, use one slice.]

### Slice 1: [Name]

**Behavioral delta:**

[What is observably different after this slice.]

**Acceptance Gates**

These gates define completion. If any gate fails or is not run, this slice is incomplete.

### Gate 1: [Name]

**Why this gate matters:**

[The risk or intended outcome this gate protects.]

**Criteria:**

- [Actor/trigger/context: what happens or who acts.]
- [Expected output/state/artifact: what must be visible, returned, persisted, emitted, or structurally true.]
- [Preservation or exclusion: what existing behavior, shape, or non-goal remains unchanged.]

**Proof approach:**

[Browser / CLI / backend test / integration test / replay / static inspection / live validation / manual procedure. Name the smallest realistic proof type; exact commands belong in the plan.]

**Expected evidence:**

[What the implementation agent must show before calling this complete: screenshot, trace, command output, test result, generated artifact, code reference, or manual procedure result.]

**Supporting Verification**

Useful checks that do not define completion.

- [Useful check, or "None beyond acceptance gates."]

## Decisions

- [Decision made, tradeoff accepted, and rejected option or alternative.]

## Handoff To Plan

- Approved by user: [yes/no]
- Slices ready for planning:
- Open questions blocking planning:
- Non-blocking questions for implementation:

If approved:

REQUIRED NEXT SKILL: `meanpowers:write-plan`
