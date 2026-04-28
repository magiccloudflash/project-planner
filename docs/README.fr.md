# Project Planner — Compétence AI pour OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** est une compétence OpenCode Agent qui applique un processus professionnel de planification de projet avant la génération de code, garantissant une analyse des besoins, une conception architecturale, une décomposition des tâches et un suivi de progression clairs.

## Fonctionnalités

- **Planification obligatoire** — toute tâche de génération de code doit d'abord être planifiée, sauf si l'utilisateur l'ignore explicitement
- **Classification du domaine** — identification automatique du type de projet (Web/CLI/Library/Mobile) avec application des meilleures pratiques correspondantes
- **Analyse des besoins** — 14 dimensions pour clarifier les exigences + trois niveaux de priorité (P0/P1/P2)
- **Évaluation des risques** — identification, évaluation et stratégies d'atténuation pour 6 catégories de risques
- **Conception architecturale** — diagramme ASCII des couches + modèle de données + contrats API
- **Décomposition des tâches** — graphe des dépendances + chemin critique + estimation du temps
- **Suivi de progression** — enregistrement de chaque étape + résumé des jalons
- **Zéro conflit** — ne modifie aucun fichier de configuration des autres plugins IDE

## Installation

### Méthode 1 : Installation globale (recommandée)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Méthode 2 : Installation par projet

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Configuration

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

## Flux de travail

Demande utilisateur → identification d'une tâche de génération de code → saut de planification ? → classification du domaine → analyse des besoins → conception technique → décomposition des tâches → exécution par tâche

Artefacts : `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Compatibilité

Ne modifie pas les fichiers de configuration `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` des autres plugins.

## Licence

MIT
