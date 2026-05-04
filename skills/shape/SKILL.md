---
name: shape
description: Use when a Meanpowers inbox item or proposed change is vague, large, high-uncertainty, or needs product/system design before writing a spec
---

# Shaping

`meanpowers:shape` core principle is that vague / large scopes of work are best refined by exploring together the problem and the potential solutions through an iterative process. 

`meanpowers:shape` takes an `inbox` item, a document or a discussion as input and produces a validated shaping document and final slices ready for `meanpowers:write-spec` as output. 

## Core Concepts

Shaping is an iterative problem/solution exploration that progressively populates and refines three connected facets:

- Requirements (R): outcomes, constraints, and qualities. Requirements describe what is expected be true, not how to implement it.
- Journeys (J): successions of interactions between an actor and the system that lead to an actor's expected output. Multiple types of actors may interact with the system, and each have multiple different journeys (depending on the use cases or the context)
- Shapes (S): possible concrete system forms, and their components.

R/J/S start empty. The goal is to progressively fill and refine R/J/S to the point they are coherent, specific, and mutually consistent. Requirements should not hide solution choices. Shape components should trace back to requirements, journeys, constraints, or explicit user choices. 

Litmus test for `R`:
- If the statement can be checked by looking at the finished system's behavior, capability, or externally visible quality, it may belong in `R`.
- If the statement explains how to choose among solutions, what tradeoff to prefer, what complexity to avoid, or what proof is required before committing, it does not belong in `R` as written.

Read about R/J/S conventions in `references/shaping-concepts.md` before getting started.

## Setup Artifact

Follow the canonical Meanpowers file-management rules in `../use-meanpowers/references/file-management.md`.

- Create or select the work item folder.
- If starting from an inbox item, move it into the work item folder.
- Create the shaping document named with the canonical shaping filename, such as `010_shaping_short-title.md`.


## Workflow

```text

Input
  -> Setup working log
  -> Sort intake
  -> Shape
  -> Slice
  
```

## Intake Sorting

**Compress the problem:**
Extract from the input:
  - goals
  - journey expectations
  - shape expectations
  - constraints
  - non-goals
  - uncertainties

Be truthful to what is stated and what is not. Don't infer, or guess. 

**Present that to the user:**

Present the intake sorting in this format:

```markdown

**INTAKE READBACK**

**Goals**

- [Only goals stated or directly implied by the input.]
- If none: None stated.

**Journey Expectations**

- [Expected actor journeys, workflows, or use cases.]
- If none: None stated.

**Shape Expectations**

- [Expected solution directions, platforms, architectures, components, or implementation shapes.]
- If none: None stated.

**Constraints**

- [Boundaries, compatibility needs, policies, costs, deadlines, technical constraints.]
- If none: None stated.

**Non-Goals**

- [Things the input excludes or deprioritizes.]
- If none: None stated.

**Uncertainties**

- [Questions, unknowns, risks, ambiguities, or suspected blockers.]
- If none: None stated.

**Empty Starting Model**

R/J/S are currently empty. The intake readback is not the shaped solution.

**Suggested First Step**

[Propose one next step: a clarifying question, codebase research, external research, or a specific shaping action.]

```

## Shaping

IMPORTANT: shaping is an iterative and collaborative process. You are not allowed to change alter R/J/S without consulting with the user.

Shaping is a exploration / investigation loop: keep going until one of those 2 exit conditions is met:
1. You believe R/J/S are highly consistent and S is "final" in your opinion. Then ask the user if he agrees. 
2. The user tells you to move to slicing. Ask for confirmation that the user consider S final.

Actions you may run autonomously at any moment:
1. `Ask the user a clarifying question`. Ask one at a time
2. `Research the codebase` for additional insights. If a question may be answered by researching the codebase, start by researching the codebase.
3. `Research on the internet`. Even if you think you know about a technology, always confirm through a search. Besides good research is a source of opportunities, it may lead to new alternative shape ideas.
4. `Suggest a refinement` to R, J or S (add/remove/split/merge/edit/... items). Ask for confirmation before acting.

Actions you may suggest to the user, and run only once you have confirmation (mandatory read: `references/shaping-actions.md` for additional details):
1. `Generate alternative shapes or components` when the current shape feels too narrow or complex
2. `Generate alternative journeys` when the current journeys seem unintuitive.
3. `Run a spike` when there is uncertainty about mechanics, feasibility, or existing system behavior
4. `Challenge the baseline` when the existing system silently imposes constraints that could be revisited.
5. `Run an adversarial review` when shaping is quite advanced but may rely on hidden assumptions.
6. `Run a Fit Check` to identify gap between R, J, and S.
7. Any other course of action that you identify as the best next action in this exploration.

At any moment the user may 
- Provide feedback. Always process that first. Prioritize over anything else. 
- Ask you do display the R/J/S tables
- Request a specific shaping action.

Mandatory actions:
- When a decision has been made regarding a modification of R, J or S, always return the modified table in full. Mark changed or added rows with `CHANGED:` at the start of the changed cell.
- When important shaping decisions are made (tradeoff, directions,...), update the working log when decisions are made.

## Confirm final shape

- Before exiting the shaping phase, display R / J / S in full.
- Ask for the user confirmation that the shape is final.
- If not keep the shaping going.

## Slicing

**Definition:**
- A vertical slice introduces an observable behavior or journey change and can be demonstrated. 
- A horizontal slice only changes internals.

**Goal of slicing:**
- We slice in order to better manage the risks involved with large changes. Slicing in small increments allows to account for new information as it is discovered. 

**Slicing principles:**
- Slicing options represent different path from start to finish. Each path may be preferable under specific preferences. For example, for 2 paths going from S to F, one going through A another through B: 
  - S->A->F may be shorter in distance
  - S->B->F may have lower total elevation
  - While another S->C->F may be less risky
- Contrasting slicing options highlights what the available `optimization dimensions` are and questions their relative priority: how is minimizing the distance important with regards to minimizing total elevation, or risk-exposure?

**Good slicing traits:**
- Good slicing options have a clear and distinctive positioning with regards to how they do on each optimization dimension compared to other options. 
- Good slicing options have clear intermediate system states: if a slicing proposal stretches a component over multiple slices, it may be a signal that the component bundles mutliple responsibilities. Be ready to challenge the shape and the components. 
- Good slicing options are easily and unambiguously verifiable (success / total completion may not be confused with failure / partial completion)
- Slicing may be unbalanced. However, big slices are candidates for further slicing.

**Process:**
1. Identify at least 3 slicing options. Make them as different as possible. Discard variations around a shared rationale. Re-generate if they are too close.
2. Contrast slicing options and extract `optimization dimensions`
3. Self-review: can you generate more radical options. 
3. Present the slicing options to the user. Show the details for each slicing if the user asks for it. 
4. Process the user feedback and rework the slices with the user until they are satisfied. 

**How to display slicing options:**

```markdown

## Slicing options

**Compare & contrast slicing options:**
[Short plain-language paragraph contrasting options. What are the differences between them that make a difference. If the options do not clearly differ, they are probably variations of the same slicing logic]

**Optimization dimensions:**
[List of identified optimization dimensions: use plain language]

### Option 1: [Title]
- Rationale: [One sentence. State what this option optimizes for, compared to the other options. Use plain language. Highlight risk posture or priority, not implementation detail]
- Sequence: [explain why the slices happen in this order and what each slice makes possible for the next one. Focus on progression logic, not implementation detail.]
- Map: 

| Component | V1 | V2 | V3 |
|---|---:|---:|---:|
| B1 | X |  |  |
| B2 | X |  |  |
| B3 |  | X |  |

**V1**
- Slice type: [vertical/horizontal]
- Demo scenario: [if vertical: describe a user scenario, focus on what's new/different]
- Notes for `meanpowers:write-spec`

```

## Confirm Final Slices

After confirmation by the user that slices are final:
- render the working log into the final shaping artifact format using `references/final-shaping-document-template.md`
- save it over the shaping document
- recap the confirmed slices
- state `REQUIRED NEXT SKILL: meanpowers:write-spec`
