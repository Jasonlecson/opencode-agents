# Opencode-agents

A ready-to-use collection of OpenCode agent configurations: 2 primary agents and 25 specialized subagents covering architecture, code review, debugging, testing, frontend development, database engineering, DevOps, and more.

## Project Structure

```
opencode-agents/
├── opencode.jsonc          # OpenCode global config (permissions, default agent)
├── agents/
│   ├── Zero.md             # Primary — rapid prototyping (mimo-v2.5, multimodal)
│   ├── Erribaba.md         # Primary — production coding (mimo-v2.5-pro)
│   ├── api-designer.md     # API endpoint design, OpenAPI specs
│   ├── architect.md        # System architecture, module planning
│   ├── code-generator.md   # High-quality code generation, algorithms
│   ├── db-engineer.md      # Database schema, migrations, SQL optimization
│   ├── debugger.md         # Systematic debugging, root cause analysis
│   ├── devops.md           # Docker, CI/CD, Kubernetes, IaC
│   ├── doc-writer.md       # Technical docs, README, API references
│   ├── e2e-tester.md       # Playwright/Cypress end-to-end tests
│   ├── executor.md         # Command execution, test running, builds
│   ├── frontend-dev.md     # React/Vue/Svelte component development
│   ├── frontend-reviewer.md# Frontend review, WCAG 2.1 AA accessibility
│   ├── git-assistant.md    # Commit messages, branch naming, PR descriptions
│   ├── migration.md        # DB migration, framework upgrades, stack changes
│   ├── perf-optimizer.md   # Performance profiling and optimization
│   ├── project-manager.md  # Requirements breakdown, sprint planning
│   ├── refactorer.md       # Code refactoring, duplication removal
│   ├── research.md         # Documentation lookup, tech research
│   ├── reviewer.md         # Backend code review (logic/security/performance)
│   ├── security-auditor.md # OWASP Top 10 security audit
│   ├── software-engineer.md# Full-stack end-to-end implementation
│   ├── test-writer.md      # Unit, integration, and edge-case tests
│   ├── ui-designer.md      # CSS/Tailwind, responsive layouts, animations
│   ├── validator.md        # Final validation (build/tests/type check)
│   ├── explore.md          # Codebase exploration, structure analysis
│   └── vision-dev.md       # Design screenshot analysis, image-to-code
├── AGENTS.md               # Contributing guide & agent authoring spec
├── CHANGELOG.md            # Version history
├── README.md               # Chinese
├── README.en.md            # English (this file)
└── LICENSE                 # MIT
```

## Agent Overview

### Primary Agents

| File | Model | Purpose |
|------|-------|---------|
| `Zero.md` | `opencode-go/mimo-v2.5` | Rapid prototyping — multimodal input, visual analysis, lightweight tasks |
| `Erribaba.md` | `opencode-go/mimo-v2.5-pro` | Production coding — complex algorithms, deep analysis, perf-critical code |

Both primary agents share the same subagent orchestration system. The difference is model capability and use case:

- **Zero**: Fast, supports image input, ideal for prototyping and simple tasks
- **Erribaba**: Stronger coding ability, ideal for production code and complex engineering

### Subagents

#### Code Quality & Review

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `reviewer.md` | deepseek-v4-pro | Backend review (logic/security/performance/types) | ✗ |
| `frontend-reviewer.md` | mimo-v2.5 | Frontend review (components/perf/WCAG 2.1 AA/CSS) | ✗ |
| `security-auditor.md` | deepseek-v4-pro | OWASP Top 10 security audit | ✗ |
| `validator.md` | minimax-m2.7 | Final validation (build/tests/types/lint) | ✗ |

#### Testing

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `test-writer.md` | mimo-v2.5-pro | Unit/integration/edge-case tests (AAA pattern) | ✓ |
| `e2e-tester.md` | mimo-v2.5-pro | Playwright/Cypress end-to-end tests | ✓ |

#### Debugging & Optimization

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `debugger.md` | deepseek-v4-pro | Systematic debugging, root cause, minimal fix | ✓ |
| `perf-optimizer.md` | deepseek-v4-pro | Performance profiling, bottleneck identification | ✗ |
| `refactorer.md` | mimo-v2.5-pro | Code refactoring, extract functions, DRY | ✓ |

#### Architecture & Design

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `architect.md` | glm-5.1 | System architecture, module planning, tech selection | ✗ |
| `api-designer.md` | mimo-v2.5-pro | API endpoint design, OpenAPI specs, error codes | ✓ |

#### Implementation

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `code-generator.md` | mimo-v2.5-pro | High-quality code gen, algorithms, bug fixes | ✓ |
| `software-engineer.md` | mimo-v2.5 | Full-stack end-to-end implementation | ✓ |
| `frontend-dev.md` | kimi-k2.6 | React/Vue/Svelte component development | ✓ |
| `ui-designer.md` | kimi-k2.6 | CSS/Tailwind, responsive layouts, animations | ✓ |
| `vision-dev.md` | mimo-v2.5 | Design analysis, screenshot-to-code (multimodal) | ✓ |

#### Data & Infrastructure

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `db-engineer.md` | deepseek-v4-pro | Schema design, migrations, SQL optimization | ✓ |
| `devops.md` | mimo-v2.5-pro | Docker, CI/CD, Kubernetes, IaC | ✓ |
| `migration.md` | deepseek-v4-pro | DB migration, framework upgrades, stack changes | ✓ |

#### Documentation & Planning

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `doc-writer.md` | qwen3.6-plus | Technical docs, README, API references | ✓ |
| `project-manager.md` | qwen3.6-plus | Requirements breakdown, sprint planning | ✓ |
| `git-assistant.md` | mimo-v2.5 | Commit messages, branch naming, PR descriptions | ✗ |
| `research.md` | qwen3.6-plus | Documentation lookup, tech research | ✗ |

#### Execution

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `executor.md` | minimax-m2.7 | Command execution, test running, builds | ✓ |

#### Exploration

| File | Model | Responsibility | Write |
|------|-------|---------------|:-----:|
| `explore.md` | qwen3.6-plus | Codebase search, project structure analysis | ✗ |

## Usage

### 1. Copy Agent Files

Copy the `agents/` directory to your OpenCode config location:

```bash
# Global config
cp -r agents/ ~/.config/opencode/agents/

# Or project-level config
cp -r agents/ <your-project>/.opencode/agents/
```

### 2. Configure opencode.jsonc

Copy `opencode.jsonc` to your OpenCode config directory:

```bash
cp opencode.jsonc ~/.config/opencode/opencode.jsonc
```

This file defines:
- `default_agent` — which primary agent to use (`Zero` or `Erribaba`)
- `permission` — tool permissions (file ops, command execution, network access, etc.)

### 3. Start Using

After launching OpenCode, the primary agent automatically delegates tasks to the appropriate subagent. You can also explicitly request a specific subagent in your conversation.

## File Format

Each agent file consists of YAML frontmatter + Markdown body:

```yaml
---
description: Chinese description (used by OpenCode for trigger matching)
mode: primary | subagent
model: provider/model-name
temperature: 0.0-1.0
tools:              # optional — restrict tool access
  write: false
  edit: false
  bash: false
---

<System prompt>
```

### Field Reference

| Field | Required | Description |
|-------|:--------:|-------------|
| `description` | Yes | Chinese text — OpenCode uses this to decide when to invoke the agent |
| `mode` | Yes | `primary` (top-level session) or `subagent` (invoked via delegation only) |
| `model` | Yes | Model identifier in `provider/model-name` format |
| `temperature` | Yes | Generation temperature, 0.0-1.0 |
| `tools` | No | Tool permissions; omitted keys default to allowed; set `false` to deny |

### Models Used

| Model ID | Purpose |
|----------|---------|
| `opencode-go/mimo-v2.5` | Multimodal, rapid prototyping, general tasks |
| `opencode-go/mimo-v2.5-pro` | Production coding, complex algorithms |
| `opencode-go/deepseek-v4-pro` | Code review, security audit, database, debugging |
| `opencode-go/kimi-k2.6` | Frontend development, UI design |
| `opencode-go/qwen3.6-plus` | Documentation, research, project management |
| `opencode-go/glm-5.1` | Architecture design |
| `opencode-go/minimax-m2.7` | Command execution, result validation |

## Contributing

1. Fork the repository
2. Create a `Feat_xxx` branch
3. Commit your code
4. Create a Pull Request

For detailed agent authoring guidelines, see [AGENTS.md](AGENTS.md).

## License

[MIT](LICENSE)
