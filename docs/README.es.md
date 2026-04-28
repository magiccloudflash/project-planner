# Project Planner — Habilidad de IA para OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** es una habilidad del OpenCode Agent que impone un proceso profesional de planificación de proyectos antes de la generación de código, garantizando un análisis de requisitos, diseño de arquitectura, descomposición de tareas y seguimiento de progreso claros.

## Características

- **Planificación obligatoria** — cualquier tarea de generación de código debe planificarse primero, a menos que el usuario la omita explícitamente
- **Clasificación de dominio** — identificación automática del tipo de proyecto (Web/CLI/Library/Mobile) con aplicación de las mejores prácticas correspondientes
- **Análisis de requisitos** — 14 dimensiones para aclarar requisitos + tres niveles de prioridad (P0/P1/P2)
- **Evaluación de riesgos** — identificación, clasificación y estrategias de mitigación para 6 categorías de riesgo
- **Diseño de arquitectura** — diagrama ASCII de capas + modelo de datos + contratos de API
- **Descomposición de tareas** — grafo de dependencias + ruta crítica + estimación de tiempo
- **Seguimiento de progreso** — registro de cada paso + resumen de hitos
- **Cero conflictos** — no modifica archivos de configuración de otros plugins IDE

## Instalación

### Método 1: Instalación global (recomendado)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Método 2: Instalación por proyecto

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Configuración

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

## Flujo de trabajo

Solicitud del usuario → identificación de tarea de generación de código → ¿omitir planificación? → clasificación de dominio → análisis de requisitos → diseño técnico → descomposición de tareas → ejecución por tarea

Artefactos: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Compatibilidad

No modifica los archivos de configuración `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` de otros plugins.

## Licencia

MIT
