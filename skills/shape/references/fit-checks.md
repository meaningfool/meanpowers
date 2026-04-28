# Fit Checks

The fit check compares shape options against requirements.

## Standard Fit Check

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

## Macro Fit Check

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
