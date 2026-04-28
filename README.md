# Project Planner — AI Skill for OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

<div align="center">

**🌐 Languages / 语言 / 語言 / Языки / Langues / Sprachen / Lingue / Idiomas / 언어 / اللغات / زبان‌ها / زبانیں / Språk / Kielet**

[🇨🇳 简体中文](docs/README.zh-CN.md) · [🇭🇰 繁體中文](docs/README.zh-TW.md) · [🇷🇺 Русский](docs/README.ru.md) · [🇫🇷 Français](docs/README.fr.md) · [🇩🇪 Deutsch](docs/README.de.md) · [🇮🇹 Italiano](docs/README.it.md) · [🇧🇷 Português](docs/README.pt.md) · [🇪🇸 Español](docs/README.es.md) · [🇰🇷 한국어](docs/README.ko.md) · [🇸🇦 العربية](docs/README.ar.md) · [🇮🇷 فارسی](docs/README.fa.md) · [🇵🇰 اردو](docs/README.ur.md) · [🇳🇴 Norsk](docs/README.no.md) · [🇫🇮 Suomi](docs/README.fi.md)

</div>

**project-planner** 是一个 OpenCode Agent Skill，用于在代码生成前强制执行专业的项目规划流程，确保每次开发都有清晰的需求分析、架构设计、任务拆解和进度追踪。

## Features

- **强制规划** — 任何代码生成任务必须先经过规划，除非用户明确跳过
- **领域分类** — 自动识别项目类型（Web/CLI/Library/Mobile/等），应用对应最佳实践
- **需求分析** — 14 个维度的需求澄清问题 + 三级优先级（P0/P1/P2）
- **风险评估** — 6 类风险的识别、评级与缓解策略
- **架构设计** — ASCII 分层架构图 + 数据模型 + API 契约
- **任务拆解** — 依赖关系图 + 关键路径 + 工时估算
- **进度追踪** — 每步记录 + 里程碑总结
- **零冲突** — 不修改任何其他 IDE 插件的配置文件

## Installation

### 方式一：全局安装（推荐）

将 `project-planner` 复制到 OpenCode 全局 skills 目录：

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### 方式二：项目级安装

每个项目单独启用：

```bash
# 在项目根目录下
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

### 验证安装

安装后重启 OpenCode，当发起代码生成请求时，AI 会自动加载该 Skill。你也可以在对话中查看可用的 skills 列表。

## Configuration

### Skill 权限配置（可选）

在 `~/.config/opencode/opencode.json` 或项目根目录的 `opencode.json` 中配置：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "skill": {
      "project-planner": "allow"
    }
  }
}
```

### Agent 覆盖配置

为不同 agent 设置不同 Skill 访问权限：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "build": {
      "permission": {
        "skill": {
          "project-planner": "allow"
        }
      }
    },
    "plan": {
      "permission": {
        "skill": {
          "project-planner": "allow"
        }
      }
    }
  }
}
```

### 禁用 Skill

如要临时关闭：

```jsonc
{
  "permission": {
    "skill": {
      "project-planner": "deny"
    }
  }
}
```

## How It Works

### Skill 触发规则

```
用户提出需求
    │
    ▼
是否为代码生成任务？──否──→ 正常处理
    │ 是
    ▼
用户说了"不需要规划"？──是──→ 跳过规划，直接编码
    │ 否
    ▼
    ┌─────────────────────┐
    │ Step 0: 领域分类     │
    └─────────┬───────────┘
              ▼
    ┌─────────────────────┐
    │ Phase 1: 需求分析   │ → plan.md
    └─────────┬───────────┘
              ▼ (用户确认)
    ┌─────────────────────┐
    │ Phase 2: 技术设计   │ → design.md
    └─────────┬───────────┘
              ▼ (用户确认)
    ┌─────────────────────┐
    │ Phase 3: 任务拆解   │ → tasks.md
    └─────────┬───────────┘
              ▼
    ┌─────────────────────┐
    │ Phase 4: 任务驱动执行│ → progress.md
    └─────────────────────┘
```

### 输出产物

所有文件写入项目根目录的 `memory/project-planner/`：

| 文件 | 内容 | 产出阶段 |
|------|------|----------|
| `plan.md` | 需求分析、范围、验收标准、风险矩阵 | Phase 1 |
| `design.md` | 架构图、数据模型、API 契约、文件结构 | Phase 2 |
| `tasks.md` | 任务依赖图、每个任务规格、关键路径 | Phase 3 |
| `progress.md` | 执行日志、里程碑总结 | Phase 4 |

### Example: plan.md

```markdown
# Project Plan — User Auth Service

## Domain
- **Type**: Web Backend
- **Pattern**: Clean Architecture (Controller → Service → Repository)
- **Language**: TypeScript 5.x + Node.js 20

## Overview
RESTful authentication service supporting email/password and OAuth2 login...

## Scope
### P0 — MVP
| ID   | Feature | Description |
|------|---------|-------------|
| F-001 | Register | Email + password signup with validation |
| F-002 | Login | JWT-based login with refresh token |
### P1 — Important
| ID   | Feature |
|------|---------|
| F-003 | OAuth2 (Google) |
### P2 — Deferred
| ID   | Feature |
|------|---------|
| F-004 | Password reset via email |

## Risk Matrix
| ID   | Description | Likelihood | Impact | Mitigation |
|------|-------------|-----------|--------|------------|
| R-001 | JWT secret leak | Low | High | Use env vars + key rotation |
```

## Compatibility

| 插件 | 是否冲突 | 说明 |
|------|---------|------|
| **Cline** | ❌ 不冲突 | 不修改 `.claude/` 目录 |
| **Continue.dev** | ❌ 不冲突 | 不修改 `.continue/` 目录 |
| **Cursor** | ❌ 不冲突 | 不修改 `.cursor/` 目录 |
| **GitHub Copilot** | ❌ 不冲突 | 无配置交集 |
| **code-review** (本机) | ❌ 不冲突 | 先规划再审查，流程互补 |
| **hallucination-prevention** (本机) | ❌ 不冲突 | 各自独立工作 |

**核心原则**：不修改 `.vscode/`、`.cursor/`、`.continue/`、`.github/`、`.idea/` 等任何其他插件的配置文件。

## Development

```bash
# 仓库结构
project-planner/
├── SKILL.md       # Skill 主文件（725 行）
├── README.md      # 本文档（英文，含语言选择器）
└── docs/
    ├── README.zh-CN.md   # 简体中文
    ├── README.zh-TW.md   # 繁體中文
    ├── README.ru.md      # Русский
    ├── README.fr.md      # Français
    ├── README.de.md      # Deutsch
    ├── README.it.md      # Italiano
    ├── README.pt.md      # Português
    ├── README.es.md      # Español
    ├── README.ko.md      # 한국어
    ├── README.ar.md      # العربية
    ├── README.fa.md      # فارسی
    ├── README.ur.md      # اردو
    ├── README.no.md      # Norsk
    └── README.fi.md      # Suomi
```

### 修改后同步

```bash
# 安装到 opencode
Copy-Item -Path "D:\skill插件开发\project-planner\SKILL.md" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner\SKILL.md" -Force
```

## License

MIT
