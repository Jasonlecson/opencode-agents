# Opencode-agents

一套开箱即用的 OpenCode 智能体配置集合，涵盖架构设计、代码审查、调试、测试、前端开发、数据库工程、DevOps 等 24 个专业子智能体，以及 2 个主智能体。

## 项目结构

```
opencode-agents/
├── opencode.jsonc          # OpenCode 全局配置（权限、默认智能体）
├── agents/
│   ├── Zero.md             # 主智能体 — 快速原型（mimo-v2.5，多模态）
│   ├── Erribaba.md         # 主智能体 — 生产级编码（mimo-v2.5-pro）
│   ├── api-designer.md     # API 端点设计、OpenAPI 规范
│   ├── architect.md        # 系统架构、模块划分、技术选型
│   ├── code-generator.md   # 高质量代码生成、算法实现
│   ├── db-engineer.md      # 数据库 Schema、Migration、SQL 优化
│   ├── debugger.md         # 调试诊断、根因分析
│   ├── devops.md           # Docker、CI/CD、Kubernetes、IaC
│   ├── doc-writer.md       # 技术文档、README、API 参考
│   ├── e2e-tester.md       # Playwright/Cypress 端到端测试
│   ├── executor.md         # 命令执行、测试运行、项目构建
│   ├── frontend-dev.md     # React/Vue/Svelte 组件开发
│   ├── frontend-reviewer.md# 前端代码审查、WCAG 2.1 AA 无障碍
│   ├── git-assistant.md    # 提交消息、分支命名、PR 描述
│   ├── migration.md        # 数据库迁移、框架升级、技术栈切换
│   ├── perf-optimizer.md   # 性能分析与优化
│   ├── project-manager.md  # 需求拆解、Sprint 规划、工作量评估
│   ├── refactorer.md       # 代码重构、消除重复
│   ├── research.md         # 文档查找、技术调研
│   ├── reviewer.md         # 后端代码审查（逻辑/安全/性能）
│   ├── security-auditor.md # OWASP Top 10 安全审计
│   ├── software-engineer.md# 全栈端到端实现
│   ├── test-writer.md      # 单元/集成/边界测试
│   ├── ui-designer.md      # CSS/Tailwind/响应式/动画
│   ├── validator.md        # 最终验证（构建/测试/类型检查）
│   └── vision-dev.md       # 设计稿分析、截图转代码
├── AGENTS.md               # 贡献指南与 Agent 编写规范
├── README.md               # 中文说明
├── README.en.md            # English
└── LICENSE                 # MIT
```

## 智能体一览

### 主智能体（Primary）

| 文件 | 模型 | 定位 |
|------|------|------|
| `Zero.md` | `opencode-go/mimo-v2.5` | 快速原型 — 多模态输入、视觉分析、轻量任务、快速迭代 |
| `Erribaba.md` | `opencode-go/mimo-v2.5-pro` | 生产编码 — 复杂算法、深度分析、性能关键代码 |

两个主智能体共享相同的子智能体调度体系，区别在于模型能力和适用场景：

- **Zero**：速度快、支持图像输入，适合原型验证和简单任务
- **Erribaba**：编码能力更强，适合生产环境代码和复杂工程任务

### 子智能体（Subagent）

#### 代码质量与审查

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `reviewer.md` | deepseek-v4-pro | 后端代码审查（逻辑/安全/性能/类型） | ✗ |
| `frontend-reviewer.md` | mimo-v2.5 | 前端审查（组件/性能/WCAG 2.1 AA/CSS） | ✗ |
| `security-auditor.md` | deepseek-v4-pro | OWASP Top 10 安全审计 | ✗ |
| `validator.md` | minimax-m2.7 | 最终验证（构建/测试/类型/lint） | ✗ |

#### 测试

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `test-writer.md` | mimo-v2.5-pro | 单元/集成/边界测试（AAA 模式） | ✓ |
| `e2e-tester.md` | mimo-v2.5-pro | Playwright/Cypress 端到端测试 | ✓ |

#### 调试与优化

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `debugger.md` | deepseek-v4-pro | 系统化调试、根因分析、最小修复 | ✓ |
| `perf-optimizer.md` | mimo-v2.5-pro | 性能分析、瓶颈定位、优化方案 | ✗ |
| `refactorer.md` | mimo-v2.5-pro | 代码重构、提取函数、消除重复 | ✓ |

#### 架构与设计

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `architect.md` | glm-5.1 | 系统架构、模块划分、技术选型 | ✗ |
| `api-designer.md` | mimo-v2.5-pro | API 端点设计、OpenAPI 规范、错误码 | ✓ |

#### 实现

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `code-generator.md` | mimo-v2.5-pro | 高质量代码生成、算法实现、Bug 修复 | ✓ |
| `software-engineer.md` | mimo-v2.5 | 全栈端到端实现（前后端+数据库） | ✓ |
| `frontend-dev.md` | kimi-k2.6 | React/Vue/Svelte 组件开发 | ✓ |
| `ui-designer.md` | kimi-k2.6 | CSS/Tailwind/响应式布局/动画 | ✓ |
| `vision-dev.md` | mimo-v2.5 | 设计稿分析、截图转代码（多模态） | ✓ |

#### 数据与基础设施

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `db-engineer.md` | deepseek-v4-pro | Schema 设计、Migration、SQL 优化 | ✓ |
| `devops.md` | mimo-v2.5-pro | Docker、CI/CD、Kubernetes、IaC | ✓ |
| `migration.md` | deepseek-v4-pro | 数据库迁移、框架升级、技术栈切换 | ✓ |

#### 文档与规划

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `doc-writer.md` | qwen3.6-plus | 技术文档、README、API 参考 | ✓ |
| `project-manager.md` | qwen3.6-plus | 需求拆解、Sprint 规划、工作量评估 | ✓ |
| `git-assistant.md` | mimo-v2.5 | 提交消息、分支命名、PR 描述 | ✗ |
| `research.md` | qwen3.6-plus | 文档查找、技术调研、方案对比 | ✗ |

#### 执行

| 文件 | 模型 | 职责 | 写权限 |
|------|------|------|:------:|
| `executor.md` | minimax-m2.7 | 命令执行、测试运行、项目构建 | ✓ |

## 使用方式

### 1. 复制智能体文件

将 `agents/` 目录下的文件复制到你的 OpenCode 配置目录：

```bash
# 全局配置目录
cp -r agents/ ~/.config/opencode/agents/

# 或项目级配置目录
cp -r agents/ <your-project>/.opencode/agents/
```

### 2. 配置 opencode.jsonc

将 `opencode.jsonc` 复制到你的 OpenCode 配置目录：

```bash
cp opencode.jsonc ~/.config/opencode/opencode.jsonc
```

该文件定义了：
- `default_agent` — 默认使用的主智能体（`Zero` 或 `Erribaba`）
- `permission` — 工具权限配置（文件操作、命令执行、网络访问等）

### 3. 开始使用

启动 OpenCode 后，主智能体会根据任务类型自动调度对应的子智能体。你也可以在对话中显式要求调用特定智能体。

## 配置格式

每个智能体文件由 YAML frontmatter + Markdown 正文组成：

```yaml
---
description: 中文描述（OpenCode 用于匹配触发场景）
mode: primary | subagent
model: provider/model-name
temperature: 0.0-1.0
tools:              # 可选，限制工具权限
  write: false
  edit: false
  bash: false
---

<系统提示词>
```

### 字段说明

| 字段 | 必填 | 说明 |
|------|:----:|------|
| `description` | ✓ | 中文描述，OpenCode 用它来决定何时调用该智能体 |
| `mode` | ✓ | `primary`（可作为顶层会话）或 `subagent`（仅通过调度调用） |
| `model` | ✓ | 模型标识，格式为 `provider/model-name` |
| `temperature` | ✓ | 生成温度，0.0-1.0 |
| `tools` | ✗ | 工具权限，省略的键默认允许；显式设为 `false` 则禁止 |

### 模型列表

本配置使用的模型：

| 模型标识 | 用途 |
|----------|------|
| `opencode-go/mimo-v2.5` | 多模态、快速原型、通用任务 |
| `opencode-go/mimo-v2.5-pro` | 生产级编码、复杂算法 |
| `opencode-go/deepseek-v4-pro` | 代码审查、安全审计、数据库、调试 |
| `opencode-go/kimi-k2.6` | 前端开发、UI 设计 |
| `opencode-go/qwen3.6-plus` | 文档、研究、项目管理 |
| `opencode-go/glm-5.1` | 架构设计 |
| `opencode-go/minimax-m2.7` | 命令执行、结果验证 |

## 参与贡献

1. Fork 本仓库
2. 新建 `Feat_xxx` 分支
3. 提交代码
4. 新建 Pull Request

详细的智能体编写规范请参考 [AGENTS.md](AGENTS.md)。

## 许可证

[MIT](LICENSE)
