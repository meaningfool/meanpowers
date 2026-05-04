# Shaping Concepts

## System And Behavior

A software product is a system that actors interact with. A system has internal components and exposed interfaces. System behavior is the set of observable reactions to inputs and state.

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

**How to diplay R:**

Use the following format:

```markdown
| ID | Requirement | Status | Notes |
|---|---|---|---|
| R0 | Items are searchable from the index page | Core goal | |
| R1 | State survives page refresh | Must-have | |
```

## Journeys (J)

Journeys describe actor interactions with the system.
- Use IDs such as `J1`, `J1.1`, and `J2`.
- Good journey titles lead with a verb, identify the actor, and avoid jargon.

Diplay J using the following format:

```markdown
| ID | Journey / Step | Actor | Description |
|---|---|---|---|
| J1 | Create a report | back-office user | User creates a report from selected data. |
| J1.1 | Choose report inputs | back-office user | User selects the data range and filters. |
```

## Shapes (S)

Shapes are solution options or selected system forms. 
- Letters represent mutually exclusive top-level shape options. 
- Numbered IDs represent components.

Examples:

- `A`, `B`, `C`: top-level shape options
- `A1`, `A2`: components of Shape A
- `A2-A`, `A2-B`: alternative approaches to component A2


Diplay S using the following format:

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

## Avoid Tautologies Between R And S

Requirements state outcomes. Shapes describe solutions.

Bad:

```text
R17: Use Clerk for authentication
```

Better:

```text
R17: Only authenticated users can access full articles
A3: Clerk authentication workflow
```
