# ICARM Skills

Shared [Agent Skills](https://developers.openai.com/codex/skills) for ICARM research workflows. Each skill is a folder under `skills/` containing a `SKILL.md`. The `SKILL.md` format is a cross-agent standard, so these work in both **Claude Code** and **OpenAI Codex CLI**.

## Skills

| Skill | Description |
|-------|-------------|
| `ae-setup` | Translates a mathematical idea, paper, or setting into a viable AlphaEvolve experiment. |

## Install — Claude Code

This repo is packaged as a Claude Code plugin with a marketplace catalog.

```
/plugin marketplace add icarm/skills
/plugin install icarm@icarm
```

Or from a local checkout:

```
/plugin marketplace add /path/to/icarm/skills
/plugin install icarm@icarm
```

Skills are namespaced as `icarm:<skill-name>` (e.g. `icarm:ae-setup`).

## Install — Codex CLI

Codex scans `.agents/skills/` directories. Clone the repo and link the skills into a scope Codex reads.

**User scope** (available in every repo):

```bash
git clone git@github.com:icarm/skills.git
mkdir -p ~/.agents/skills
ln -s "$(pwd)/skills/"* ~/.agents/skills/
```

**Project scope** (checked into a specific repo, shared with collaborators):

```bash
mkdir -p .agents/skills
ln -s /path/to/icarm/skills/skills/* .agents/skills/
```

Restart Codex to pick up new skills. Browse them with `/skills`, invoke one explicitly with `$ae-setup`, or let Codex select automatically based on the skill's description.

## Contributing

See [CLAUDE.md](CLAUDE.md) for repo structure and how to add a new skill.
