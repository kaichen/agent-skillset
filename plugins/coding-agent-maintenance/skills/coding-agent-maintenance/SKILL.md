---
name: coding-agent-maintenance
description: Maintain, install, update, and configure AI coding agents on macOS. Use this skill whenever the user wants to upgrade coding agents, install a new agent, check agent versions, manage MCP servers, troubleshoot agent issues, or asks "how do I update claude/codex/gemini/amp/droid". Also trigger for any question about agent health, reinstalling, switching package managers, or managing agent skills/plugins. Covers: Claude Code, Codex, Gemini CLI, GitHub Copilot, Amp, Augment, Jules, Factory Droid, and more.
---

# Coding Agent Maintenance

## ⚠️ Self-Update Limitation

A coding agent **cannot update itself** from within its own session. The native self-updater replaces the running binary in-place, which kills the parent process (exit 137 / SIGKILL).

### Detect which agent you're currently inside

Walk up the process tree from the current shell — the agent binary will appear as a parent process:

```bash
pid=$$
while [ "$pid" -gt 1 ]; do
  comm=$(ps -p "$pid" -o comm= 2>/dev/null | tr -d ' ')
  echo "$pid $comm"
  ppid=$(ps -p "$pid" -o ppid= 2>/dev/null | tr -d ' ')
  [ "$ppid" = "$pid" ] && break
  pid=$ppid
done | grep -iE 'claude|codex|droid|amp|gemini|copilot|jules'
```

Example output when inside Claude Code:
```
15876 claude
```

This works universally across all agents — no env var knowledge needed. The agent binary name in the process tree is the ground truth.

**If the matched agent name == the agent you're about to update → exit this session first, then run the update from a plain terminal.**

---

## Quick Reference

```bash
# Check versions
claude --version ; codex --version ; gemini --version ; copilot --version ; jules version ; amp --version

# Built-in self-updaters — run from a plain terminal, NOT from inside the same agent
claude update ; codex update ; amp update ; droid update

# Update the rest via bun
bun add -g @augmentcode/auggie @github/copilot @google/gemini-cli @google/jules happy-coder opencode-ai @mariozechner/pi-coding-agent
```

---

## Agents Overview

| Agent | Binary | Package | Updater |
|-------|--------|---------|---------|
| Claude Code | `claude` | `@anthropic-ai/claude-code` | `claude update` / native installer |
| Codex | `codex` | `@openai/codex` | `codex update` |
| Amp | `amp` | `@sourcegraph/amp` | `amp update` |
| Factory Droid | `droid` | `@factory-ai/cli` | `droid update` |
| Gemini CLI | `gemini` | `@google/gemini-cli` | bun/npm |
| GitHub Copilot | `copilot` | `@github/copilot` | bun/npm |
| Google Jules | `jules` | `@google/jules` | bun/npm |
| Augment | `auggie` | `@augmentcode/auggie` | bun/npm |
| pi | `pi` | `@mariozechner/pi-coding-agent` | bun/npm |
| Happy Coder | `happy` | `happy-coder` | bun/npm |
| Opencode | `opencode` | `opencode-ai` | bun/npm |

---

## Install & Update

### Claude Code

```bash
# Native installer (recommended — avoids node path issues):
curl -fsSL https://claude.ai/install.sh | bash

# Migrate from npm to native:
claude migrate-installer        # or: npm uninstall -g @anthropic-ai/claude-code first

# Update:
claude update
/Users/kaichen/.claude/local/claude update   # if binary not in PATH

# Pin a specific version:
npm i -g @anthropic-ai/claude-code@2.0.23

# Health check:
claude doctor
```

### Factory Droid

```bash
# Install:
curl -fsSL https://app.factory.ai/cli | sh

# Update:
droid update
```

### All others — bun (preferred) / npm

```bash
# Install / upgrade via bun:
bun add -g @openai/codex @sourcegraph/amp @google/gemini-cli @github/copilot @google/jules @augmentcode/auggie

# Switching from npm → bun (run once):
npm uninstall -g @anthropic-ai/claude-code @augmentcode/auggie @github/copilot @google/gemini-cli @google/jules @sourcegraph/amp happy-coder opencode-ai
bun add -g @augmentcode/auggie @github/copilot @google/gemini-cli @google/jules happy-coder opencode-ai @mariozechner/pi-coding-agent

# oh-my-opencode — installs & configures multiple agents at once:
bunx oh-my-opencode install --no-tui --claude=max20 --chatgpt=yes --gemini=yes
```

---

## MCP Management

MCP servers are shared across agents (same URLs), but each agent has its own CLI syntax.

### Claude

```bash
# HTTP transport (remote, no local process):
claude mcp add --transport http context7 https://mcp.context7.com/mcp
claude mcp add --transport http exa_websearch 'https://mcp.exa.ai/mcp?tools=web_search_exa'
claude mcp add --transport http grep https://mcp.grep.app

# stdio transport (local process):
claude mcp add --scope project --transport stdio codex -- codex mcp-server
claude mcp add playwright -- npx @playwright/mcp@latest
claude mcp add context7 -- npx -y @upstash/context7-mcp --api-key <KEY>

# JSON (advanced):
claude mcp add-json auggie-mcp --scope user '{"type":"stdio","command":"auggie","args":["--mcp"]}'

claude mcp list
claude mcp remove context7
```

### Codex

```bash
# HTTP transport only (--url flag):
codex mcp add context7 --url https://mcp.context7.com/mcp
codex mcp add exa_websearch --url 'https://mcp.exa.ai/mcp?tools=web_search_exa'
codex mcp add grepapp --url https://mcp.grep.app
codex mcp list
```

### Droid

```bash
droid mcp    # interactive MCP management
```

---

## Config Files

```bash
# Claude
~/.claude/settings.json
~/.claude/CLAUDE.md              # global instructions

# Codex
~/.codex/config.toml             # main config
~/.codex/AGENTS.md               # default instructions
~/.codex/auth.json               # auth token

# Multiple Codex accounts
mkdir -p ~/.codex/accounts
cp ~/.codex/auth.json ~/.codex/accounts/myaccount.json

# Gemini
~/.gemini/antigravity/skills/    # skills directory
```

---

## Skills & Plugins

```bash
# Claude
ls ~/.claude/skills/
claude plugin install <name>@<marketplace>
claude plugin marketplace add <org/repo>
git clone https://github.com/<user>/<repo>.git ~/.claude/skills/<name>   # direct from GitHub

# Codex
ls ~/.codex/skills/

# Copy a skill between agents
cp -r ~/.codex/skills/brainstorming ~/.claude/skills/
```

---

## Troubleshooting

```bash
# Binary not found after install
which claude
ls -l ~/.local/bin/claude
ls ~/.local/share/claude/versions/

# Force reinstall claude (remove npm version first)
rm -rf ~/.nvm/versions/node/v22.14.0/bin/claude
rm -rf ~/.nvm/versions/node/v22.14.0/lib/node_modules/@anthropic-ai/claude-code
curl -fsSL https://claude.ai/install.sh | bash

# Check running processes
ps aux | grep -E 'claude|codex|gemini|droid'
```
