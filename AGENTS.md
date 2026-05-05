# AGENTS.md

## What This Repo Is

A collection of OpenCode agent configuration files. No code, no build, no tests — only `.md` files that define agent behavior via YAML frontmatter + prompt body.

## Structure

```
agents/
  *.md          # Agent definitions (18 files)
README.md       # Chinese (Gitee boilerplate, mostly placeholder)
README.en.md    # English (same)
LICENSE         # MIT
```

## Agent File Format

Every file in `agents/` uses this structure:

```yaml
---
description: <Chinese description — this is what OpenCode uses to decide when to invoke the agent>
mode: primary | subagent
model: <provider/model-name>
temperature: <0.0-1.0>
tools:            # optional — omit keys to allow all
  write: false
  edit: false
  bash: false
---

<System prompt in English or Chinese>
```

## Key Conventions

- **`description` is always in Chinese** — this is the trigger text OpenCode matches against. Keep it consistent with existing files.
- **`mode: primary`** means the agent can be a top-level session. Only `Zero.md` (Kimi K2.6) and `Erribaba.md` (mimo-v2.5-pro) are primary agents.
- **`mode: subagent`** means the agent is only invoked via delegation from a primary agent.
- **Tool restrictions** in frontmatter (`write: false`, `edit: false`, `bash: false`) make an agent read-only. Most subagents are read-only; `executor` and `frontend-dev` are not.
- **Model naming**: provider prefix matters — `opencode-go/mimo-v2.5`, `opencode-go/kimi-k2.6`, `xiaomi-token-plan-cn/mimo-v2.5-pro`.
- **Filename = agent name** used in delegation (e.g., `reviewer.md` → delegate as `reviewer`).

## When Adding or Editing Agents

1. Match the frontmatter field order: `description`, `mode`, `model`, `temperature`, then optional `tools`.
2. Write `description` in Chinese, matching the style of existing files (role + trigger scenarios).
3. Keep system prompts concise and structured with `##` sections.
4. Primary agents must list all available subagents in their body — update both `Zero.md` and `Erribaba.md` if adding a new subagent.
5. Do not add build/CI/tooling — this repo has none and needs none.

## Language

- Frontmatter `description`: Chinese
- System prompt body: English (most files) or Chinese (acceptable)
- README: Chinese primary, English secondary
