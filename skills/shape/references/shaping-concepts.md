# Shaping Concepts

## System And Behavior

A software product is a system that actors interact with. A system has internal components and exposed interfaces. System behavior is the set of observable reactions to inputs and state.

## Artifact Model

Shaping has two core facets:

- `Requirements` (R): what must be true about the finished system.
- `Shapes` (S): possible concrete system forms and their components.

Shaping also uses supporting artifacts:

- `Context Log`: preferences, tradeoffs, uncertainties, risks, meta-process notes, decision criteria, and other important considerations that are not part of R or S.
- `Derived Actor Journeys`: actor interactions inferred from a specific shape. Use them to check whether a shape creates coherent user-facing behavior. They are not first-class shaping facets and may not apply cleanly in every context.

## Requirements (R)

**Instructions:**
Requirements describe what is needed, not how it will be implemented.
- Use IDs such as `R0`, `R1`, and `R2`.
- Each requirement has a status among: Core goal, Undecided, Must-have, Nice-to-have, Out
- Good requirement titles are concrete, human-readable assertions in the present tense.
- Avoid solution-in-disguise requirements.
- Do not put preferences, process gates, migration-cost preferences, or user trade-off rules into `R` unless they are restated as truths about the finished system.
- Prefer positive requirement phrasing.
- When the real intent is to exclude a capability, express the capability positively and mark its status as `Out` rather than writing a negative requirement.
- Keep negative phrasing only when the prohibition is itself the requirement, such as security, privacy, safety, or compliance rules.

**Phrasing guidance:**

Bad:
```text
R3: Independent browser sessions do not require shared cross-session coordination
R4: The system does not persist session state across reconnects
```

Better when the capability is intentionally excluded:
```text
R3: The hosted system coordinates state across browser sessions | Out
R4: Session state survives reconnects | Out
```

Better when independence is itself the desired system property:
```text
R3: Each browser session is handled independently | Must-have
```

Valid negative requirement when the prohibition is the behavior:
```text
R5: Audio recordings are not retained after session end | Must-have
```

**How to display R:**

Use the following format:

```markdown
| ID | Requirement | Status | Notes |
|---|---|---|---|
| R0 | Items are searchable from the index page | Core goal | |
| R1 | State survives page refresh | Must-have | |
```

## Shapes (S)

Shapes are solution options or selected system forms. 
- Letters represent mutually exclusive top-level shape options. 
- Numbered IDs represent components.

Examples:

- `A`, `B`, `C`: top-level shape options
- `A1`, `A2`: components of Shape A
- `A2-A`, `A2-B`: alternative approaches to component A2


Display S using the following format:

```markdown
| ID | Shape | Summary | Status |
|---|---|---|---|
| A | Server-side filtering | Filtering happens in the backend. | Candidate |
| B | Client-side filtering | Filtering happens in the browser. | Rejected |
```


Display a specific shape using the following format: 

```markdown
| ID | Component | Flag | Notes |
|---|---|:---:|---|
| A1 | Query parameter parser | | Reuses existing route state. |
| A2 | Filtered backend endpoint | WARNING | Mechanics need investigation. |
```

Use `WARNING` in component flags when the what is known but the how is still uncertain.

## Is a required solution part of R or S

If the user states: "We will use Clerk authentication" is it:
- An actual requirement?
- A research direction regarding the possible shapes?

Both are possible, and deciding requires clarifying with the user. Do they want:

```text
R17: Use Clerk for authentication
```

Or:

```text
R17: Only authenticated users can access full articles
[with Clerk considered as one of the shapes/components]
```

## Context Log

The `Context Log` serves as a place to collect important points made by the user that are not R nor S.

Use the Context Log for:

- Preferences that help choose between shapes.
- Tradeoffs and decision criteria.
- Uncertainties, risks, and assumptions.
- Meta-process notes about how shaping should proceed.
- Important points of view that should be preserved without becoming requirements.

Do not put finished-system behavior into the Context Log when it can be stated as a requirement. Do not put concrete system forms into the Context Log when they belong in S.

Context Log entries can be resolved or superseded as shaping progresses, but keep them visible when they explain why a shape was selected or rejected.

Display the Context Log using the following format:

```markdown

## Context Log

| ID | Point | Type | Object | Importance | Status | Notes |
|---|---|---|---|---|---|---|
| CL1 | [Short factual statement] | expectation \| uncertainty \| preference \| constraint \| risk \| other | meta \| shape | high \| low | active \| resolved \| superseded \| discarded |  |

```

## Derived Actor Journeys

Derived actor journeys describe actor interactions with the system. They are inferred from a specific shape and used as a coherence check.

- Use them when the shaped change affects actor behavior, workflows, or observable interactions.
- Do not force them when the shape is internal, infrastructural, or otherwise not naturally journey-shaped.
- Good journey titles lead with a verb, identify the actor, and avoid jargon.

Display derived actor journeys using the following format:

```markdown
| Journey / Step | Actor | Description |
|---|---|---|
| Create a report | back-office user | User creates a report from selected data. |
| Choose report inputs | back-office user | User selects the data range and filters. |
```
