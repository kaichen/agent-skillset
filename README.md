# Kai's Agent Skills

English | [中文](./README.zh-CN.md)

A collection of Agent Skills, could be used as Claude Code plugins.

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

**Official:**

| Repository | Description |
|------------|-------------|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic skills - document processing, creative design, MCP builders |
| [openai/skills](https://github.com/openai/skills) | Skills for Codex |

**Community Curated (Awesome Lists):**

| Repository | Description |
|------------|-------------|
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | Comprehensive catalog with categorized skills |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | Community skills collection |
| [VoltAgent/awesome-claude-skills](https://github.com/VoltAgent/awesome-claude-skills) | Partner and community contributions |
| [BehiSecc/awesome-claude-skills](https://github.com/BehiSecc/awesome-claude-skills) | Curated skills list |

**Community Featured Skills:**

| Repository | Description |
|------------|-------------|
| [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | Vercel's official agent skills for React/Next.js and Web Design |
| [huggingface/skills](https://github.com/huggingface/skills) | HuggingFace ML/AI focused skills |
| [trailofbits/skills](https://github.com/trailofbits/skills) | Security-focused skills from Trail of Bits |
| [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | Obsidian knowledge management skills |
| [K-Dense-AI/claude-scientific-skills](https://github.com/K-Dense-AI/claude-scientific-skills) | Scientific research and analysis skills |
| [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | UI/UX design with 50+ styles and multi-framework support |

## My Recommendations

Two skills I personally use daily and highly recommend installing to user scope:

| Skill | Description |
|-------|-------------|
| [planning-with-files](https://github.com/OthmanAdi/planning-with-files) | Manus-style file-based planning for complex tasks |
| [brainstorming](https://github.com/obra/superpowers/blob/main/skills/brainstorming/SKILL.md) | Explores user intent and requirements before implementation |

**Install to user scope (`~/.claude/skills/`):**

```bash
# planning-with-files - clone as plugin or download skill directly
gh repo clone OthmanAdi/planning-with-files ~/.claude/skills/planning-with-files

# brainstorming - download single skill from superpowers repo
# (superpowers contains many skills, only install what you need)
mkdir -p ~/.claude/skills/brainstorming
gh repo view obra/superpowers --raw skills/brainstorming/SKILL.md > ~/.claude/skills/brainstorming/SKILL.md
```

> **Why user scope?** Skills in `~/.claude/skills/` are available globally across all projects, perfect for general-purpose workflows like planning and brainstorming.

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
