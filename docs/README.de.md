# Project Planner — AI-Fähigkeit für OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** ist eine OpenCode Agent-Fähigkeit, die einen professionellen Projektplanungsprozess vor der Codegenerierung erzwingt und eine klare Anforderungsanalyse, Architekturdesign, Aufgabenzerlegung und Fortschrittsverfolgung gewährleistet.

## Funktionen

- **Verpflichtende Planung** — jede Codegenerierungsaufgabe muss zuerst geplant werden, es sei denn, der Benutzer überspringt sie explizit
- **Domänenklassifizierung** — automatische Erkennung des Projekttyps (Web/CLI/Library/Mobile) mit entsprechenden Best Practices
- **Anforderungsanalyse** — 14 Dimensionen zur Klärung der Anforderungen + drei Prioritätsstufen (P0/P1/P2)
- **Risikobewertung** — Identifizierung, Bewertung und Minderungsstrategien für 6 Risikokategorien
- **Architekturdesign** — ASCII-Schichtendiagramm + Datenmodell + API-Verträge
- **Aufgabenzerlegung** — Abhängigkeitsgraph + kritischer Pfad + Zeitaufwandsschätzung
- **Fortschrittsverfolgung** — Aufzeichnung jedes Schritts + Meilensteinzusammenfassung
- **Null Konflikte** — ändert keine Konfigurationsdateien anderer IDE-Plugins

## Installation

### Methode 1: Globale Installation (empfohlen)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Methode 2: Projektbezogene Installation

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Konfiguration

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

## Arbeitsablauf

Benutzeranfrage → Erkennung einer Codegenerierungsaufgabe → Planung überspringen? → Domänenklassifizierung → Anforderungsanalyse → technisches Design → Aufgabenzerlegung → aufgabenbasierte Ausführung

Artefakte: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Kompatibilität

Ändert keine Konfigurationsdateien von `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` oder anderen Plugins.

## Lizenz

MIT
