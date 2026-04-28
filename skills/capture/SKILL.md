---
name: capture
description: Use when a conversation, transcript, or document contains multiple candidate project changes that need to be separated into independent Meanpowers inbox items
---

# Capture Changes

Capture is a lightweight demultiplexer. It turns messy input into independent Meanpowers inbox items.

It does not create work item folders, write specs, shape solutions, define acceptance gates, or plan implementation.

**Announce at start:** "I'm using the capture skill to separate candidate changes into Meanpowers inbox items."

## Output

Create one inbox file per validated change under `docs/meanpowers/inbox/`. Follow the canonical naming rules from `meanpowers:use-meanpowers` file-management reference:

```text
INB-0001_short-title.md
```

## Process

1. Read the input conversation, transcript, or document.
2. Gather the context needed to understand item boundaries, by reading project files.
3. Extract candidate changes.
4. Split unrelated changes and keep tightly coupled changes together.
5. Ask immediate questions only when the answer changes how items should be split.
6. Present the proposed item list to the user.
7. Revise the list until the user approves it.
8. Write one inbox file per approved item.

<HARD-GATE>
Do not write inbox files until the user has approved the proposed item list.
</HARD-GATE>

## Item Format

Present each proposed item in this shape:

```text
CHANGE N
Baseline: 1-2 short sentences
Target: 1-2 short sentences
Intent: 1 sentence
Scope boundary: Included / excluded, if useful
Questions for later: Non-blocking questions for shape/write-spec, if any
```

Use `Questions for later` for downstream uncertainties that do not affect the item split. Ask the user now only when the answer changes the item boundary.

## Boundary Self-Review

Before presenting the item list, check:

- Are unrelated changes split?
- Are tightly coupled changes kept together?
- Is each item understandable without the original conversation?
- Did capture avoid spec, design, acceptance-gate, and planning detail?

If the review changes the item boundaries, update the list before presenting it.

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
