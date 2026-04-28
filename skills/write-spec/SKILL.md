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

The process produces the spec template sections as it goes:

- Step 1 produces `Baseline` and the decision to continue with `write-spec` or route to `meanpowers:shape`.
- Step 2 produces `Target System`, `Non-Goals`, `Design And Implementation Constraints`, and `Decisions`.
- Step 3 produces validated target sections.
- Step 4 produces `Slices`.
- Step 5 produces `Acceptance Gates`.
- Step 6 produces `Supporting Verification`.
- Step 7 produces approval state and handoff.

### 1. Read Input, Understand Baseline, And Check Scope

Read the input change proposal, work item, shaping output, or conversation scope.

Read the docs, code, commit history, or existing artifacts only enough to understand how the system works and behaves in the vicinity of the requested change.

Reframe the requested change against the baseline:

```text
CHANGE {i}
Baseline: {1-2 short sentences}
Target: {1-2 short sentences}
Intent: {1 sentence}
-------
```

Start from what the input already tells you. Ask baseline questions only when the current behavior depends on user or product intent that the code cannot reveal.

After understanding the baseline, continue with `write-spec` when the work has a clear target and the remaining decisions can be resolved while writing the spec.

Route to `meanpowers:shape` when the work is either large or vague or high-uncertainty. If routing to shape, stop and say: `REQUIRED NEXT SKILL: meanpowers:shape`.

### 2. Design The Target With The User

**Designing the target:**
- Interview the user relentlessly about every aspect of this scope until you reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.
- Ask the questions one at a time.
- Think of multiple approaches, repeatedly. What trade-offs do they reveal?
- Present options and the corresponding tradeoff conversationally with your recommendation and reasoning
- Lead with your recommended option and explain why
- If a question can be answered by exploring the codebase, explore the codebase instead.

The target system is broader than user-visible behavior. It may include internal structure, data contracts, migration choices, error handling, observability, compatibility, or constraints that shape implementation.

Capture meaningful target decisions as you make them: selected approach, rejected options, tradeoffs, constraints, non-goals, and any deviation from shaping decisions. These decisions feed the spec's `Target System`, `Non-Goals`, `Design And Implementation Constraints`, and `Decisions` sections.

Design principles to use during target design:

- Break the system into smaller units that each have one clear purpose, communicate through well-defined interfaces, and can be understood and tested independently
- For each unit, you should be able to answer: what does it do, how do you use it, and what does it depend on?
- Can someone understand what a unit does without reading its internals? Can you change the internals without breaking consumers? If not, the boundaries need work.
- Smaller, well-bounded units are also easier for you to work with - you reason better about code you can hold in context at once, and your edits are more reliable when files are focused. When a file grows large, that's often a signal that it's doing too much.

### 3. Present The Target For Validation

**Presenting the target:**
- Once you believe most design decisions have been made, present the design
- Scale each section to its complexity: a few sentences if straightforward, up to 200-300 words if nuanced
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something doesn't make sense

Include non-goals and design constraints in the target presentation. Non-goals are what the spec explicitly does not change. Constraints are contract-relevant decisions from Step 2 that implementation must respect.

Examples:

- preserve a public API
- reuse an existing subsystem instead of introducing a new dependency
- preserve a storage format
- require browser live validation for browser-facing behavior
- exclude a compatibility mode
- keep provider-specific logic behind a named abstraction
- preserve a generated report schema except for the stated additions

Tactical execution details belong in `meanpowers:write-plan`, not in the spec.

### 4. Define Slices

Use slices only when sequencing is needed. Do not force slices for small work.

If the spec comes from shaping, shaping slices are a starting point. You may refine, merge, or split them, but do not silently change shaping decisions. Call out any deviation from the shaping document before asking for approval.

Every slice must have:

- behavioral delta
- acceptance gates with criteria and proofs
- supporting verification, if useful

The behavioral delta says what becomes different after this slice. For user-facing work, prefer externally meaningful deltas. For refactors or architecture work, the delta may be a structural change plus preserved behavior.

### 5. Define Acceptance Gates

Use `references/acceptance-gates.md` while writing gates.

Acceptance gates are blocking checkpoints. They combine intent and evidence so an implementation agent can tell whether the slice is complete.

Each gate should include:

- why the gate matters
- criteria that state what must be true
- proof approach, such as browser, CLI, backend test, integration test, replay, static inspection, live validation, or manual procedure
- expected evidence the agent must produce before claiming completion

If you cannot define gates clearly, ask clarifying questions or route back to `meanpowers:shape`.

Use the gate structure from the template:

- `Why this gate matters`
- `Criteria`
- `Proof approach`
- `Expected evidence`

Criteria state the intended conditions. Proof approach states how those conditions can be proven. `meanpowers:write-plan` later turns proof approaches into exact commands or procedures.

### 6. Define Supporting Verification

Define supporting verification separately from acceptance gates. Supporting verification improves implementation confidence but does not define done.

Examples:

- helper unit tests
- adapter tests
- type checks
- fixture/replay checks
- lint checks
- focused regression tests that do not prove the behavioral delta by themselves

### 7. Self-Review And Approval

Before asking for approval, verify:

- no placeholders remain
- every slice has a behavioral delta
- every slice has acceptance gates
- non-goals are explicit
- design and implementation constraints are captured
- supporting verification is separate from acceptance gates
- the spec contains no implementation task steps
- deviations from shaping are called out
- the user can tell exactly what proof is required before implementation can be called complete

Fix issues inline before presenting the spec.

Present the spec to the user for approval. Do not save the final spec until the user approves it.

After approval, save the spec and state `REQUIRED NEXT SKILL: meanpowers:write-plan`.

## File Operations

Follow the canonical Meanpowers file-management rules from `meanpowers:use-meanpowers`.

For this skill:

- create the next spec file in the selected work item folder
- use the canonical spec prefix and slug rules
- do not create a plan file
- do not save the final spec until the user approves it

## Handoff

After the user approves the spec and it is saved, state:

```text
REQUIRED NEXT SKILL: meanpowers:write-plan
```
