---
name: write-spec
description: Use when a change proposal, Meanpowers work item, or Meanpowers shaping output is scoped enough to define target behavior, non-goals, slices, and acceptance gates before implementation planning
---

# Writing Specs

`write-spec` turns a scoped change proposal, Meanpowers work item, or Meanpowers shaping output into a behavioral contract.

It defines what will change, what will not change, which design and implementation constraints matter, and which `Acceptance Gates` define done.

**Announce at start:** "I'm using the write-spec skill to define the behavioral contract and acceptance gates."

## Input

`write-spec` receives one scoped change proposal, work item, or Meanpowers shaping output. The input is ready for spec writing only when the user has made the target scope explicit enough to define behavior and acceptance gates.

Inputs may come from:

- a Meanpowers inbox item
- a Meanpowers shaping document
- a specific slice or work item within a Meanpowers shaping document
- another document that proposes changes, such as an audit, review, investigation, transcript, or project note
- the current conversation, if the user has already scoped the work clearly

If the user points to a Meanpowers shaping document, clarify which slice, work item, or scoped subset should be included in the spec when that is not already explicit.

## Core Terms

- `Baseline`: the current system behavior, interface, data shape, workflow, or internal structure near the requested change. Include only the parts needed to explain what currently happens and why the requested change matters.
- `Target System`: the intended post-change system, including behavior, outputs, interfaces, internal design choices, and constraints that matter for implementation.
- `Acceptance Gate`: a blocking completion checkpoint for a slice. If a gate fails or is not run, that slice is not complete.
- `Acceptance Criterion`: one concrete condition inside a gate. It describes what must be true from the perspective of a user, operator, external system, API consumer, or maintainer.
- `Acceptance Proof`: the runnable or inspectable evidence that proves the criterion.
- `Supporting Verification`: useful checks that improve implementation confidence but do not define done.

Use `references/acceptance-gates.md` for gate, criterion, proof, and example guidance.

## Process

Follow these steps in order. The subsections below are part of the process, not separate optional guidance.

### 1. Read Input, Understand Baseline, And Decide Whether To Recommend Shape

**Agent work:**
- Read the change proposal, work item, shaping output, or conversation scope.
- Inspect existing docs/code only enough to identify the affected system surface and current baseline.
- Decide whether the uncertainty is contained enough for `write-spec`, or broad enough to recommend `meanpowers:shape`.

Recommend `meanpowers:shape` only when uncertainty is likely to require broad exploration before a spec can be written:
- `Problem space broad`: the user need, operational pain, or reason for the change could imply substantially different outcomes.
- `Surface broad`: the affected product flow, API, report, data model, workflow, or subsystem cannot be narrowed to a contained area.
- `Direction broad`: the input requires choosing between substantially different product/workflow directions or system shapes.
- `Boundaries broad`: the input appears to bundle multiple independent changes or could split into meaningfully different work items.

If the uncertainty is specific and contained, stay in `write-spec` and resolve it through target-design questions.

**User interaction:**
- If recommending shape, present the recommendation and the criteria that triggered it.
- Ask the user to confirm the route.
- Only after the user confirms, use the skill tool to call `meanpowers:shape`.
- If not recommending shape, continue to target design without asking for route confirmation.

### 2. Design The Target With The User

**User interaction:**
- Interview the user relentlessly about every aspect of this scope until you reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.
- Ask the questions one at a time.
- Think of multiple approaches, repeatedly. What trade-offs do they reveal?
- Present options and the corresponding tradeoff conversationally with your recommendation and reasoning
- Lead with your recommended option and explain why
- If a question can be answered by exploring the codebase, explore the codebase instead.

Designing the target system includes internal structure, data contracts, migration choices, error handling, observability, compatibility, or constraints that shape implementation.

As the target takes shape, record selected approaches, rejected options and tradeoffs, constraints, non-goals, and deviations from shaping decisions. These feed the spec's `Target System`, `Non-Goals`, `Design And Implementation Constraints`, and `Decisions` sections.

#### Design Principles

- Break the system into smaller units that each have one clear purpose, communicate through well-defined interfaces, and can be understood and tested independently
- For each unit, you should be able to answer: what does it do, how do you use it, and what does it depend on?
- Can someone understand what a unit does without reading its internals? Can you change the internals without breaking consumers? If not, the boundaries need work.
- Smaller, well-bounded units are also easier for you to work with - you reason better about code you can hold in context at once, and your edits are more reliable when files are focused. When a file grows large, that's often a signal that it's doing too much.

### 3. Present The Target For Validation

**User interaction:**
- Once you believe most design decisions have been made, present the design
- Scale each section to its complexity: a few sentences if straightforward, up to 200-300 words if nuanced
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something doesn't make sense

Include non-goals and design constraints in the target presentation. Non-goals are what the spec explicitly does not change. Constraints are contract-relevant decisions from Step 2 that implementation must respect.

### 4. Define Slices

**Agent work:**
- Decide whether sequencing is needed. Do not force slices for small work.
- If the spec comes from shaping, use shaping slices as a starting point.
- If you refine, merge, or split shaping slices, briefly explain what changed and why.
- For each proposed slice, define the behavioral delta.

The behavioral delta says what becomes different after this slice. For user-facing work, prefer externally observable system behavior deltas. For refactors or architecture work, the delta may be a structural change plus preserved behavior.

**User interaction:**
- Present slices for validation when there is more than one slice, when sequencing is ambiguous, or when you changed shaping slices.
- Ask whether the slice boundaries and order look right before defining acceptance gates.

### 5. Define Acceptance Gates

**Agent work:**
- Use `references/acceptance-gates.md` while writing gates.
- Define acceptance gates for each slice.
- Define enough gates to prove the slice is complete, but avoid turning supporting checks into gates.

Each gate must include:
- why the gate matters
- criteria that state what must be true
- proof approach, such as browser, CLI, backend test, integration test, replay, static inspection, live validation, or manual procedure
- expected evidence the agent must produce before claiming completion

Criteria state the intended conditions. Proof approach states how those conditions can be proven. `meanpowers:write-plan` later turns proof approaches into exact commands or procedures.

**User interaction:**
- Ask targeted questions only when a criterion cannot be made concrete.
- Present gates for validation before moving to supporting verification.

### 6. Define Supporting Verification

**Agent work:**
- Define supporting verification separately from acceptance gates.
- Use supporting verification for checks that improve implementation confidence but do not define done.
- Prefer supporting verification for helper-level tests, adapter tests, type checks, fixture/replay checks, lint checks, and focused regression tests that do not prove the behavioral delta by themselves.
- Do not duplicate acceptance gates as supporting verification.

**User interaction:**
- Do not ask for validation by default.
- Ask only when a supporting check would add meaningful cost, slow feedback loops, or expand the implementation scope.

### 7. Self-Review

**Agent work:**
- Run an adversarial self-review against the spec before presenting it.
- Check especially for vague target language, missing non-goals, missing constraints, weak gates, missing proof approaches, placeholders, and implementation task steps.
- Fix issues inline before presenting the spec.

### 8. Present Final Spec For Approval

**User interaction:**
- Present the final spec for approval.
- Do not save the final spec until the user approves it.
- If the user requests changes, revise the relevant section and present it again.
- After approval, save the spec and state `REQUIRED NEXT SKILL: meanpowers:write-plan`.

## File Operations

Follow the canonical Meanpowers file-management rules from `meanpowers:use-meanpowers`.

For this skill:
- create the next spec file in the selected work item folder
- use the canonical spec prefix and slug rules
- do not save the final spec until the user approves it

## Handoff

After the user approves the spec and it is saved, state:

```text
REQUIRED NEXT SKILL: meanpowers:write-plan
```
