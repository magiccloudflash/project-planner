# Project Planner — OpenCode AI 技能插件

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** 是一个 OpenCode Agent Skill，用于在代码生成前强制执行专业的项目规划流程，确保每次开发都有清晰的需求分析、架构设计、任务拆解和进度追踪。

## 功能特性

- **强制规划** — 任何代码生成任务必须先经过规划，除非用户明确跳过
- **领域分类** — 自动识别项目类型（Web/CLI/Library/Mobile 等），应用对应最佳实践
- **需求分析** — 14 个维度的需求澄清问题 + 三级优先级（P0/P1/P2）
- **风险评估** — 6 类风险的识别、评级与缓解策略
- **架构设计** — ASCII 分层架构图 + 数据模型 + API 契约
- **任务拆解** — 依赖关系图 + 关键路径 + 工时估算
- **进度追踪** — 每步记录 + 里程碑总结
- **零冲突** — 不修改任何其他 IDE 插件的配置文件

## 安装方法

### 方式一：全局安装（推荐）

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### 方式二：项目级安装

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

### 验证安装

安装后重启 OpenCode，当发起代码生成请求时，AI 会自动加载该 Skill。

## 配置指南

### Skill 权限配置

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

```jsonc
{
  "agent": {
    "build": {
      "permission": {
        "skill": { "project-planner": "allow" }
      }
    }
  }
}
```

## 工作流程

用户提出需求 → 判断是否代码生成任务 → 用户是否跳过规划 → 领域分类 → 需求分析 → 技术设计 → 任务拆解 → 按任务执行

输出产物：`memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## 兼容性

不修改 `.vscode/`、`.cursor/`、`.continue/`、`.github/`、`.idea/` 等任何其他插件配置文件，与 Cline、Continue.dev、Cursor、Copilot 等完全兼容。

## License

MIT
