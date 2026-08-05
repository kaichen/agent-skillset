---
name: codebase-evidence-review
description: Use this when the user asks to research, review, audit, explain, or trace behavior in a codebase, repository, PR, spec, architecture doc, or local implementation. This skill should trigger for phrases like "基于 codebase", "从头梳理", "review", "audit", "看源码", "研究这份 codebase", "这个流程怎么跑", or when a symptom may be explained by local source. It enforces source-backed findings, exact file/function references, and verification before claims.
---

# Codebase Evidence Review

## Purpose

Produce answers that are grounded in the actual repository instead of product assumptions, docs-only reasoning, or visible UI labels. The user's repeated pattern is to ask for the real source path, real control fields, and real activation conditions before deciding whether to patch.

## When to use

Use this skill for:
- Codebase exploration, architecture tracing, source-backed explanations, PR/spec reviews, and bug triage.
- Questions that compare a visible symptom with implementation reality, such as model labels, Slack threading, runtime ownership, or route behavior.
- Review requests where findings must be actionable and tied to exact locations.

Do not use it for pure brainstorming, copy editing, or tasks where the user explicitly says not to inspect files.

## Workflow

1. **Orient on the repo**
   - Run `pwd` and inspect the nearest `AGENTS.md`.
   - Use `rg --files` or `fd` to find likely entrypoints, tests, config, and docs.
   - Read the smallest set of files that can answer the question.

2. **Trace the primary path**
   - Identify the first real entrypoint: CLI command, route handler, monitor, hook, service, component, or worker.
   - Follow data and control flow to the final side effect.
   - Name the decisive symbols: functions, classes, fields, env vars, config keys, routes, and storage tables.

3. **Separate facts from hypotheses**
   - Mark as fact only what is proven by source, local files, tests, logs, or a direct command.
   - Treat UI labels, model names, stale docs, and memory summaries as clues until source confirms them.
   - If external docs are needed because the code calls a third-party API, use primary docs and cite them.

4. **Check for real enablement**
   - Distinguish "code exists" from "this path is active."
   - Verify wiring: imports, route registration, package scripts, feature flags, env gates, config defaults, and runtime command path.
   - For reviews, include missing tests only when they would catch the actual risk.

5. **Report with evidence**
   - Findings first for reviews, ordered by severity.
   - For explanations, start with the direct answer, then show the source path that proves it.
   - Use exact local file links with line numbers when available.

## Review Output

For review-style tasks, use:

```markdown
**Findings**
- [P1] Title
  File: path:line
  Why it matters:
  Fix:

**Open Questions**
- ...

**Verification**
- Command/result or why not run.
```

For explanation-style tasks, use:

```markdown
Direct answer:

Evidence:
- path:line -> what it proves
- path:line -> what it proves

What could go wrong:
- ...
```

## Common Failure Modes

| Risk | Likelihood | Mitigation |
| --- | --- | --- |
| Broad greps create noise and hide the real path | High | Narrow quickly to entrypoints, helpers, and final send/side-effect code |
| Visible UI label is mistaken for implementation truth | Medium | Check the source fields and config that produce the behavior |
| A doc/spec is treated as shipped behavior | Medium | Verify route registration, scripts, tests, and runtime defaults |
| A code path exists but is not enabled | High | Check imports, feature gates, env, and package scripts |

## Key Principle

The answer is not "what seems likely"; the answer is the smallest source-backed path that explains the behavior.
