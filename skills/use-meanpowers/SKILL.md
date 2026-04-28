---
name: use-meanpowers
description: Use when starting a conversation in a project that uses Meanpowers, or when deciding whether work should go through Meanpowers capture, shape, spec, or plan routing
---

# Using Meanpowers

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific implementation task, skip this skill.
</SUBAGENT-STOP>

Meanpowers routes work-definition before implementation. It replaces `superpowers:brainstorming` and `superpowers:writing-plans` for Meanpowers-managed work definition, while Superpowers remains the execution layer.

## Workflow

```text
Messy input
  conversation, transcript, document, or meeting notes
  -> meanpowers:capture
  -> docs/meanpowers/inbox/INB-####_<slug>.md

Inbox item
  if vague, large, high-uncertainty, or design-heavy
    -> meanpowers:shape
    -> confirmed shaping doc and final slices
    -> meanpowers:write-spec
  if already scoped enough to define behavior and acceptance gates
    -> meanpowers:write-spec

Approved Meanpowers spec
  -> meanpowers:write-plan
  -> implementation plan with acceptance gates operationalized
  -> REQUIRED HANDOFF: superpowers:executing-plans
```

## Routing

- Use `meanpowers:capture` when a conversation, transcript, document, or meeting note contains multiple candidate project changes that need to become independent inbox items.
- Use `meanpowers:shape` when a Meanpowers inbox item or proposed change is vague, large, high-uncertainty, or needs product/system design before writing a spec.
- Use `meanpowers:write-spec` when a Meanpowers work item or shaped slice is scoped enough to define target behavior, non-goals, slices, and acceptance gates.
- Use `meanpowers:write-plan` when creating an implementation plan from an approved Meanpowers spec.

## Boundary With Superpowers

Meanpowers owns work definition:

- capture
- shape
- write-spec
- write-plan

Superpowers owns implementation execution:

- `superpowers:executing-plans` is the default handoff
- `superpowers:subagent-driven-development` is optional when the environment supports it well

If Superpowers is missing or not discoverable, warn the user before implementation handoff. Meanpowers can still define work, but it cannot complete the planned execution workflow without Superpowers.

## Artifacts

Meanpowers artifacts live under `docs/meanpowers`. Follow the canonical naming and movement rules in `references/file-management.md`.

## Cross-References

Use skill names, not file paths. Do not force-load another skill file. Use handoff labels only at phase boundaries:

- `REQUIRED NEXT SKILL`
- `REQUIRED HANDOFF`
- `OPTIONAL HANDOFF`
