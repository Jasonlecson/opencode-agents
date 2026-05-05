# Opencode-agents

一套开箱即用的 OpenCode 智能体配置集合，涵盖架构设计、代码审查、调试、测试、前端开发等 18 个专业角色。

## 目录结构

```
agents/
├── Zero.md              # 主智能体（Kimi K2.6）
├── Erribaba.md          # 主智能体（mimo-v2.5-pro）
├── architect.md         # 架构设计
├── debugger.md          # 调试诊断
├── doc-writer.md        # 文档编写
├── e2e-tester.md        # 端到端测试
├── executor.md          # 命令执行
├── frontend-dev.md      # 前端开发
├── frontend-reviewer.md # 前端审查
├── git-assistant.md     # Git 工作流
├── perf-optimizer.md    # 性能优化
├── refactorer.md        # 代码重构
├── research.md          # 信息研究
├── reviewer.md          # 代码审查
├── security-auditor.md  # 安全审计
├── test-writer.md       # 测试编写
├── ui-designer.md       # UI 设计
└── validator.md         # 结果验证
```

## 智能体一览

### 主智能体（Primary）

| 文件 | 模型 | 说明 |
|------|------|------|
| `Zero.md` | Kimi K2.6 | 主编程智能体，负责需求分析、任务拆分和子智能体调度 |
| `Erribaba.md` | mimo-v2.5-pro | 主编程智能体，同上，使用不同模型 |

### 子智能体（Subagent）

| 文件 | 职责 | 只读 |
|------|------|:----:|
| `architect.md` | 系统设计、模块划分、技术选型 | ✓ |
| `debugger.md` | 定位和修复代码缺陷 | ✓ |
| `doc-writer.md` | 生成技术文档、API 参考 | ✓ |
| `e2e-tester.md` | Playwright/Cypress 端到端测试 | ✓ |
| `executor.md` | 运行命令、执行测试、构建项目 | ✗ |
| `frontend-dev.md` | React/Vue/Svelte 组件开发 | ✗ |
| `frontend-reviewer.md` | 前端代码审查、无障碍合规 | ✓ |
| `git-assistant.md` | 提交消息、分支命名、PR 描述 | ✓ |
| `perf-optimizer.md` | 性能分析与优化 | ✓ |
| `refactorer.md` | 代码重构、消除重复 | ✓ |
| `research.md` | 查找文档、调研技术方案 | ✓ |
| `reviewer.md` | 代码审查（逻辑/安全/性能） | ✓ |
| `security-auditor.md` | OWASP Top 10 安全审计 | ✓ |
| `test-writer.md` | 单元/集成/边界测试 | ✓ |
| `ui-designer.md` | CSS/Tailwind/响应式布局 | ✓ |
| `validator.md` | 最终验证（构建/测试/类型检查） | ✓ |

## 使用方式

1. 将 `agents/` 目录下的文件复制到你的 OpenCode 配置目录
2. 选择一个主智能体（`Zero.md` 或 `Erribaba.md`）作为默认智能体
3. 主智能体会根据任务类型自动调度对应的子智能体

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

## 参与贡献

1. Fork 本仓库
2. 新建 `Feat_xxx` 分支
3. 提交代码
4. 新建 Pull Request

## 许可证

[MIT](LICENSE)
