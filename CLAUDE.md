# ICARM Skills

Plugin repository housing shared Claude Code skills for ICARM projects.

## Structure

```
.claude-plugin/plugin.json   — Plugin manifest
skills/<name>/SKILL.md       — One directory per skill
```

## Adding a new skill

1. Create `skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`) and markdown instructions
2. Optional: add `references/`, `scripts/`, `templates/` subdirectories for supporting files
3. Keep SKILL.md under 500 lines — move detailed reference material to `references/`

## Installing into a project

From any ICARM project: `/install-plugin /home/matt.linux/icarm/skills`

Skills will be namespaced as `icarm:<skill-name>`.
