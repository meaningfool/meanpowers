---
name: shape
description: Use when a Meanpowers inbox item or proposed change is vague, large, high-uncertainty, or needs product/system design before writing a spec
---

# Shaping

`meanpowers:shape` core principle is that vague / large scopes of work are best refined by exploring the problem and potential solutions together through an iterative process.

`meanpowers:shape` takes an `inbox` item, a document or a discussion as input and produces a validated shaping document and final slices ready for `meanpowers:write-spec` as output. 

## Core Concepts

Shaping is an iterative problem/solution exploration that progressively populates and refines two connected facets:

- `Requirements` (R): outcomes, constraints, and qualities. Requirements describe what is expected to be true, not how to implement it.
- `Shapes` (S): possible concrete system forms, and their components.

R and S start empty. The goal is to progressively fill and refine R/S to the point they are coherent, specific, and mutually consistent. 

Supporting artifacts:
- `Context Log`: a place to track preferences, tradeoffs, uncertainties, risks, meta-process notes, decision criteria, and other important considerations that are not part of R or S.
- `Derived Actor Journeys`: actor interactions inferred from a specific shape. Use them to check whether a shape creates coherent user-facing behavior. They are not first-class shaping facets and may not apply cleanly in every context.

Litmus test for `R`:
- If the statement can be checked by looking at the finished system's behavior, capability, or externally visible quality, it may belong in `R`.
- If the statement explains how to choose among solutions, what tradeoff to prefer, what complexity to avoid, or what proof is required before committing, it belongs to the `Context Log`.

Read about R/S and supporting artifact conventions in `references/shaping-concepts.md` before getting started.

## Setup Document

Follow the canonical Meanpowers file-management rules in `../use-meanpowers/references/file-management.md`.

- Create or select the work item folder.
- If starting from an inbox item, move it into the work item folder.
- Create the shaping document named with the canonical shaping filename, such as `010_shaping_short-title.md`.


## Workflow

```text

Input
  -> Compress the problem
  -> Sort the intake
  -> Shape
  -> Slice
  
```

## Compress the problem

**Process:**
- Restate the problem
- Sort the intake
- Present the problem statement and Context Log

### Restate the problem
- Restate the problem as a single sentence using the template: `How might we [do X]?`
- Avoid verbs like `explore`, `decide`, `shape` that qualify what we might `do` and instead directly state what `do` is. The shaping process is about identifying different ways to `do` X, which will help `decide` what we actually want to do.
- Good `How might we host this app on the edge?` / Bad: `How might we explore edge hosting options for this app?`
- Good: `How might we prevent the user from entering their payment details multiple times?` / Bad: `How might we decide which of [option A], [option B] we prefer to prevent users from entering their payment details multiple times`

### Sort the intake

The intake may be lengthy containing both important information and noise regarding the expected shape and requirements, as well as the shaping process itself. 

**Process:**
- Semantic triaging: triage assertions, expectations, preferences... expressed by the user in the intake
- Clarification: clarify with the user what they meant
- Presentation: present to the user

**Semantic triaging:**
- Extract a list of `semantically distinct points` in the intake, together with a `type`, an `object` and an estimated `importance`.
- `type`: in [`expectation`, `uncertainty`, `preference`, `constraint`, `risk`, `other`]
- `object`: in [`meta` if the point is about the shaping process, `shape` if the point is about the solution]
- `importance`: in [`high`, `low`]
- Order the list by descending importance.

**Clarification:**
For each point:
- Skip it if it was already clarified by earlier questions.
- Clarify or verify with the user what their intention was. 
- If the point may qualify as a requirement, verify with the user if you should add it to R.
- Otherwise decide if it's worth tracking in the `Context Log`, or just discarded as noise. 
- `decision`: in [`requirement`, `context_log`, `noise`]

### Presentation:
- Present the semantic points to the user
- Iterate with them as necessary

<HARD-GATE>
Do not generate shape options, solution directions, or implementation approaches until the user has explicitly confirmed the compressed problem statement.

If the user has not confirmed the `How might we ... ?` statement, stay in the Compress phase.
</HARD-GATE>

```markdown

## Compressed problem

**Problem statement:**
[Problem statement]

**Context Log:**
| Point | `type` | `object` | `importance` |
|---|---|---|---|
| [Short factual statement extracted from the intake.] | expectation \| uncertainty \| preference \| constraint \| risk \| other | meta \| shape | high \| low |
| [Repeat for each semantically distinct point.] |  |  |  |

```

## Shaping

**Process:**
1. Ideation: generate 5-8 shape options
2. Convergence: clarify or contrast options through successive conversation threads
3. Adversarial review

**Your role:**
1. You proactively guide the user through the process with suggestions and feedback.
2. You detect potential new requirements.
3. You capture changes to R / S / Context Log (IMPORTANT: always ask for user confirmation before changing any of the shaping records).
4. You collect evidence through research 


Mandatory actions:
- When a decision has been made regarding a modification of R or S, always return the modified table in full. Mark changed or added rows with `CHANGED:` at the start of the changed cell.
- When a decision has been made regarding a modification of the Context Log, always return the modified Context Log table in full. Mark changed or added rows with `CHANGED:` at the start of the changed cell.
- When important shaping decisions are made (tradeoff, direction, rejected option, selected option), update the shaping document when decisions are made.

### Ideation

We want to prevent premature convergence by generating a large set of diverse options from the beginning. 

**Process:**
1. Generate: generate 5+ `low-temperature` options and 3+ `high-temperature` options
2. Collapse: collapse similar options into their most distinctive version
4. Select: select a set of 5-8 options that best capture the diversity generated.

**Generate:**
- `low-temperature` options focus around the stated problem and the current baseline.
- `low-temperature` options explore logical and reasonable options, including those put forward by the user.
- `high-temperature` options focus on adjacent problems.
- `high-temperature` options challenge the stated problem and/or the current baseline to identify otherwise ignored directions.
- Use internet search creatively to expand your thinking

Here are some prompts to help you generate more diverse options: 
- What radically different architecture could work?
- What is the simplest functioning shape?
- Are we using existing libraries or vendors to their fullest?
- What would be the simplest relevant actor journey?
- What would it mean to shift some responsibility from the actor to the system or from the system to the actor?
- What new options would be available if we scraped the existing solution and started from scratch?

**Generation-highTemp:**
For high temperature idea generation, challenge the frame to generate new ideas, that may not be applicable but may be revealing:
- What if we did the opposite?
- What if we could change / remove significant parts of the current solution?
- Run search queries that ignore or contradict some aspects of the stated problem / current baseline.

### Convergence

**Goal:**
- The convergence phase aims at reducing the option space to a single well clarified option that will be accepted as the final shape. This happens through `contrasting` and `clarification` of existing options. 
- Yet, the overarching goal of the shaping process is to thoroughly explore the problem/solution space. So if some insights hint at new options distinctive from our existing set, we should pursue them, see `generation`.

**Process:**
1. Choose which `action type` from [`contrasting`, `clarification`, `generation`] is likely to generate the largest amount of new insights. 
2. Submit to the user 2 suggestions of [`action_type`, `action`]
3. Run the action decided by the user and `follow through`.
4. Decide if a `termination` condition is met or go back to 1.

**`contrasting`:**
- Contrasting options is how we discover what's important to the designer.
- Choose 2 options and ask: `Under which circumstances would [option A] be a better fit than [option B]? And the other way around.` 
- Output to the user the list of separate `context` within which each option would be better (ignore contexts where both would be roughly equivalent).
- Each `context` is a conjunctive set of at least one `condition`
- Present the result to the user as a starting point for the discussion.

Example:

```markdown

## Contrasting [option A] and [option B]

[option A] is a better fit:
- If there is a large number of transactions AND transactions may come from anywhere in the world
- If we assume that there will be a low rate of fraudulent transactions.

[option B] is a better fit:
- If the schema is expected to evolve 

```

**`clarification`:**
A clarification action answers questions and removes uncertainties regarding a specific shape option (S) or the requirements (R).

Action ideas:
1. `Ask the user a clarifying question`. Ask one at a time
2. `Research the codebase`
3. `Research on the internet`
4. `Run a spike` when there is uncertainty about mechanics, feasibility, or existing system behavior. Mandatory read before running a spike `references/spike.md`

**`generation`:**
- When a conversation reveals a gap in the option space, generate 3 distinctive options that may fill that gap.
- Example: 
  - A new requirement is identified `The payment system allows for a high number of parallel transactions`
  - And identified as a non-goal (`status`:`out`)
  - All existing options silently assumed the new requirement to be true.
  - There is a gap in the option space: "what would a solution that assumes a low number of parallel transactions look like?"

**`follow through`:**
Once a conversation started, see that it gets closure. To do that you may need to:
- Follow-up with new questions or actions
- Suggest a refinement to R/S
- Ask: What are the 2nd order consequences of modifying R/S? For example, what are the consequences on relevant derived actor journeys?
- Did we uncover new insights that may reveal any new option / gap / uncertainty / potential requirements?

**`termination`:**
Terminate the Shaping phase if one of these two exit conditions is met:
1. You believe R/S are highly consistent and S is "final" in your opinion. Then ask the user if they agree.
2. The user tells you to move to slicing. Ask for confirmation that the user considers S final.

### Adversarial review

**Instruction:**
Review the shaping document with fresh eyes looking for:
- Undocumented assumptions about the shape, its components, the actors, the constraints...
- Gaps between the shape and the requirements
- Missed opportunity for simplification: ask "What would be the simplest version of this shape?"

## Confirm final shape

- Before exiting the shaping phase, display R / S and the Context Log in full.
- Display derived actor journeys for the selected shape where relevant. If actor journeys do not apply cleanly, state why instead of forcing them.
- Ask for the user confirmation that the shape is final.
- If not, keep the shaping going.

## Slicing

**Definition:**
- A vertical slice introduces an observable behavior or journey change and can be demonstrated. 
- A horizontal slice only changes internals.

**Goal of slicing:**
- We slice in order to better manage the risks involved with large changes. Slicing in small increments allows to account for new information as it is discovered. 

**Slicing principles:**
- Slicing options represent different paths from start to finish. Each path may be preferable under specific preferences. For example, for two paths going from S to F, one going through A and another through B:
  - S->A->F may be shorter in distance
  - S->B->F may have lower total elevation
  - While another S->C->F may be less risky
- Contrasting slicing options highlights the available `optimization dimensions` and questions their relative priority: how important is minimizing distance compared with minimizing total elevation or risk exposure?

**Good slicing traits:**
- Good slicing options have a clear and distinctive positioning with regards to how they do on each optimization dimension compared to other options. 
- Good slicing options have clear intermediate system states: if a slicing proposal stretches a component over multiple slices, it may be a signal that the component bundles multiple responsibilities. Be ready to challenge the shape and the components. 
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
- render the confirmed shaping document into the final shaping document format using `references/final-shaping-document-template.md`
- save it over the shaping document
- recap the confirmed slices
- state `REQUIRED NEXT SKILL: meanpowers:write-spec`
