# Project Planner — AI-ferdighet for OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** er en OpenCode Agent-ferdighet som håndhever en profesjonell prosjektplanleggingsprosess før kodegenerering, og sikrer tydelig behovsanalyse, arkitekturdesign, oppgavedekomponering og fremdriftsoppfølging.

## Funksjoner

- **Obligatorisk planlegging** — enhver kodegenereringsoppgave må først gjennomgå planlegging, med mindre brukeren uttrykkelig hopper over det
- **Domeneklassifisering** — automatisk gjenkjenning av prosjekttype (Web/CLI/Library/Mobile) med anvendelse av tilsvarende beste praksis
- **Behovsanalyse** — 14 dimensjoner for å avklare krav + tre prioriteringsnivåer (P0/P1/P2)
- **Risikovurdering** — identifisering, vurdering og reduksjonsstrategier for 6 risikokategorier
- **Arkitekturdesign** — ASCII-lagsdiagram + datamodell + API-kontrakter
- **Oppgavedekomponering** — avhengighetsgraf + kritisk sti + tidsestimering
- **Fremdriftsregistrering** — logging av hvert trinn + milepælsoppsummering
- **Null konflikter** — endrer ikke konfigurasjonsfiler for andre IDE-plugins

## Installasjon

### Metode 1: Global installasjon (anbefalt)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Metode 2: Prosjektnivåinstallasjon

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Konfigurasjon

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

## Arbeidsflyt

Brukerforespørsel → identifisering av kodegenereringsoppgave → hopp over planlegging? → domeneklassifisering → behovsanalyse → teknisk design → oppgavedekomponering → oppgavebasert utførelse

Artefakter: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Kompatibilitet

Endrer ikke konfigurasjonsfiler for `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` eller andre plugins.

## Lisens

MIT
