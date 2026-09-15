# Kai's Agent Skills

A collection of Agent Skills, installable with the `skills` CLI (`npx skills`).

## Skills

| Skill | Description |
|-------|-------------|
| [codebase-fact-check](./skills/codebase-fact-check) | Source-backed codebase review and audit with exact file/function references |
| [comeon](./skills/comeon) | 鼓励模型 |
| [discover-skills](./skills/discover-skills) | Discover available skills and popular collections |
| [grok-search](./skills/grok-search) | Search and research using Grok AI via browser automation |
| [herdr-orchestration](./skills/herdr-orchestration) | Orchestrate multiple agents via Herdr terminal multiplexer |

## Install

Install with the [skills CLI](https://github.com/vercel-labs/skills) (no global install needed, works with Claude Code, Cursor, Copilot and other agents):

```bash
# Interactive: pick skills and target agents
npx skills add kaichen/agent-skillset

# List available skills in this repo
npx skills add kaichen/agent-skillset --list

# Install a specific skill
npx skills add kaichen/agent-skillset --skill codebase-fact-check
npx skills add kaichen/agent-skillset --skill comeon
npx skills add kaichen/agent-skillset --skill discover-skills
npx skills add kaichen/agent-skillset --skill grok-search
npx skills add kaichen/agent-skillset --skill herdr-orchestration
```

Manual install also works — copy a skill folder into your agent's skills directory (e.g. `.claude/skills/` for project scope, `~/.claude/skills/` for user scope):

```bash
mkdir -p ~/.claude/skills/discover-skills
gh repo view kaichen/agent-skillset --raw skills/discover-skills/SKILL.md > ~/.claude/skills/discover-skills/SKILL.md
```

## License

MIT
