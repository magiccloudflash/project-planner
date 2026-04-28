# Project Planner — OpenCode AI 스킬

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner**는 코드 생성 전에 전문적인 프로젝트 계획 프로세스를 강제하는 OpenCode Agent 스킬입니다. 요구사항 분석, 아키텍처 설계, 작업 분해 및 진행 상황 추적을 보장합니다.

## 기능

- **필수 계획** — 사용자가 명시적으로 건너뛰지 않는 한 모든 코드 생성 작업은 먼저 계획을 거쳐야 합니다
- **도메인 분류** — 프로젝트 유형 자동 식별 (Web/CLI/Library/Mobile) 및 해당 모범 사례 적용
- **요구사항 분석** — 14가지 차원의 요구사항 명확화 + 3단계 우선순위 (P0/P1/P2)
- **위험 평가** — 6가지 위험 범주 식별, 등급 지정 및 완화 전략
- **아키텍처 설계** — ASCII 계층 다이어그램 + 데이터 모델 + API 계약
- **작업 분해** — 종속성 그래프 + 중요 경로 + 시간 추정
- **진행 상황 추적** — 각 단계 기록 + 마일스톤 요약
- **충돌 없음** — 다른 IDE 플러그인의 설정 파일을 수정하지 않음

## 설치

### 방법 1: 전역 설치 (권장)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### 방법 2: 프로젝트별 설치

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## 설정

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

## 워크플로우

사용자 요청 → 코드 생성 작업 식별 → 계획 건너뛰기? → 도메인 분류 → 요구사항 분석 → 기술 설계 → 작업 분해 → 작업별 실행

산출물: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## 호환성

다른 플러그인의 `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` 설정 파일을 수정하지 않습니다.

## 라이선스

MIT
