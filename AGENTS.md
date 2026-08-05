# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-20
**Commit:** eece8ba
**Branch:** main

## OVERVIEW

Agent Skills collection for skill discovery, source analysis, and Grok browser integration. Documentation-only repo (no executable code). Installed via the `skills` CLI (`npx skills add kaichen/agent-skillset`).

## STRUCTURE

```
agent-skillset/
├── skills/
│   ├── analyze-claude-code/SKILL.md   # Reverse-engineer Claude Code CLI
│   ├── discover-skills/SKILL.md       # Browse/search skill collections
│   └── grok-search/SKILL.md           # Grok AI via Claude-in-Chrome MCP
└── README.md                          # Install instructions + skill ecosystem overview
```

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Add new skill | `skills/<name>/SKILL.md` | YAML frontmatter + markdown body |
| Modify skill behavior | `skills/*/SKILL.md` | Keep frontmatter `name` matching folder name |
| Understand skill ecosystem | `README.md` | Links to official/community collections |

## CONVENTIONS

- **Skill structure**: `skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`) + markdown instructions
- **No plugin manifests**: No `.claude-plugin/` — plain Agent Skills layout compatible with `npx skills` and manual copy
- **No executable code**: Pure documentation skills (SKILL.md files only)

## ANTI-PATTERNS (THIS PROJECT)

- **Never add code files**: This is a docs-only skill bundle. No `.js`, `.ts`, `.py`.
- **Security notice for discover-skills**: Always review third-party skills before installing - treat SKILL.md as executable instructions.

## UNIQUE STYLES

- Skills reference external tools via MCP (e.g., `mcp__claude-in-chrome__*` for grok-search)
- analyze-claude-code uses CLI one-liners to download/format minified source
- discover-skills provides `gh` CLI patterns for dynamic skill discovery

## COMMANDS

```bash
# Install skills via the skills CLI
npx skills add kaichen/agent-skillset

# List / install specific skills
npx skills add kaichen/agent-skillset --list
npx skills add kaichen/agent-skillset --skill analyze-claude-code

# No build/test commands - documentation only
```

## NOTES

- **grok-search** requires Claude-in-Chrome MCP extension + grok.com login
- **analyze-claude-code** downloads ~10MB minified CLI bundle; use `js-beautify` to format
- Skill locations priority: `.claude/skills/` (project) > plugin bundles > `~/.claude/skills/` (user)
