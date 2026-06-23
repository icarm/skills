# ICARM Skills

Plugin repository housing shared Claude Code skills for ICARM projects.

## Structure

```
.claude-plugin/plugin.json      — Plugin manifest
.claude-plugin/marketplace.json — Marketplace catalog (for /plugin marketplace add)
skills/<name>/SKILL.md          — One directory per skill (auto-discovered)
```

## Adding a new skill

1. Create `skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`) and markdown instructions
2. Optional: add `references/`, `scripts/`, `templates/` subdirectories for supporting files
3. Keep SKILL.md under 500 lines — move detailed reference material to `references/`

## Installing into a project

- **From the GitHub marketplace:** `/plugin marketplace add icarm/skills` then `/plugin install icarm@icarm`
- **From a local checkout:** `/plugin marketplace add /home/matt.linux/icarm/skills` then `/plugin install icarm@icarm`

Skills will be namespaced as `icarm:<skill-name>`.
