---
name: capture
description: Use when a conversation, transcript, or document contains multiple candidate project changes that need to be separated into independent Meanpowers inbox items
---

# Capture Changes

Capture is a lightweight demultiplexer. It turns noisy input into focused independent Meanpowers inbox items.

It does not create work item folders, write specs, shape solutions, define acceptance gates, or plan implementation.

**Announce at start:** "I'm using the capture skill to separate candidate changes into Meanpowers inbox items."

## Output

Create one inbox file per validated change under `docs/meanpowers/inbox/`. For canonical naming rules, read `../use-meanpowers/references/file-management.md` from this skill directory.

```text
INB-0001_short-title.md
```

## Process

1. Read the input conversation, transcript, or document.
2. Gather the context needed to understand item boundaries, by reading project files.
3. Extract candidate changes.
4. Split unrelated changes and keep tightly coupled changes together.
5. If several paths are alternative ways to achieve the same outcome, capture 1 umbrella item and move the path options into `Questions for later`.
6. Ask immediate questions only when the answer changes how items should be split.
7. Present the proposed item list to the user.
8. Revise the list until the user approves it.
9. Write one inbox file per approved item.

<HARD-GATE>
Do not write inbox files until the user has approved the proposed item list.
</HARD-GATE>

## Boundary Rules

Use 1 umbrella item when:

- the source is asking 1 product, research, or evaluation question and lists multiple possible ways to answer it
- several paths could be chosen later without changing the underlying intent
- a staged experiment is exploratory and later stages depend on what earlier stages reveal
- provider choices, hosting choices, or implementation strategies are still options rather than committed work

Split into separate items only when:

- the source clearly commits to multiple independent changes, not just multiple options
- each item could be approved, shaped, and specified independently if the others were dropped
- the items would still make sense as separate work if different people implemented them

When unsure, ask 1 boundary question: "Do you want one umbrella item for this question, or separate execution-track items?"

## Item Format

Present each proposed item in this shape:

```markdown
**CHANGE N**: [change title]

**Baseline:** 1 short sentence

**Target:** 1 short sentence

**Intent:** 1 sentence

**Questions for later:** Non-blocking questions for shape/write-spec, if any

---
```

- The `baseline` and the `target` are "states" of the system's behavior (and/or internals). Use present form. 
- Use `Questions for later` for downstream uncertainties that do not affect the item split. Ask the user now only when the answer changes the item boundary.

Example:
```markdown
**CHANGE N**: Add tags to bookmarks

**Baseline:** A user's bookmarks has a title and a creation date.

**Target:** A user can add tags when creating a bookmark.

**Intent:** Allow the user to navigate their bookmarks through tags.

**Questions for later:** Can the user change or remove tags after bookmark creation? Can the user manage the list of tags?

---
```

## Boundary Self-Review

Before presenting the item list, check:

- Are unrelated changes split?
- Are tightly coupled changes kept together?
- Are alternative implementation paths grouped under 1 umbrella item when they serve the same intent?
- Did capture avoid turning options, stages, or provider choices into separate items too early?
- Is each item understandable without the original conversation?
- Did capture avoid spec, design, acceptance-gate, and planning detail?

If the review changes the item boundaries, update the list before presenting it.

## Research-Style Inputs

If the source material is exploratory, default to the smallest set of items that preserves the actual decision surface.

- Capture the durable product question or requested outcome as the item.
- Put candidate approaches, trial order, and path-specific hypotheses into `Questions for later`.
- Only split once the source commits to multiple independent workstreams.

## Writing Inbox Files

For each approved item:

- create one file in `docs/meanpowers/inbox/`
- use the next `INB-####_<slug>.md` ID
- start with the approved item summary
- include relevant context, hypotheses, decisions, and questions for later
- do not create or move work item folders

After writing files, recap the created inbox items and likely next skills:

- `meanpowers:shape` for vague, large, high-uncertainty items
- `meanpowers:write-spec` for scoped items
