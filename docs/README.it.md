# Project Planner — Skill AI per OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** è una skill per OpenCode Agent che impone un processo professionale di pianificazione del progetto prima della generazione del codice, garantendo analisi dei requisiti, progettazione architetturale, scomposizione delle attività e monitoraggio dei progressi chiari.

## Funzionalità

- **Pianificazione obbligatoria** — qualsiasi attività di generazione del codice deve essere prima pianificata, a meno che l'utente non la salti esplicitamente
- **Classificazione del dominio** — riconoscimento automatico del tipo di progetto (Web/CLI/Library/Mobile) con applicazione delle migliori pratiche corrispondenti
- **Analisi dei requisiti** — 14 dimensioni per chiarire i requisiti + tre livelli di priorità (P0/P1/P2)
- **Valutazione dei rischi** — identificazione, valutazione e strategie di mitigazione per 6 categorie di rischio
- **Progettazione architetturale** — diagramma ASCII a livelli + modello dati + contratti API
- **Scomposizione delle attività** — grafico delle dipendenze + percorso critico + stima dei tempi
- **Monitoraggio dei progressi** — registrazione di ogni passo + riepilogo delle tappe fondamentali
- **Zero conflitti** — non modifica i file di configurazione di altri plugin IDE

## Installazione

### Metodo 1: Installazione globale (consigliata)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Metodo 2: Installazione a livello di progetto

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Configurazione

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

## Flusso di lavoro

Richiesta utente → identificazione attività di generazione codice → salto pianificazione? → classificazione dominio → analisi requisiti → progettazione tecnica → scomposizione attività → esecuzione per attività

Artefatti: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Compatibilità

Non modifica i file di configurazione `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` di altri plugin.

## Licenza

MIT
