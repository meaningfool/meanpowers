# Installing Meanpowers For Codex

Meanpowers is intended to be edited from a project-local source tree and loaded through Codex native skill discovery.

## Prerequisites

- Git, if you want to sync Meanpowers changes to a remote repository.
- Superpowers installed and discoverable. Meanpowers uses Superpowers for
  implementation handoff, especially `superpowers:executing-plans`.

## Project-Local Installation

1. Place or clone Meanpowers at:

   ```bash
   .codex/meanpowers
   ```

2. Make sure the skills live under:

   ```bash
   .codex/meanpowers/skills
   ```

3. Create the Codex discovery symlink:

   ```bash
   mkdir -p .agents/skills
   ln -s ../../.codex/meanpowers/skills .agents/skills/meanpowers
   ```

4. Restart Codex so the skills are discovered.

## Superpowers Dependency

Meanpowers owns work definition: capture, shaping, spec writing, and
implementation planning. It does not execute implementation work itself.

Implementation handoff requires Superpowers. The default handoff is:

```text
superpowers:executing-plans
```

If Superpowers is missing or not discoverable, Meanpowers can still help define
work, but it must warn before implementation handoff because the required
execution skills are unavailable.

## Updating

Because Meanpowers is loaded through a symlink, edits under `.codex/meanpowers`
are picked up after Codex reloads skill metadata. Use normal git workflows in
the `.codex/meanpowers` source tree when syncing changes.
