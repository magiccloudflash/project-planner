# Project Planner — OpenCode AI 技能插件

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** 是一個 OpenCode Agent Skill，用於在程式碼生成前強制執行專業的專案規劃流程，確保每次開發都有清晰的需求分析、架構設計、任務拆解和進度追蹤。

## 功能特性

- **強制規劃** — 任何程式碼生成任務必須先經過規劃，除非使用者明確跳過
- **領域分類** — 自動識別專案類型（Web/CLI/Library/Mobile 等），應用對應最佳實踐
- **需求分析** — 14 個維度的需求釐清問題 + 三級優先級（P0/P1/P2）
- **風險評估** — 6 類風險的識別、評級與緩解策略
- **架構設計** — ASCII 分層架構圖 + 資料模型 + API 合約
- **任務拆解** — 依賴關係圖 + 關鍵路徑 + 工時估算
- **進度追蹤** — 每步記錄 + 里程碑總結
- **零衝突** — 不修改任何其他 IDE 插件的設定檔

## 安裝方法

### 方式一：全域安裝（推薦）

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### 方式二：專案級安裝

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## 配置指南

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

## 工作流程

使用者提出需求 → 判斷是否程式碼生成任務 → 使用者是否跳過規劃 → 領域分類 → 需求分析 → 技術設計 → 任務拆解 → 按任務執行

輸出產物：`memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## 兼容性

不修改 `.vscode/`、`.cursor/`、`.continue/`、`.github/`、`.idea/` 等任何其他插件設定檔。

## License

MIT
