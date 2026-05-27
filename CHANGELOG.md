# Changelog

All notable changes to this project will be documented in this file.

## [1.1.0] - 2026-05-27

### Added
- `explore.md` — 新增代码库探索智能体，用于快速搜索代码、理解项目结构
- `CHANGELOG.md` — 新增变更日志
- `opencode.jsonc` — 新增 OpenCode 全局配置文件

### Changed
- `Zero.md` — 子智能体列表从平铺改为分类格式（与 Erribaba 一致）
- `Zero.md` — 添加 explore 智能体到调度列表
- `Erribaba.md` — 添加 explore 智能体到调度列表
- `Erribaba.md` — 去除 prompt 中硬编码的模型名
- `perf-optimizer.md` — 模型从 mimo-v2.5-pro 改为 deepseek-v4-pro（更适合推理分析）；充实优化方法论和工具参考
- `research.md` — 充实研究领域、质量标准和反模式；添加 webfetch 工具权限
- `AGENTS.md` — 补充温度选择指南、模型分配策略、编写规范

### Fixed
- `debugger.md` — 修复工具权限（write/edit=true）与 Limitations（"Cannot modify code"）的矛盾
- `api-designer.md` — 删除重复的 "What You Do NOT Do" 章节
- `architect.md` — 删除重复的 "What You Do NOT Do" 章节
- `validator.md` — 修复中英文混杂（"is明确" → "is explicit"）
- `security-auditor.md` — 去除 prompt 中硬编码的模型名
- `software-engineer.md` — 统一 "What You Don't Do" 为 "What You Do NOT Do"
- 多个子智能体 — 清理重复的 Limitations 章节，保留独特的边界信息

## [1.0.0] - 2026-05-25

### Initial Release
- 2 个主智能体：Zero（快速原型）、Erribaba（生产编码）
- 24 个子智能体覆盖：架构设计、代码审查、调试、测试、前端开发、数据库工程、DevOps、文档、项目管理等
- MIT 许可证
