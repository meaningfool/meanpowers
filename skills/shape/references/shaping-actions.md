# Shaping Actions

## Generate Alternative Shapes or Components

**Prompt inspiration:**
- What radically different architecture could work?
- What component could be removed?
- What is the simplest functioning shape?
- Are we using existing libraries or vendors well?

**Instruction:**
If alternatives involve unfamiliar technology, check primary documentation before leaning on assumptions.

## Generate Alternative Journeys

**Prompt inspiration:**
- What parts of the journey may be overly complex? What are our options to simplify them?
- What would be the simplest version of this journey? 
- What would it mean to shift some responsibility from the actor to the system or from the system to the actor? Does it unlock new shape directions?
- What would it mean to prevent the user from having through that journey?

## Run a spike

- A spike is an investigation task used to learn how the existing system works or what mechanics are required to implement a component.
- Use a spike when there is uncertainty about mechanics, feasibility, or existing system behavior.

### File Rules

- Create spikes in the same work item folder as the shaping document.
- Use the canonical file-management rules in `../../use-meanpowers/references/file-management.md`.
- Use a filename such as `010_spike_topic.md`.
- Use `spike-document-template.md`.

### Good Spike Questions

Good questions reveal mechanics:

- Where is the current logic for X?
- What changes are needed to achieve Y?
- How does the system currently perform Z?
- Are there constraints that affect this approach?

Avoid:

- How long will this take?
- Is this hard?
- Yes/no questions that do not reveal mechanics.

### Shaping Doc Impact

Keep full investigation details in the spike file. In the shaping document, record only the spike's question, outcome, and impact on the shape.

## Challenge The Baseline

**Prompt inspiration:**
- How does the current system shape constrains our exploration? 
- Are these constraints actual requirements? And if so how necessary are they?
- What new tradeoffs may become available if we were to drop some of these constraints?

## Run an Adversarial Review

**Instruction:**
Review the shaping document with fresh eyes looking for:
- Reasonning/logic gaps
- Undocumented assumptions about the shape, its components, the actors, the constraints...
- Intrinsic knowledge is being relied on.

## Run a Fit Check
Run a fit check to identify gaps between R, J and S. Here are questions that it may help with:
- Which requirements lack a corresponding journey or shape component?
- Which shape components lack a requirement?
- Which journey requires a system behaviour that the shape does not fullfil?

### Standard Fit Check

Requirements are rows. Shape options are columns.

```markdown
## Fit Check

| Req | Requirement | Status | A | B | C |
|---|---|---|---|---|---|
| R0 | Items are searchable from index page | Core goal | PASS | PASS | PASS |
| R1 | State survives page refresh | Must-have | PASS | FAIL | PASS |
| R2 | Back button restores state | Must-have | FAIL | PASS | PASS |

**Notes:**
- A fails R2: [brief explanation]
- B fails R1: [brief explanation]
```

Rules:

- Always show full requirement text.
- Shape columns contain only `PASS` or `FAIL`.
- Put explanations in notes.
- If a shape passes all checks but still feels wrong, add the missing requirement and rerun the fit check.

### Macro Fit Check

Use only when explicitly useful for early, high-level shapes where mechanisms are still uncertain.

```markdown
## Macro Fit Check: R x A

| Req | Requirement | Addressed? | Answered? |
|---|---|:---:|:---:|
| R0 | Core goal description | YES | NO |
| R1 | Guided workflow | PARTIAL | NO |
| R2 | Agent boundary | NO | NO |
```

Rules:

- Show only top-level requirements.
- `Addressed?` can be `YES`, `PARTIAL`, or `NO`.
- `Answered?` can be `YES` or `NO`.
- Follow with a `Gaps` table when useful.

