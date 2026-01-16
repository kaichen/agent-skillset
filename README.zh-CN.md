# Kai's Agent Skills

我的 Agent Skills 集合，可以作为 Claude Code 插件使用。

[English](./README.md) | 中文

## 插件

| 插件 | 描述 |
|------|------|
| [analyze-claude-code](./plugins/analyze-claude-code) | 分析 Claude Code CLI 源码 |
| [discover-skills](./plugins/discover-skills) | 发现可用技能和热门集合 |

## 什么是 Agent Skills？

[Agent Skills](https://agentskills.io) 是一个开放标准，用于教授 AI Agent 执行专业任务。Skill 是一个包含指令、脚本和资源的文件夹，Agent 可以动态加载以提升性能。

**核心特点：**
- **渐进式加载** - 初始只加载元数据（约 100 tokens），相关内容（<5k tokens）按需加载
- **跨平台** - 同一标准适用于 Claude Code、Claude.ai、Codex 等兼容 Agent
- **可组合** - Skill 可以引用其他 skill 和资源

**Skill 结构：**
```yaml
---
name: my-skill
description: 触发此 skill 的场景
---
# Agent 执行指令
```

**官方：**

| 仓库 | 描述 |
|------|------|
| [anthropics/skills](https://github.com/anthropics/skills) | Anthropic 官方 skills - 文档处理、创意设计、MCP 构建器 |
| [openai/skills](https://github.com/openai/skills) | Codex 专用 skills |

**社区精选（Awesome Lists）：**

| 仓库 | 描述 |
|------|------|
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 分类全面的 skills 目录 |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | 社区 skills 集合 |
| [VoltAgent/awesome-claude-skills](https://github.com/VoltAgent/awesome-claude-skills) | 合作伙伴和社区贡献 |
| [BehiSecc/awesome-claude-skills](https://github.com/BehiSecc/awesome-claude-skills) | 精选 skills 列表 |

**社区优质 Skills：**

| 仓库 | 描述 |
|------|------|
| [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | Vercel 官方 agent skills，专注 React/Next.js 和 Web 设计 |
| [huggingface/skills](https://github.com/huggingface/skills) | HuggingFace ML/AI 相关 skills |
| [trailofbits/skills](https://github.com/trailofbits/skills) | Trail of Bits 安全专项 skills |
| [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | Obsidian 知识管理 skills |
| [K-Dense-AI/claude-scientific-skills](https://github.com/K-Dense-AI/claude-scientific-skills) | 科研分析 skills |
| [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | UI/UX 设计，50+ 风格，多框架支持 |

## 推荐自用的 Skills

两个我每天都在用的 Skill，强烈推荐安装到用户级别：

| Skill | 描述 |
|-------|------|
| [planning-with-files](https://github.com/OthmanAdi/planning-with-files) | Manus 风格的文件化任务规划 |
| [brainstorming](https://github.com/obra/superpowers/blob/main/skills/brainstorming/SKILL.md) | 实现前探索用户意图和需求 |

**安装到用户级别 (`~/.claude/skills/`)：**

```bash
# planning-with-files - 直接 clone 到 skills 目录
gh repo clone OthmanAdi/planning-with-files ~/.claude/skills/planning-with-files

# brainstorming - 从 superpowers 仓库单独下载
# （superpowers 包含大量 skills，按需安装即可）
mkdir -p ~/.claude/skills/brainstorming
gh repo view obra/superpowers --raw skills/brainstorming/SKILL.md > ~/.claude/skills/brainstorming/SKILL.md
```

> **为什么用户级别？** `~/.claude/skills/` 中的 skills 全局可用，适合规划和头脑风暴这类通用工作流。

## 安装

```bash
# 从 marketplace 安装插件
claude plugins marketplace add kaichen/agent-skillset

# 或从 GitHub 安装
claude plugins add agent-skillset:analyze-claude-code
claude plugins add agent-skillset:discover-skills
```

## 许可证

MIT
