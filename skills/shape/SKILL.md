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

Read about R/J/S conventions in `references/shaping-concepts.md` before getting started.

## References

Read only as needed:

- `references/shaping-actions.md` for possible actions during the shaping loop
- `references/fit-checks.md` for fit check and macro fit check rules
- `references/spikes.md` for spike guidance

## Setup Artifact

Follow the canonical Meanpowers file-management rules in `../use-meanpowers/references/file-management.md`.

- Create or select the work item folder.
- If starting from an inbox item, move it into the work item folder.
- Create the shaping document named with the canonical shaping filename, such as `010_shaping_short-title.md`.


## Workflow

```text

  -> Sort intake

Main shaping loop
  -> Choose the next investigation step that most improves the R/J/S model
  -> Use shaping actions as prompts or techniques when useful
  -> Work through the result with the user
  -> Update the working log and any affected R/J/S tables
  -> Identify the next useful question, research task, fit check, spike, or convergence point
  -> Repeat until the shape converges

Gate 1: Move to final slicing
  -> If slicing is requested, clarify exploratory vs final unless obvious
  -> Cross this gate only when the user confirms the shape is final

Slicing loop
  -> Propose vertical slices
  -> Map each slice to behavior/journey change and shape components
  -> Discuss and revise slices with the user
  -> Render full slice table
  -> Repeat until slicing converges

Gate 2: Confirm final slices
  -> User explicitly confirms final slices
  -> Render and save final shaping document
  -> REQUIRED NEXT SKILL: meanpowers:write-spec
```

## Intake Sorting

- Sort the provided input into the facets it already contains:
  - goals
  - journey expectations
  - shape expectations
  - constraints
  - non-goals
  - uncertainties
- Present that to the user

Note: 
- Use this as a readback of the starting material. Be truthful to what is stated and what is not. Don't infer, or guess. 
- The first useful step may be to ask interpretation questions, explore a source-provided shape, extract requirements, generate alternative journeys, challenge the baseline, or run a fit check.

## Shaping

Shaping is a exploration / investigation loop: keep going until one of those 2 exit conditions is met:
1. You believe R/J/S are highly consistent and S is "final" in your opinion. Then ask the user if he agrees. 
2. The user tells you to move to slicing. Ask for confirmation that the user consider S final.

What you may do at any moment:
1. `Ask the user a clarifying question`. Ask one at a time
2. `Research the codebase` for additional insights. If a question may be answered by researching the codebase, start by researching the codebase.
3. `Research on the internet`. Even if you think you know about a technology, always confirm through a search. Besides good research is a source of opportunities, it may lead to new alternative shape ideas.
4. `Suggest a refinement` to R, J or S (add/remove/split/merge/edit/... items). Ask for confirmation before acting.

What you may suggest to the user (wait for confirmation before running):
1. `Generate alternative shapes or components` when the current shape feels too narrow or complex
2. `Generate alternative journeys` when the current journeys seem unintuitive.
3. `Run a spike` when there is uncertainty about mechanics, feasibility, or existing system behavior
4. `Challenge the baseline` when the existing system silently imposes constraints that could be revisited.
5. `Run an adversarial review` when shaping is quite advanced but may rely on hidden assumptions.
6. `Run a Fit Check` to identify gap between R, J, and S.
7. `Do a slicing dry run`, it may expose hidden tradeoffs or excessive scope.
8. Any other course of action that you identify as the best next action in this exploration.

At any moment the user may 
- Provide feedback. Always process that first. Prioritize over anything else. 
- Ask you do display the R/J/S tables
- Request a specific shaping action.

Mandatory actions:
- When a decision has been made regarding a modification of R, J or S, always return the modified table in full. Mark changed or added rows with `CHANGED:` at the start of the changed cell.
- When important shaping decisions are made (tradeoff, directions,...), update the working log when decisions are made.


Use `references/shaping-actions.md` for available shaping actions.

## Confirm final shape

- Before exiting the shaping phase, display R / J / S in full.
- Ask for the user confirmation that the shape is final.
- If not keep the shaping going.

## Slicing

**Definition:**
A vertical slice introduces an observable behavior or journey change and can be demonstrated. A horizontal slice only changes internals.

**Process:**
1. Slice vertically into slices way, way smaller than you otherwise would. Like, 10x smaller.
2. Try to identify multiple slicing logics. If you identify more than 1, submit the options to the user.
3. Show the slices to the user.
4. Process the user feedback and rework the slices with the user until they are satisfied.

**Notes:**
- When a small behavioural change still requires a significant amount of change in the system (e.g. adding a mobile native app), you may create intermediate slices that are mostly technical, as long as those slices produce a demoable output. To do that you may introduce transient UI elements that allow to demo the evolving system behavior (e.g. a first slice with a mobile app that displays "Hello World", followed by slices integrating the UI and the data by chunks up to the point where it is actually usable). 

**How to display a slice:**
For each slice, include:
- behavioral or journey delta
- included shape components
- `demo scenario`: describes the concrete scenario that we expect to be demonstrable after the slice.
- notes for `meanpowers:write-spec`

## Confirm Final Slices

After confirmation by the user that slices are final:
- render the working log into the final shaping artifact format using `references/final-shaping-document-template.md`
- save it over the shaping document
- recap the confirmed slices
- state `REQUIRED NEXT SKILL: meanpowers:write-spec`
