# Project Planner — Skill de IA para OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** é uma skill do OpenCode Agent que impõe um processo profissional de planejamento de projetos antes da geração de código, garantindo análise de requisitos, design de arquitetura, decomposição de tarefas e acompanhamento de progresso claros.

## Funcionalidades

- **Planejamento obrigatório** — qualquer tarefa de geração de código deve passar por planejamento primeiro, a menos que o usuário explicitamente pule essa etapa
- **Classificação de domínio** — identificação automática do tipo de projeto (Web/CLI/Library/Mobile) com aplicação das melhores práticas correspondentes
- **Análise de requisitos** — 14 dimensões para esclarecer requisitos + três níveis de prioridade (P0/P1/P2)
- **Avaliação de riscos** — identificação, classificação e estratégias de mitigação para 6 categorias de risco
- **Design de arquitetura** — diagrama ASCII de camadas + modelo de dados + contratos de API
- **Decomposição de tarefas** — grafo de dependências + caminho crítico + estimativa de tempo
- **Acompanhamento de progresso** — registro de cada etapa + resumo de marcos
- **Zero conflitos** — não modifica arquivos de configuração de outros plugins IDE

## Instalação

### Método 1: Instalação global (recomendado)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### Método 2: Instalação por projeto

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## Configuração

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

## Fluxo de trabalho

Solicitação do usuário → identificação de tarefa de geração de código → pular planejamento? → classificação de domínio → análise de requisitos → design técnico → decomposição de tarefas → execução por tarefa

Artefatos: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## Compatibilidade

Não modifica arquivos de configuração `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/` de outros plugins.

## Licença

MIT
