# project-spec-interrogator

A [Claude Code](https://claude.com/claude-code) skill that guides you through a structured interrogation to develop a well-defined project specification. It surfaces hidden assumptions, probes for gaps, challenges weak answers, and helps clarify goals before work begins.

Useful when starting a new project, when a project feels unclear, when scope is creeping, or when a vague idea needs shape.

## Install

Clone (or copy) this repo into your Claude Code skills directory:

```bash
git clone https://github.com/gniht/project-spec-interrogator.git \
  ~/.claude/skills/project-spec-interrogator
```

Then invoke it from any Claude Code session:

```
/project-spec-interrogator
```

Claude will also offer the skill automatically when your request matches its description (starting a new project, scoping, etc.).

## Files

- `SKILL.md` — the skill definition Claude Code loads
- `spec-template.md` — the spec document template produced at the end of an interrogation

## License

MIT — see [LICENSE](LICENSE).
