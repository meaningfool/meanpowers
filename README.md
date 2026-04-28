# Meanpowers

Meanpowers is a project-work definition skill suite for Codex. It builds on
Superpowers by handling the phases before implementation:

```text
conversation or document -> capture
inbox item -> shape or write-spec
shape -> write-spec
write-spec -> write-plan
write-plan -> Superpowers execution
```

Meanpowers owns:

- separating messy input into independent inbox items
- shaping large or vague work
- writing behavioral specs with acceptance gates
- writing implementation plans from approved specs

Superpowers owns:

- implementation execution
- TDD discipline during execution
- debugging
- verification before completion
- branch finishing and review workflows

For Meanpowers-managed work definition, use Meanpowers instead of
`superpowers:brainstorming` or `superpowers:writing-plans`. For implementation
handoff, default to `superpowers:executing-plans`.
