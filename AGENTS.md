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
│   └── *.md                # 25 subagent definitions
├── AGENTS.md               # This file
├── CHANGELOG.md            # Version history
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
| `opencode-go/mimo-v2.5-pro` | Erribaba, api-designer, code-generator, devops, e2e-tester, refactorer, test-writer | Best coding capability |
| `opencode-go/deepseek-v4-pro` | db-engineer, debugger, migration, perf-optimizer, reviewer, security-auditor | Strong at analysis and reasoning |
| `opencode-go/kimi-k2.6` | frontend-dev, ui-designer | Good at frontend/creative tasks |
| `opencode-go/qwen3.6-plus` | doc-writer, explore, project-manager, research | Good at writing, planning, and exploration |
| `opencode-go/glm-5.1` | architect | Architecture-level reasoning |
| `opencode-go/minimax-m2.7` | executor, validator | Execution and validation focus |

## Temperature Guide

Temperature controls the randomness/creativity of the model's output. Choose based on the task:

| Temperature | Use Case | Agents |
|-------------|----------|--------|
| **0.1** | Precise, deterministic output — code generation, database queries, command execution | code-generator, db-engineer, executor |
| **0.2** | Mostly deterministic with slight variation — debugging, review, security audit, validation | debugger, explore, frontend-reviewer, migration, perf-optimizer, reviewer, security-auditor, validator |
| **0.3** | Balanced — general implementation, refactoring, testing, DevOps, E2E, UI, vision | Erribaba, Zero, api-designer, devops, e2e-tester, frontend-dev, refactorer, software-engineer, test-writer, vision-dev |
| **0.4** | Slightly more creative — architecture design, Git workflow | architect, git-assistant |
| **0.5** | More creative — documentation, research, project management, UI design | doc-writer, project-manager, research, ui-designer |

**Guidelines:**
- Code generation and execution tasks → lower temperature (0.1-0.2)
- Review and analysis tasks → lower temperature (0.2)
- Implementation tasks → balanced temperature (0.3)
- Design and planning tasks → slightly higher temperature (0.4)
- Writing and research tasks → higher temperature (0.5)

## Prompt Writing Guidelines

### DO
- Use `##` sections for clear structure
- Include "What You Do NOT Do" section for delegation directions
- Include "Limitations" section for capability boundaries (only when different from delegation)
- Add "Quality Checklist" with actionable items
- Provide concrete output format examples
- Keep prompts focused — one role per agent

### DON'T
- Hardcode model names in prompts (they're in the frontmatter)
- Duplicate the same info in multiple sections
- Mix Chinese and English in the same sentence
- Make prompts longer than necessary — concise is better
- Add build/CI/tooling — this repo has none and needs none

### Section Order (subagents)
1. Role statement (one line)
2. "What You Do" or "Core Expertise"
3. "What You Do NOT Do" (delegation directions)
4. Domain-specific content (methodologies, patterns, etc.)
5. "Output Format"
6. "Limitations" (capability boundaries, if different from delegation)
7. "Interaction Style"
8. "Quality Checklist"

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
6. Update CHANGELOG.md with a summary of changes.

## Language

- Frontmatter `description`: Chinese
- System prompt body: English (most files) or Chinese (acceptable)
- README: Chinese primary, English secondary
