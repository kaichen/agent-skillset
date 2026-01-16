# Agent Skillset Marketplace

A collection of Claude Code plugins and skills.

## Plugins

| Plugin | Description |
|--------|-------------|
| [analyze-claude-code](./plugins/analyze-claude-code) | Analyze Claude Code CLI source code |
| [discover-skills](./plugins/discover-skills) | Discover available skills and popular collections |

## What is Agent Skills?

[Agent Skills](https://agentskills.io) is an open standard for teaching AI agents specialized tasks. A skill is a folder containing instructions, scripts, and resources that agents load dynamically to improve performance.

**Key characteristics:**
- **Progressive disclosure** - Only metadata (~100 tokens) loaded initially; full content (<5k tokens) loads when relevant
- **Cross-platform** - Same standard works across Claude Code, Claude.ai, Codex, and other compatible agents
- **Composable** - Skills can reference other skills and resources

**Skill structure:**
```yaml
---
name: my-skill
description: When to trigger this skill
---
# Instructions for the agent
```

**Popular collections:**

| Repository | Description |
|------------|-------------|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic skills |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | Curated community catalog |
| [openai/skills](https://github.com/openai/skills) | Skills for Codex |

## Install

```bash
# Install a specific plugin
claude plugins marketplace add kaichen/agent-skillset

# Or install from GitHub
claude plugins add agent-skillset:analyze-claude-code
claude plugins add agent-skillset:discover-skills
```

## License

MIT
