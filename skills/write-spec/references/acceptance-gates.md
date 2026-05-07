# Acceptance Gates

Acceptance gates translate intent into feedback an implementation agent can use. A good gate says what must be true, why it matters, and what evidence proves it.

## Definitions

- `Acceptance Gate`: a blocking completion checkpoint for a slice. If a gate fails or is not run, the slice is incomplete.
- `Acceptance Criterion`: one concrete condition inside a gate. It describes the intended change or preservation.
- `Acceptance Proof`: the runnable or inspectable evidence that proves the criterion.
- `Supporting Verification`: useful checks that improve confidence but do not define completion.

## Baseline And Target

`Baseline` is the current system behavior, interface, data shape, workflow, or internal structure near the requested change. Include only what is needed to explain what currently happens and why the requested change matters.

`Target System` is the intended post-change system. It may include user-visible behavior, API or CLI behavior, report output, data contracts, internal architecture, migration behavior, observability, or constraints that matter for implementation.

## Choosing Gates

Start by naming the slice outcome, not the test you expect to write.

Use the minimum number of gates needed to cover independent blocking outcomes.

Merge candidate gates when:
- they prove the same slice outcome
- they would normally pass or fail together
- one is only a different proof dimension of the other, such as protocol ordering, architectural boundary, or edge-case preservation within the same behavior

Split candidate gates when:
- they describe different actors or externally distinct outcomes
- one can fail while the other still passes
- the implementation could reasonably be complete for one outcome while unfinished for the other

For refactors or architecture slices, start with one gate named after the preserved or changed behavior, then add structural criteria inside that gate. Do not turn adapter boundaries, protocol ordering, or regression checks into separate gates unless they are independent outcomes.

## Good Proofs

A good proof is concrete enough that a planning agent can turn it into exact commands without inventing the test shape.

Each proof should answer:
- `Setup`: what environment, fixtures, fakes, or live systems are involved?
- `Action`: what exact interaction, command, or sequence is performed?
- `Assertions`: what exact output, ordering, state, or file contents are checked?
- `Evidence`: what must be reported back?

These are not sufficient by themselves:
- "backend acceptance test"
- "browser validation"
- "static inspection"

Those are categories, not proofs.

## Good Criteria

Good criteria are:

- concrete: they say exactly what must be true
- single-purpose: one condition per criterion
- actor-aware: the user, operator, API consumer, external system, or maintainer is clear
- output-aware: the visible state, response, file, event, persisted state, or structural boundary is clear
- testable: a proof can be written without reinterpreting the intent
- minimal: they cover the contract without duplicating every implementation detail

Avoid:

- vague adjectives: appropriate, reasonable, intuitive, clean, fast, robust
- passive phrasing that hides the actor or trigger
- criteria that only say "tests pass"
- implementation details when the work is user-facing and the user-visible outcome is what matters
- broad regression sweeps as the only proof of a specific behavior

## Proof Types

Use the smallest realistic proof that establishes the criterion.

- Browser or live validation: for UI flows, interactions, navigation, responsive behavior, or browser-facing workflows.
- Backend or integration test: for API behavior, persistence, jobs, events, service boundaries, or generated outputs.
- CLI command: for command-line tools, scripts, exit codes, generated files, or logs.
- Report or file inspection: for exports, generated reports, snapshots, transformed files, or artifacts.
- Replay or fixture: for deterministic reproduction of an input stream, bug, migration, or import/export scenario.
- Static inspection: for architecture, module boundaries, dependency removal, or refactoring constraints.
- Manual procedure: for behavior that cannot be automated yet, with exact setup, action, and expected evidence.

## Criteria Patterns

EARS-style criteria are useful when a trigger matters:

```text
WHEN [condition or event], THE SYSTEM SHALL [specific response].
```

Gherkin-style criteria are useful when setup/action/outcome is clearer:

```text
Given [context]
When [action]
Then [observable result]
```

Output-contract criteria are useful for reports, files, API responses, and generated artifacts:

```text
For [input/context], [output/artifact] contains [field/section/value] and excludes [non-goal].
```

Structural criteria are allowed when the purpose of the work is architectural or refactoring:

```text
[Module/layer] depends on [abstraction] and no longer imports [forbidden dependency].
```

## Examples

### UI

```markdown
### Gate 1: Invalid Login Shows Clear Feedback

**Why this gate matters:**
Users must understand why login failed without gaining access.

**Criteria:**
- When a user submits invalid credentials, the login page shows "Invalid email or password."
- The user remains logged out.
- The password field is cleared and the email field remains filled.

**Proof approach:**
Browser validation.

**Expected evidence:**
Screenshot or browser trace showing the failed login state and preserved email value.
```

### Report Output

```markdown
### Gate 1: Weekly Report Shows Risk Summary

**Why this gate matters:**
The report change is complete only if users can see the new risk information in the generated report.

**Criteria:**
- For a project with overdue tasks, the weekly report contains a "Risk summary" section.
- The section shows the number of overdue tasks.
- The section shows the oldest overdue date.
- For a project with no overdue tasks, the report shows "No overdue task risk."

**Proof approach:**
Generate or open weekly report fixtures for both project states.

**Expected evidence:**
The generated report output shows the expected section and values for both cases.
```

### API Or Backend

```markdown
### Gate 1: Cursor Pagination Returns Stable Pages

**Why this gate matters:**
API consumers need deterministic pagination without skipped or duplicated records.

**Criteria:**
- A request to `GET /api/users?limit=10` returns 10 users, `next_cursor`, and `has_more`.
- A request using the returned cursor returns the next 10 users.
- User objects keep the existing response shape.

**Proof approach:**
Backend integration test or CLI `curl` procedure.

**Expected evidence:**
Command output or test result showing both pages and unchanged user object fields.
```

### CLI Or Tooling

```markdown
### Gate 1: Import Command Writes Summary File

**Why this gate matters:**
Operators need a deterministic artifact after each import.

**Criteria:**
- When `voice-todos import sample.json` succeeds, it writes `import-summary.json`.
- The command exits with status 0.
- The summary contains imported count, skipped count, and error count.

**Proof approach:**
CLI command against a fixture.

**Expected evidence:**
Command output, exit status, and generated summary file contents.
```

### Refactor / Architecture

```markdown
### Acceptance Gate: CSV Import Preserves Operator Workflow Through The Shared Parser Boundary

**Why this gate matters:**
The refactor is complete only if the existing import workflow behaves the same for operators while the parsing logic moves behind a reusable boundary.

**Criteria:**
- When an operator runs the existing CSV import entrypoint with a valid file, the command reports the same imported-row summary and produces the same persisted records as before the refactor.
- When the CSV contains a malformed row, the command preserves the existing failure-reporting contract while continuing or stopping according to the current system rules.
- The import entrypoint depends on a shared parser interface, and the shared parsing core does not import CLI or persistence modules.

**Proof:**
- Setup: invoke the existing import entrypoint against fixed success and partial-failure fixtures, with a fake persistence adapter that records parsed rows.
- Action: run the import flow for both fixtures.
- Assertions: verify exit status, summary output, recorded rows, and code references showing that the entrypoint exercises the shared parser interface rather than concrete parsing or storage code.
- Evidence: named test cases or commands, asserted summary values, and code references for the boundary.
```

### Migration

```markdown
### Gate 1: Existing Records Migrate Without Data Loss

**Why this gate matters:**
The schema change is incomplete if existing user data cannot be read after migration.

**Criteria:**
- The migration converts existing records to the new schema.
- Records missing the new optional field remain readable.
- Running the migration twice does not duplicate or corrupt data.

**Proof approach:**
Migration fixture test.

**Expected evidence:**
Test output showing pre-migration fixture data, post-migration shape, and idempotent rerun.
```
