---
name: shape
description: Use when a Meanpowers inbox item or proposed change is vague, large, high-uncertainty, or needs product/system design before writing a spec
---

# Shaping

`meanpowers:shape` core principle is that vague / large scopes of work are best refined by exploring together the problem and the potential solutions through an iterative process. 

`meanpowers:shape` takes an `inbox` item, a document or a discussion as input and produces a validated shaping document and final slices ready for `meanpowers:write-spec` as output. 

## Core Concepts

Shaping is an iterative problem/solution exploration that progressively populates and refines three connected facets:

- `Requirements` (R): outcomes, constraints, and qualities. Requirements describe what is expected be true, not how to implement it.
- `Shapes` (S): possible concrete system forms, and their components.

R and S start empty. The goal is to progressively fill and refine R/S to the point they are coherent, specific, and mutually consistent. 

Other concepts: 
- `Context Log`: a place to track other important considerations that are not part of R or S.
- `Journeys`: the description of the user journeys associated with a specific shape. 

Litmus test for `R`:
- If the statement can be checked by looking at the finished system's behavior, capability, or externally visible quality, it may belong in `R`.
- If the statement explains how to choose among solutions, what tradeoff to prefer, what complexity to avoid, or what proof is required before committing, it belongs to the `Context Log`.

Read about R/S conventions in `references/shaping-concepts.md` before getting started.

## Setup Artifact

Follow the canonical Meanpowers file-management rules in `../use-meanpowers/references/file-management.md`.

- Create or select the work item folder.
- If starting from an inbox item, move it into the work item folder.
- Create the shaping document named with the canonical shaping filename, such as `010_shaping_short-title.md`.


## Workflow

```text

Input
  -> Setup working log
  -> Compress the problem
  -> Sort the intake
  -> Shape
  -> Slice
  
```

## Compress the problem

**Process:**
- Compress the problem
- Verify the problem statement with the user 
- Iterate until agreement

**Compress the problem:**
- Restate the problem as a single sentence using the template: `How might we [do X]?`
- Avoid verbs like `explore`, `decide`, `shape` that qualify what we might `do` and instead directly state what `do` is. The shaping process is about identifying different ways to `do` X, which will help `decide` what we actually want to do.
- Good `How might we host this app on the edge?` / Bad: `How might we explore edge hosting options for this app?`
- Good: `How might we prevent the user from entering their payment details multiple times?` / Bad: `How might we decide which of [option A], [option B] we prefer to prevent users from entering their payment details multiple times`

## Sort the intake

The intake may be lengthy containing both important information and noise regarding the expected shape and requirements, as well as the shaping process itself. 

**Process:**
- Semantic triaging: triage assertions, expectations, preferences... expressed by the user in the intake
- Clarification: clarify with the user what they meant
- Presentation: present to the user

**Semantic triaging:**
- Extract a list of `semantically distinct points` in the intake, together with a `type`, an `object` and an estimated `importance`.
- `type`: in [`expectation`, `uncertainty`, `preference`, `constraint`, `risk`, `other`]
- `object`: in [`meta` if the point is about the shaping process, `shape` if the point if about the solution]
- `importance`: in [`high`, `low`]
- Order the list by descending importance.

**Clarification:**
For each point:
- Skip it if it was already clarified by earlier questions.
- Clarify or verify with the user what their intention was. 
- If the point may qualify as a requirement, verify with the user if you should add it to R.
- Otherwise decide if it's worth tracking in the `Context Log`, or just discarded as noise. 
- `decision`: in [`requirement`, `context_log`, `noise`]

**Presentation:**
- Present the semantic points to the user
- Ask if you can start the shaping process

```markdown

## Semantic triaging

| Point | `type` | `object` | `importance` |
|---|---|---|---|
| [Short factual statement extracted from the intake.] | expectation \| uncertainty \| preference \| constraint \| risk \| other | meta \| shape | high \| low |
| [Repeat for each semantically distinct point.] |  |  |  |

```


## Shaping

**Process:**
1. Ideation: generate 5-8 shape options
2. Clarification: run a clarification action
3. Follow through: follow through with the consequences of the newly gathered insights.
4. Termination: decide if a termination condition is met or go back to 2
5. Adversarial review

**Your role:**
1. You proactively guide the user through the process with suggestions and feedback.
2. You detect potential new requirements.
3. You capture changes to R / S / Context Log (IMPORTANT: always ask for user confirmation before changing any of the artefacts).
4. You collect evidence through research 


Mandatory actions:
- When a decision has been made regarding a modification of R or S, always return the modified table in full. Mark changed or added rows with `CHANGED:` at the start of the changed cell.
- When important shaping decisions are made (tradeoff, directions,...), update the working log when decisions are made.

### Ideation

We want to prevent premature convergence by generating a large set of diverse options from the beginning. 

**Process:**
1. Generation-lowTemp: generate 5+ options with low temperature techniques.
2. Generation-highTemp: generate 2+ options with high temperature techniques.
3. Collapse: collapse similar options into its most distinctive version
4. Selection: select a set of 5-8 options that capture the best the diversity generated. 

**Generation-lowTemp:**
- Prompts: 
  - Inversion: "What if we did the opposite?
  - Constraint removal: "What if budget/time/tech weren't factors?"
  - Audience shift: "What if this were for [different user]?"
  - Combination: "What if we merged this with [adjacent idea]?"
  - Simplification: "What's the version that's 10x simpler?"
  - 10x version: "What would this look like at massive scale?"
  - Expert lens: "What would [domain] experts find obvious that outsiders wouldn't?"
- Consider any option that the user previously mentioned / requested
- Search queries compatible with the stated problem / current baseline

**Generation-highTemp:**
- Challenge the baseline
- Search queries that ignore or contradict some aspects of the stated problem / current baseline.

**Collapse:**
- Inspect similar options together
- Can
TODO 

### Clarification

**Process:**
1. List and rank sources of uncertainty.
2. Choose an action to clarify the highest ranking source of uncertainty 

**List and rank sources of uncertainty:**
TODO

**Choose an action:**
1. `Ask the user a clarifying question`. Ask one at a time
2. `Research the codebase`
3. `Research on the internet`
4. `Run a spike` when there is uncertainty about mechanics, feasibility, or existing system behavior


### Follow through

**Process:**
1. Follow-up actions
2. Suggest a refinement to R/S
2. What are the consequences? 
2. If change in shape -> new journey?
2. Does it reveal any new option / gap / uncertainty / potential requirement?

### Termination

Terminate the Shaping phase if one of those 2 exit conditions is met:
1. You believe R/S are highly consistent and S is "final" in your opinion. Then ask the user if he agrees. 
2. The user tells you to move to slicing. Ask for confirmation that the user consider S final.

### Adversarial review

5. `Run an adversarial review` when shaping is quite advanced but may rely on hidden assumptions.
6. `Run a Fit Check` to identify gap between R, J, and S.
4. `Challenge the baseline` when the existing system silently imposes constraints that could be revisited.




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
