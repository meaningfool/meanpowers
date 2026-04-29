---
name: shape
description: Use when a Meanpowers inbox item or proposed change is vague, large, high-uncertainty, or needs product/system design before writing a spec
---

# Shaping

Shape is for converging from vague or large work toward a confirmed product and system direction. It is collaborative and iterative.

This skill is inspired by Ryan Singer's shaping methodology and Ryan's own shaping skill work: [shaping-skills](https://github.com/rjs/shaping-skills/tree/main) and [shaping](https://github.com/rjs/shaping-skills/tree/main/shaping).

Shape produces a validated shaping document and final slices ready for `meanpowers:write-spec`. It does not produce formal acceptance gates, implementation tasks, specs, or plans.

## References

Read only as needed:

- `references/shaping-concepts.md` for requirements, journeys, shapes, behavior, and slicing concepts
- `references/shaping-actions.md` for possible actions during the shaping loop
- `references/fit-checks.md` for fit check and macro fit check rules
- `references/spikes.md` for spike guidance
- `references/shaping-document-template.md` for the shaping artifact

## Workflow

```text
Input
  -> Setup artifact
  -> Establish baseline
  -> Seed R/J/S

Main shaping loop
  -> Choose next shaping action
  -> Apply the action
  -> Work through the result with the user, updating R/J/S until the model is internally consistent
  -> Render full R/J/S tables
  -> Run or update fit check when useful
  -> Examine what to do next and repeat until shape converges

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
  -> Save shaping document
  -> REQUIRED NEXT SKILL: meanpowers:write-spec
```

## Start

Shape expects a Meanpowers inbox item or a clearly proposed change as input.

If the user invokes shape on an unstructured conversation, transcript, or document, suggest `meanpowers:capture` first. If the user declines, use the conversation as the input and keep the scope explicit.

## Setup Artifact

Follow the canonical Meanpowers file-management rules from `meanpowers:use-meanpowers`.

- Create or select the work item folder.
- If starting from an inbox item, move it into the work item folder.
- Create the shaping document from `references/shaping-document-template.md`.
- Use the canonical shaping filename, such as `010_shaping_short-title.md`.

## Baseline

Gather only the baseline needed to reason about impacted behavior, journeys, and components:

- impacted actor journeys and current journey steps
- impacted observable system behaviors
- relevant current components and internal constraints

## Seed R/J/S

Create first versions of:

- R: requirements
- J: journeys
- S: shape options and components

Render complete tables when presenting them to the user. Do not summarize away rows that are part of the working model.

## Main Shaping Loop

In each loop:

1. Choose the next shaping action.
2. Apply the action.
3. Work through the result with the user, updating R/J/S until the model is internally consistent.
4. Render full updated R/J/S tables.
5. Run or update a fit check when comparing shape options.
6. Examine what to do next and repeat until shape converges.

Working through an action is not linear. Discussion may reveal missing requirements, changed journeys, revised shape components, rejected options, or new shaping actions. Update R/J/S as needed and check that the three facets still make sense together before presenting the full tables again.

When re-rendering a table after making changes, mark changed or added rows with `CHANGED:` at the start of the changed cell so the user can see what moved.

## Gate 1: Move To Final Slicing

Slicing can happen in two modes:

- Exploratory slicing: a shaping action inside the main loop.
- Final slicing: the confirmed slice set that will be handed to `meanpowers:write-spec`.

When the user asks to slice, clarify which mode they mean unless it is already obvious from context.

To cross this gate, the user only needs to confirm: "The shape is final."

## Slicing Loop

Create the smallest useful vertical slices. A vertical slice introduces an observable behavior or journey change and can be demonstrated:
- Slice vertically into slices way, way smaller than you otherwise would. Like, 10x smaller.
- When a small behavioural change still requires a significant amount of change in the system (e.g. adding a mobile native app), you may create intermediate slices that are mostly technical, as long as those slices produce a demoable output (e.g. a first slice with a mobile app that displays "Hello World", followed by slices integrating the UI and the data by chunks up to the point where it is actually usable)

For each slice, include:
- behavioral or journey delta
- included shape components
- demo scenario
- notes for `meanpowers:write-spec`

`demo scenario` describes the concrete scenario that we expect to be demonstrable after the slice.

## Gate 2: Confirm Final Slices

Do not hand off to `meanpowers:write-spec` until the user explicitly confirms the final slices.

After confirmation:

- update and save the shaping document
- recap the confirmed slices
- state `REQUIRED NEXT SKILL: meanpowers:write-spec`
