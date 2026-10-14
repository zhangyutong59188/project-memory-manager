<div align="center">

# project-memory-manager

**让 Codex 在多个会话之间记住真正重要的项目上下文。**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Codex-Skill-6E56CF)](SKILL.md)

[English](README.en.md) · [使用说明](references/usage.md)

</div>

## 它解决什么问题？

跨多个 Codex 会话开发时，项目状态、技术决策、失败原因和重要路径很容易丢失。`project-memory-manager` 使用项目内的 `.memory/` Markdown 文件保存这些长期有效的信息，让下一次会话可以快速恢复上下文。

它更像一份**项目开发笔记**，而不是流水账日志：重点记录为什么这样做、哪些方案被否定、哪些错误不要再次发生，以及重要资源在哪里。

## 主要特点

- **跨会话记忆**：保存项目状态、环境、资源、决策、失败记录和待办事项。
- **多子项目隔离**：总项目和每个子项目可以拥有独立的 memory，避免串项目。
- **中文写入**：面向人的 memory 内容默认使用中文；技术名称、路径和代码标识符保持原样。
- **安全边界**：不会保存密码、API key、token 或私密配置。
- **纯 Markdown**：不依赖数据库，容易阅读、审查、版本控制和扩展。

## 快速开始

### 安装

将此目录复制到 Codex skills 目录：

```bash
cp -R project-memory-manager ~/.codex/skills/
```

### 初始化项目 memory

在项目根目录创建 `.memory/`，使用模板目录中的文件：

```bash
mkdir -p .memory
cp ~/.codex/skills/project-memory-manager/assets/memory-template/*.md .memory/
```

### 使用

在 Codex 中显式调用：

```text
$project-memory-manager
请读取当前项目 memory，然后继续实现这个任务。
```

也可以从具体子项目目录启动任务，让 skill 优先读取该子项目的 `.memory/`。

## Memory 结构

```text
项目根目录/
├── .memory/
│   ├── PROJECT_STATE.md   # 总项目状态
│   ├── SUBPROJECTS.md     # 子项目清单与依赖关系
│   ├── ENVIRONMENT.md     # 开发环境
│   ├── ASSETS.md          # 模型、数据、代码和输出路径
│   ├── DECISIONS.md       # 技术决策及原因
│   ├── FAILURES.md        # 问题、原因和解决方案
│   ├── SESSION_LOG.md     # 重要任务总结
│   └── TODO.md            # 当前待办
│
└── 子项目/
    └── .memory/           # 子项目自己的同名文件
```

根目录 memory 保存整体状态和跨项目关系；子项目 memory 保存实现细节。跨子项目任务分别更新相关目录，只把共享决策写入根目录。

## 记录什么

| 文件 | 记录内容 |
| --- | --- |
| `PROJECT_STATE.md` | 项目名称、目标、阶段、最近完成内容、阻塞问题 |
| `SUBPROJECTS.md` | 子项目路径、用途、状态和依赖关系 |
| `ENVIRONMENT.md` | OS、Python、CUDA、GPU、虚拟环境和依赖版本 |
| `ASSETS.md` | 模型、数据集、checkpoint、输出和配置路径 |
| `DECISIONS.md` | 决定、原因、放弃方案和重新考虑条件 |
| `FAILURES.md` | 问题、原因、尝试过的方法、最终方案和避免方式 |
| `SESSION_LOG.md` | 重要任务的完成内容、修改文件和下一步计划 |
| `TODO.md` | 当前和后续的可执行任务 |

## 设计原则

1. 只记录会影响未来开发的信息。
2. 先读取当前子项目的 memory，再开始规划工作。
3. 验证可能过期的路径、版本和状态，不盲信历史记录。
4. 一个主题保持一个事实来源，避免重复记录。
5. 保留失败原因和被否定的方案，减少重复踩坑。

## 自定义与扩展

所有核心执行规则集中在 [`SKILL.md`](SKILL.md)。初始化模板位于 [`assets/memory-template/`](assets/memory-template/)，使用说明位于 [`references/usage.md`](references/usage.md)。

可以继续扩展：

- AI 模型实验记录
- 数据集版本管理
- 自动生成实验报告
- Git commit 关联

## 许可证

本项目使用 [MIT License](LICENSE)。
