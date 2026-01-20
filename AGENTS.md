# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-20
**Commit:** eece8ba
**Branch:** main

## OVERVIEW

Claude Code plugin bundle providing Agent Skills for skill discovery, source analysis, and Grok browser integration. Documentation-only repo (no executable code).

## STRUCTURE

```
agent-skillset/
├── .claude-plugin/marketplace.json   # Bundle metadata for `claude plugins marketplace`
├── plugins/
│   ├── analyze-claude-code/          # Reverse-engineer Claude Code CLI
│   ├── discover-skills/              # Browse/search skill collections
│   └── grok-search/                  # Grok AI via Claude-in-Chrome MCP
└── README.md                         # Install instructions + skill ecosystem overview
```

## WHERE TO LOOK

| Task | Location | Notes |
|------|----------|-------|
| Add new plugin | `plugins/<name>/.claude-plugin/plugin.json` + `skills/<name>/SKILL.md` | Follow existing structure |
| Modify skill behavior | `plugins/*/skills/*/SKILL.md` | YAML frontmatter + markdown body |
| Update marketplace listing | `.claude-plugin/marketplace.json` | Add to `plugins` array |
| Understand skill ecosystem | `README.md` | Links to official/community collections |

## CONVENTIONS

- **Skill structure**: YAML frontmatter (`name`, `description`) + markdown instructions
- **Plugin structure**: `.claude-plugin/plugin.json` + `skills/` subdir
- **No executable code**: Pure documentation skills (SKILL.md files only)
- **Bilingual docs**: README.md (EN) + README.zh-CN.md (中文)

## ANTI-PATTERNS (THIS PROJECT)

- **Never add code files**: This is a docs-only skill bundle. No `.js`, `.ts`, `.py`.
- **Security notice for discover-skills**: Always review third-party skills before installing - treat SKILL.md as executable instructions.

## UNIQUE STYLES

- Skills reference external tools via MCP (e.g., `mcp__claude-in-chrome__*` for grok-search)
- analyze-claude-code uses CLI one-liners to download/format minified source
- discover-skills provides `gh` CLI patterns for dynamic skill discovery

## COMMANDS

```bash
# Install plugin from marketplace
claude plugins marketplace add kaichen/agent-skillset

# Install specific plugin directly
claude plugins add agent-skillset:analyze-claude-code
claude plugins add agent-skillset:discover-skills

# No build/test commands - documentation only
```

## NOTES

- **grok-search** requires Claude-in-Chrome MCP extension + grok.com login
- **analyze-claude-code** downloads ~10MB minified CLI bundle; use `js-beautify` to format
- Skill locations priority: `.claude/skills/` (project) > plugin bundles > `~/.claude/skills/` (user)
