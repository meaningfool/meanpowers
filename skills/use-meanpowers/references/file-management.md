# Meanpowers File Management

Meanpowers artifacts live under `docs/meanpowers`.

## Canonical Layout

```text
docs/meanpowers/
  inbox/
    INB-0001_short-title.md
    INB-0002_short-title.md

  01_short-title/
    INB-0001_short-title.md
    010_shaping_short-title.md
    010_spike_topic.md
    011_spec_first-slice-group.md
    011_plan_first-slice-group.md
    012_spec_second-slice-group.md
    012_plan_second-slice-group.md
```

## Naming Rules

- Inbox files use global IDs: `INB-0001_short-title.md`.
- Work item folders use global IDs: `01_short-title/`.
- Slugs are short, lowercase, and hyphenated.
- When an inbox item becomes a work item, move the inbox file into the work item folder. Do not duplicate it.
- Shaping files use the work item prefix: `010_shaping_short-title.md`.
- Spike files use the work item prefix: `010_spike_topic.md`.
- Spec/plan pairs use incrementing three-digit prefixes inside the work item folder:
  - `011_spec_first-slice-group.md`
  - `011_plan_first-slice-group.md`
- A plan mirrors its matching spec by replacing `_spec_` with `_plan_`.

## ID Selection

- For a new inbox item, inspect `docs/meanpowers/inbox/` and existing work item folders for the highest `INB-####` ID, then use the next number.
- For a new work item folder, inspect `docs/meanpowers/` for numeric folders such as `01_short-title/`, then use the next number.
- For a new spec in a work item folder, inspect existing `*_spec_*.md` files and use the next available three-digit prefix for that work item.

## Validation Checklist

Before writing or moving artifacts, verify:

- the next ID is correct
- the slug style is consistent
- promoted inbox items are moved, not duplicated
- plan/spec names match
- phase skills are not repeating a conflicting file tree
