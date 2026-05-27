# AGENTS.md

## What This Repo Is

A collection of OpenCode agent configuration files. No code, no build, no tests — only `.md` files that define agent behavior via YAML frontmatter + prompt body, plus an `opencode.jsonc` for global settings.

## Structure

```
opencode-agents/
├── opencode.jsonc          # Global config (permissions, default agent)
├── agents/
│   ├── Zero.md             # Primary agent (mimo-v2.5, multimodal)
│   ├── Erribaba.md         # Primary agent (mimo-v2.5-pro)
│   └── *.md                # 24 subagent definitions
├── AGENTS.md               # This file
├── README.md               # Chinese
├── README.en.md            # English
└── LICENSE                 # MIT
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
- **`mode: primary`** means the agent can be a top-level session. Only `Zero.md` (mimo-v2.5) and `Erribaba.md` (mimo-v2.5-pro) are primary agents.
- **`mode: subagent`** means the agent is only invoked via delegation from a primary agent.
- **Tool restrictions** in frontmatter (`write: false`, `edit: false`, `bash: false`) make an agent read-only. Most review/audit subagents are read-only; implementation agents have write access.
- **Model naming**: provider prefix matters — use `opencode-go/mimo-v2.5`, `opencode-go/deepseek-v4-pro`, etc.
- **Filename = agent name** used in delegation (e.g., `reviewer.md` → delegate as `reviewer`).
- **Primary agents must list all subagents** in their body — when adding a new subagent, update both `Zero.md` and `Erribaba.md`.

## Model Assignments

| Model | Used By | Reasoning |
|-------|---------|-----------|
| `opencode-go/mimo-v2.5` | Zero, frontend-reviewer, git-assistant, software-engineer, vision-dev | Multimodal, fast, general-purpose |
| `opencode-go/mimo-v2.5-pro` | Erribaba, api-designer, code-generator, devops, e2e-tester, perf-optimizer, refactorer, test-writer | Best coding capability |
| `opencode-go/deepseek-v4-pro` | db-engineer, debugger, migration, reviewer, security-auditor | Strong at analysis and reasoning |
| `opencode-go/kimi-k2.6` | frontend-dev, ui-designer | Good at frontend/creative tasks |
| `opencode-go/qwen3.6-plus` | doc-writer, project-manager, research | Good at writing and planning |
| `opencode-go/glm-5.1` | architect | Architecture-level reasoning |
| `opencode-go/minimax-m2.7` | executor, validator | Execution and validation focus |

## opencode.jsonc

The global config file controls:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "Zero",  // or "Erribaba"
  "permission": {
    "read": "allow",
    "edit": "allow",
    "glob": "allow",
    "grep": "allow",
    "bash": "allow",
    "webfetch": "allow",
    "websearch": "allow",
    "task": "allow",       // subagent delegation
    "skill": "allow",
    "todowrite": "allow",
    "question": "allow",
    "external_directory": "allow"
  }
}
```

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
