# Opencode-agents

A ready-to-use collection of OpenCode agent configurations covering 18 specialized roles: architecture, code review, debugging, testing, frontend development, and more.

## Directory Structure

```
agents/
├── Zero.md              # Primary agent (Kimi K2.6)
├── Erribaba.md          # Primary agent (mimo-v2.5-pro)
├── architect.md         # Architecture design
├── debugger.md          # Debugging & diagnostics
├── doc-writer.md        # Documentation writing
├── e2e-tester.md        # End-to-end testing
├── executor.md          # Command execution
├── frontend-dev.md      # Frontend development
├── frontend-reviewer.md # Frontend code review
├── git-assistant.md     # Git workflow
├── perf-optimizer.md    # Performance optimization
├── refactorer.md        # Code refactoring
├── research.md          # Technical research
├── reviewer.md          # Code review
├── security-auditor.md  # Security audit
├── test-writer.md       # Test writing
├── ui-designer.md       # UI design & styling
└── validator.md         # Final validation
```

## Agent Overview

### Primary Agents

| File | Model | Description |
|------|-------|-------------|
| `Zero.md` | Kimi K2.6 | Lead programming agent — requirement analysis, task breakdown, subagent orchestration |
| `Erribaba.md` | mimo-v2.5-pro | Same role, different model |

### Subagents

| File | Responsibility | Read-only |
|------|---------------|:---------:|
| `architect.md` | System design, module planning, tech selection | ✓ |
| `debugger.md` | Systematic bug isolation and fixing | ✓ |
| `doc-writer.md` | Technical docs, API references | ✓ |
| `e2e-tester.md` | Playwright/Cypress end-to-end tests | ✓ |
| `executor.md` | Run commands, execute tests, build projects | ✗ |
| `frontend-dev.md` | React/Vue/Svelte component development | ✗ |
| `frontend-reviewer.md` | Frontend review, accessibility compliance | ✓ |
| `git-assistant.md` | Commit messages, branch naming, PR descriptions | ✓ |
| `perf-optimizer.md` | Performance profiling and optimization | ✓ |
| `refactorer.md` | Code refactoring, duplication removal | ✓ |
| `research.md` | Documentation lookup, tech research | ✓ |
| `reviewer.md` | Code review (logic, security, performance) | ✓ |
| `security-auditor.md` | OWASP Top 10 security audit | ✓ |
| `test-writer.md` | Unit, integration, and edge-case tests | ✓ |
| `ui-designer.md` | CSS/Tailwind, responsive layouts, animations | ✓ |
| `validator.md` | Final validation (build, tests, type check) | ✓ |

## Usage

1. Copy the files from `agents/` to your OpenCode configuration directory
2. Choose a primary agent (`Zero.md` or `Erribaba.md`) as your default
3. The primary agent automatically delegates tasks to the appropriate subagent

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

## Contributing

1. Fork the repository
2. Create a `Feat_xxx` branch
3. Commit your code
4. Create a Pull Request

## License

[MIT](LICENSE)
