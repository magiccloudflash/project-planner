---
name: project-planner
description: Mandatory project planning before code generation — requirement analysis, architecture design, task breakdown, risk assessment, and development tracking with professional-grade detail and accuracy
license: MIT
compatibility: opencode
metadata:
  audience: developer
  workflow: planning
  version: 2.0.0
---

# Core rule — Planning is mandatory

**Any code generation task MUST go through planning first.** This includes: writing new code, refactoring, adding features, creating files, fixing bugs that require structural changes.

The **only** exception: the user explicitly says they do not need planning (e.g. "不需要规划", "skip planning", "just write the code", "直接写代码").

Planning artifacts are written into `memory/project-planner/`. This directory is a dedicated namespace that does not conflict with other IDE plugins.

# Compatibility with other plugins

This skill **never**:
- Modifies or creates files in `.vscode/`, `.cursor/`, `.continue/`, `.github/`, `.idea/`, or any plugin config directories
- Injects into or intercepts other plugin workflows
- Overwrites files created by other AI plugins

# Workflow overview

```
[User request]
    │
    ▼
┌─────────────────────────────────┐
│ Step 0: Domain Classification   │
│ Identify project type &         │
│ applicable standards            │
└──────────────┬──────────────────┘
               ▼
┌─────────────────────────────────┐
│ PHASE 1: Requirement Analysis   │
│ ─ Clarify & Scope & Risk       │
│   Output → plan.md              │
└──────────────┬──────────────────┘
               ▼ (user confirms)
┌─────────────────────────────────┐
│ PHASE 2: Technical Design       │
│ ─ Architecture & Data & API    │
│   Output → design.md            │
└──────────────┬──────────────────┘
               ▼ (user confirms)
┌─────────────────────────────────┐
│ PHASE 3: Task Breakdown         │
│ ─ Granular tasks & dependencies │
│   Output → tasks.md             │
└──────────────┬──────────────────┘
               ▼
┌─────────────────────────────────┐
│ PHASE 4: Task-Driven Execution  │
│ ─ One task at a time            │
│   Output → progress.md          │
└─────────────────────────────────┘
```

If the user says "不需要规划" or "跳过规划", skip directly to coding.

---

# Step 0: Domain Classification

Before any analysis, classify the project domain. This determines architectural patterns, naming conventions, file structure, and default technology recommendations.

## Domain taxonomy

| Domain | Typical patterns | Common tech | File conventions |
|--------|-----------------|-------------|------------------|
| **Web Frontend** | Component-based, SPA/SSR | React/Vue/Svelte, Next/Nuxt | `src/components/`, `src/pages/` |
| **Web Backend** | MVC/Clean/Hexagonal | Express/Fastify/Django/Spring | `src/routes/`, `src/services/` |
| **Fullstack** | Client-Server, BFF | Next.js/Remix/SvelteKit | `client/` + `server/` |
| **CLI Tool** | Command pattern | Commander/Cobra/Click | `src/commands/` |
| **Library/SDK** | Facade/Builder | Language-native | `src/`, `index.ts` |
| **Mobile App** | MVVM/MVI | Flutter/React Native/SwiftUI | Platform-specific |
| **Desktop App** | MVC/Redux-like | Electron/Tauri/WPF | `src/main/`, `src/renderer/` |
| **Data Pipeline** | ETL/DAG | Python/Airflow/Spark | `src/extractors/`, `src/loaders/` |
| **DevOps/Infra** | IaC | Terraform/Ansible/Pulumi | `modules/`, `environments/` |
| **Database Driven** | Repository pattern | ORM/SQL | `migrations/`, `models/` |
| **AI/ML** | Pipeline/Serving | PyTorch/TF/FastAPI | `data/`, `models/`, `inference/` |

## Domain classification output

Write into `plan.md` header:
```markdown
## Domain
- **Type**: <domain>
- **Pattern**: <architectural pattern>
- **Language**: <primary language + version>
```

---

# Phase 1: Requirement Analysis

## 1.1 Requirements Elicitation

Ask targeted questions in this order. Do NOT move to next question until current is answered:

### Must-clarify (ask first)
1. **Core purpose** — What problem does this solve? Who is the end user?
2. **Input/Output** — What data goes in? What comes out?
3. **User journey** — What is the primary user flow? (step by step)
4. **Environment** — Where does this run? (browser/Node/server/mobile/desktop)
5. **Existing codebase** — Is this a new project or modifying an existing one?

### Should-clarify (ask if relevant)
6. **Performance requirements** — Expected throughput? Latency budget? Data volume?
7. **Security requirements** — Auth? Data sensitivity? Compliance (GDPR/SOC2)?
8. **Scale** — Number of users? Concurrent requests? Dataset size?
9. **Integration points** — External APIs? Databases? Message queues?
10. **Deployment** — How will this be deployed? CI/CD requirements?

### Optional (ask only if project complexity warrants)
11. **i18n/l10n** — Multiple languages needed?
12. **Accessibility** — WCAG compliance level?
13. **Offline support** — Required?
14. **Browser/device targets** — Specific versions or platforms?

## 1.2 Scope Definition

Define three priority tiers:

| Tier | Definition | Rule |
|------|-----------|------|
| **P0 (MVP)** | Core functionality, must work for launch | Implement first |
| **P1 (Important)** | Enhances value, can follow post-MVP | Implement after P0 complete |
| **P2 (Nice-to-have)** | Polish, edge cases, future | Explicitly deferred |

Each feature/requirement must be tagged with one tier.

## 1.3 Risk Assessment

Identify and rate risks:

| Risk ID | Description | Likelihood | Impact | Mitigation |
|---------|-------------|-----------|--------|------------|
| R-001 | <risk> | High/Med/Low | High/Med/Low | <mitigation strategy> |

Risk categories to consider:
- **Technical risk** — unproven technology, performance bottlenecks
- **Dependency risk** — reliance on unstable/abandoned packages
- **Integration risk** — external API changes, data format mismatches
- **Scope risk** — requirements ambiguity, scope creep
- **Security risk** — data exposure, injection vectors
- **Resource risk** — missing skills, time constraints

## 1.4 Success Criteria

Define measurable acceptance criteria. Use this format:

```markdown
## Acceptance Criteria

### Functional
- [ ] AC-001: <criterion> (verified by: <method>)
- [ ] AC-002: <criterion> (verified by: <method>)

### Non-Functional
- [ ] NF-001: Performance — <metric> <target> (verified by: <method>)
- [ ] NF-002: Security — <requirement> (verified by: <method>)
- [ ] NF-003: Accessibility — <standard> (verified by: <method>)
```

Each criterion must be:
1. **Specific** — clear pass/fail condition
2. **Measurable** — quantifiable or demonstrable
3. **Verifiable** — method to confirm
4. **Traceable** — links to a requirement from §1.2

## 1.5 Technology Selection

**Rule**: Check existing codebase first before suggesting new dependencies.

```
Step 1: Read existing config files
  → package.json / Cargo.toml / requirements.txt / go.mod / pyproject.toml / Gemfile

Step 2: List existing dependencies relevant to the task

Step 3: ONLY introduce new dependencies IF:
  a) No existing dependency serves the purpose, AND
  b) The dependency is well-maintained (recent commits, >1k stars), AND
  c) Justify each new dependency with a reason
```

For each new dependency, document:
```markdown
| Dependency | Version | Purpose | Alternatives considered | Why chosen |
|------------|---------|---------|------------------------|------------|
| <name>     | <ver>   | <why>   | <alt1, alt2>           | <reason>   |
```

## 1.6 Output → `memory/project-planner/plan.md`

Complete template:

```markdown
# Project Plan — <Project Name>

## Domain
- **Type**: <domain from taxonomy>
- **Pattern**: <architectural pattern>
- **Language**: <primary language + version>

## Overview
<1 paragraph describing what this project does, who uses it, and the core value>

## User Persona
- **Primary user**: <description>
- **User goal**: <what they want to accomplish>

## User Journey (Primary Flow)
<numbered step-by-step flow of the core user scenario>

## Scope

### P0 — MVP (Must Have)
| ID   | Feature | Description | AC |
|------|---------|-------------|----|
| F-001 |         |             | AC-001 |

### P1 — Important
| ID   | Feature | Description | AC |
|------|---------|-------------|----|

### P2 — Deferred
| ID   | Feature | Description | AC |
|------|---------|-------------|----|

### Explicitly Out of Scope
- <item not to be done>

## Acceptance Criteria

### Functional
- [ ] AC-001: <criterion> (verified by: <method>)

### Non-Functional
- [ ] NF-001: <criterion> (verified by: <method>)

## Technology Choices

| Dependency | Version | Purpose | Why chosen |
|------------|---------|---------|------------|
| <name>     | <ver>   | <why>   | <reason>   |

## Risk Matrix

| ID   | Description | Likelihood | Impact | Mitigation |
|------|-------------|-----------|--------|------------|
| R-001 |             | High/Med/Low | High/Med/Low | |

## Constraints
- <technical, business, or resource constraints>

## External Dependencies
| Name | Type | Endpoint/Version | Failure mode |
|------|------|------------------|--------------|
|      | API/DB/Service | | |

## Assumptions
- <documented assumptions that could affect planning>
```

---

# Phase 2: Technical Design

After the user confirms Phase 1, proceed to technical design.

## 2.1 Architecture Design

### Mandatory elements

1. **Architecture style** — monolithic / microservices / serverless / plugin-based
2. **Layer diagram** (ASCII) showing module decomposition
3. **Data flow** — how data moves through the system
4. **Component responsibilities** — what each module owns

Example ASCII diagram:

```
┌──────────────────────────────────────────────┐
│                  Presentation                 │
│  ┌──────────┐  ┌──────────┐  ┌────────────┐ │
│  │  Routes   │  │Components│  │  Templates │ │
│  └─────┬─────┘  └────┬─────┘  └─────┬──────┘ │
│        └──────────────┼──────────────┘        │
├───────────────────────┼───────────────────────┤
│                  Business Logic              │
│  ┌──────────┐  ┌──────┴──────┐  ┌──────────┐ │
│  │ Services │  │  Use Cases  │  │Validators│ │
│  └─────┬─────┘  └──────┬──────┘  └──────────┘ │
├────────┼───────────────┼──────────────────────┤
│        │          Data Access                 │
│  ┌─────┴─────┐  ┌──────┴──────┐  ┌──────────┐ │
│  │Repository │  │    Models   │  │  Migrations│ │
│  └───────────┘  └─────────────┘  └──────────┘ │
└──────────────────────────────────────────────┘
```

## 2.2 Data Model Design

For each entity, define:
- Field name, type, constraints
- Relationships (one-to-many, many-to-many, etc.)
- Validation rules
- Indexes (for databases)

```markdown
### Entity: <Name>

| Field    | Type      | Required | Constraints       | Description |
|----------|-----------|----------|-------------------|-------------|
| id       | UUID/Int  | Yes      | PK, auto-generated |             |
| name     | String    | Yes      | max 255 chars      |             |
| ...      |           |          |                    |             |

**Relationships**: <EntityA> ──1:N──> <EntityB>
**Indexes**: idx_<entity>_<field> ON <field>
**Validation**: <rules>
```

## 2.3 API Contract Design (if applicable)

For APIs, define endpoints with full request/response specs:

```markdown
### POST /api/v1/resource

**Purpose**: <what this endpoint does>

**Request**:
- Method: POST
- Path: /api/v1/resource
- Headers: Authorization: Bearer <token>, Content-Type: application/json

**Request Body**:
```json
{
  "field": "type",
  "optionalField?": "type"
}
```

**Success Response (201)**:
```json
{
  "id": "uuid",
  "field": "value",
  "createdAt": "ISO8601"
}
```

**Error Responses**:
| Code | Condition | Response Body |
|------|-----------|---------------|
| 400  | Validation error | `{ "error": "message", "fields": {} }` |
| 401  | Unauthorized | `{ "error": "message" }` |
| 404  | Not found | `{ "error": "message" }` |
| 500  | Server error | `{ "error": "Internal server error" }` |



## 2.4 Error Handling Strategy

Define how errors are handled at each layer:

```markdown
| Layer | Error Type | Handling | User-Facing |
|-------|-----------|----------|-------------|
| Routes | 4xx, 5xx | Status codes + body | Yes |
| Services | Business logic errors | Custom exceptions | Mapped by routes |
| Repository | DB errors | Wrapped in domain errors | No |
| External APIs | Network/timeout | Retry + circuit breaker | Degraded response |
```

## 2.5 File Structure Projection

Project the complete file tree before writing any code:

```
project-root/
├── src/
│   ├── components/      # UI components (if frontend)
│   ├── services/        # Business logic
│   ├── repositories/    # Data access
│   ├── models/          # Data models / types
│   ├── routes/          # API routes / pages
│   ├── utils/           # Shared utilities
│   ├── config/          # Configuration
│   └── index.ts         # Entry point
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── docs/                # Documentation (optional)
├── scripts/             # Build/deploy scripts
├── package.json
├── tsconfig.json
└── README.md
```

## 2.6 Test Strategy

Define testing approach by layer:

| Layer | Test Type | Framework | Coverage Target | What to Test |
|-------|-----------|-----------|----------------|--------------|
| Routes | Integration | Supertest/Playwright | All endpoints | Request/response, auth, errors |
| Services | Unit | Jest/Vitest | >80% | Business logic, edge cases |
| Repositories | Unit | Jest/Vitest | >80% | Queries, transactions |
| Components | Unit | Testing Library | >80% | Rendering, interactions |
| E2E | End-to-end | Playwright/Cypress | Critical paths | User journeys |

## 2.7 Output → `memory/project-planner/design.md`

```markdown
# Technical Design — <Project Name>

## Architecture
### Style: <chosen style>
### Layer Diagram
<ASCII diagram>

### Component Responsibilities
| Component | Responsibility | Depends On |
|-----------|---------------|------------|
| <name>    | <what it does> | <other components> |

## Data Flow
<Describe key data flows through the system>

## Data Model
<entities with field tables>

## API Contracts
<endpoint specifications>

## Error Handling
<error strategy table>

## File Structure
<complete projected file tree>

## Test Strategy
<testing approach table>

## Key Design Decisions
| Decision | Options Considered | Chosen | Rationale |
|----------|-------------------|--------|-----------|
|          |                   |        |           |
```

---

# Phase 3: Task Breakdown

After the user confirms Phase 2, break down into granular tasks.

## 3.1 Task Granularity Rules

Each task must be:
- **Independently executable** — can be completed in one session
- **Verifiable** — has a clear "done" condition matching an AC from plan.md
- **Self-contained** — produces a working increment (not broken state)
- **Atomic scope** — touches ≤5 files (if more, split further)

## 3.2 Task Dependency Graph

Before listing tasks, draw the dependency graph:

```
T-001 (Setup & Config)
  ├──→ T-002 (Data Models)
  │      ├──→ T-003 (Repositories)
  │      ├──→ T-004 (Services)
  │      └──→ T-005 (Routes)
  │             └──→ T-006 (Integration Tests)
  └──→ T-007 (Config Loaders)
         └──→ T-008 (Error Handling)
```

## 3.3 Task Specification

For each task, provide full detail:

```markdown
### T-001: Project Setup & Dependencies
- **Phase**: Scaffolding
- **Status**: pending
- **Priority**: P0
- **Depends on**: none
- **Complexity**: low
- **Estimated effort**: 15-30 min
- **Files to create**:
  - `package.json` — with dependencies
  - `tsconfig.json` — strict mode
  - `src/index.ts` — entry point skeleton
- **Files to modify**: none
- **Details**:
  1. Initialize project with `npm init`
  2. Install dependencies: <list>
  3. Configure TypeScript with strict mode
  4. Create entry point with basic server/listener
  5. Add npm scripts: `dev`, `build`, `test`, `lint`
- **Acceptance**: Server starts without errors on `npm run dev`
- **AC Mapping**: None (infrastructure)
```

## 3.4 Critical Path Identification

Mark the critical path (tasks that cannot be delayed without delaying the project):

```
Critical Path: T-001 → T-002 → T-004 → T-005 → T-007 → T-009 → T-012
```

## 3.5 Output → `memory/project-planner/tasks.md`

```markdown
# Task List — <Project Name>

## Dependency Graph
<ASCII dependency graph>

## Critical Path
<list of task IDs on critical path>

## Phase: Scaffolding
| ID   | Task         | Priority | Depends On | Complexity | Est. Effort | Status  |
|------|-------------|----------|------------|------------|-------------|---------|
| T-001 | Setup       | P0       | -          | Low        | 15-30m      | pending |

## Phase: Core Implementation
| ID   | Task         | Priority | Depends On | Complexity | Est. Effort | Status  |
|------|-------------|----------|------------|------------|-------------|---------|
| T-002 | Data Models | P0       | T-001      | Medium     | 30-60m      | pending |

## Phase: Testing
| ID   | Task         | Priority | Depends On | Complexity | Est. Effort | Status  |
|------|-------------|----------|------------|------------|-------------|---------|

## Phase: Polish
| ID   | Task         | Priority | Depends On | Complexity | Est. Effort | Status  |
|------|-------------|----------|------------|------------|-------------|---------|

---

## Task Details

### T-001: <Name>
- **Phase**: <phase>
- **Status**: pending
- **Priority**: P0/P1/P2
- **Depends on**: <task IDs>
- **Complexity**: low/medium/high
- **Estimated effort**: <time>
- **Files to create**: <list>
- **Files to modify**: <list>
- **Details**: <numbered steps>
- **Acceptance**: <measurable condition>
- **AC Mapping**: AC-001, AC-003
- **Risks**: R-001 (if applicable)
```

---

# Phase 4: Task-Driven Execution

## 4.1 Pre-Execution Checklist (before each task)

Before starting a task, verify:
- [ ] All dependencies (`Depends on`) are `completed`
- [ ] Re-read relevant existing files (use `read` tool)
- [ ] Understand the task's `Acceptance` condition
- [ ] Identify the `AC Mapping` from `plan.md`
- [ ] Re-read the `Design Decision` from `design.md` if relevant

## 4.2 During Execution

- Follow the file structure from `design.md`
- Follow the naming conventions and patterns from `design.md`
- Write code that satisfies the task's `Acceptance` condition
- If the approach in `design.md` proves wrong, **pause** and report to user before deviating

## 4.3 Post-Execution Checklist (after each task)

- [ ] Code compiles / no syntax errors
- [ ] Relevant tests pass
- [ ] Lint passes (if configured)
- [ ] Update task status to `completed` in `tasks.md`
- [ ] Append to `progress.md` (see §4.4)
- [ ] Report to user: "✓ T-XXX completed: <summary>"

## 4.4 Progress Logging

After each task, append to `memory/project-planner/progress.md`:

```markdown
# Progress Log — <Project Name>

## YYYY-MM-DD HH:MM — T-001 Completed ✓
- Created: `package.json`, `tsconfig.json`, `src/index.ts`
- Installed dependencies: express, typescript, vitest, eslint
- Acceptance: Server starts without errors — PASSED
- Blockers: None
- Notes: <any observations or deviations>

## YYYY-MM-DD HH:MM — T-002 Started
```

## 4.5 Dealing with Blockers

If a task cannot proceed:
1. Mark task as `blocked` in `tasks.md`
2. Record the blocker reason in `progress.md`
3. Ask user for input or decision
4. If dependent tasks can proceed, continue with next available task

## 4.6 Deviation Management

If implementation must diverge from the plan:
1. **Pause** before making the change
2. **Explain** the discrepancy to the user
3. Get **explicit approval** to deviate
4. **Update** `plan.md` or `design.md` to reflect the new direction
5. **Continue** with the updated plan

## 4.7 Milestone Review

After completing all tasks in a phase, present a milestone summary:

```markdown
### Milestone: <Phase Name> — Complete

**Completed**: T-001 through T-005 (5 tasks)
**Acceptance criteria met**: AC-001, AC-002, AC-003 (3/8 total)
**Deviations from plan**: None / <list>
**Files created/modified**: 12 files
**Next milestone**: Core Implementation (T-006 through T-012)
```

---

# Response Format

## When entering planning mode

```markdown
## Project Planner v2 — <Project Name>

### Step 0: Domain Classification
- **Type**: <domain>
- **Pattern**: <pattern>
- **Language**: <language>

### Phase 1: Requirement Analysis
To begin, I need to clarify the following:

1. **Core purpose**: <question>
2. **Input/Output**: <question>
3. **Environment**: <question>
...

Please answer these questions so I can build the detailed plan.
```

## When presenting a completed plan for approval

```markdown
## Project Plan Complete

**Plan**: `memory/project-planner/plan.md`
**Design**: `memory/project-planner/design.md`
**Tasks**: `memory/project-planner/tasks.md`

### Summary
- **Total tasks**: <N>
- **P0 (MVP) tasks**: <N>
- **Estimated total effort**: <time range>
- **Critical path length**: <N tasks>
- **Risks identified**: <N> (highest: <risk description>)

### Phases
1. Scaffolding: T-001 to T-003 (3 tasks)
2. Core Implementation: T-004 to T-012 (9 tasks)
3. Testing: T-013 to T-016 (4 tasks)
4. Polish: T-017 to T-019 (3 tasks)

### Next step
Confirm this plan to begin execution, or suggest changes.

(Reply "yes" / "go ahead" / "开始" to proceed, or "修改 XXX" to adjust)
```

## When reporting task completion

```markdown
✓ T-XXX completed: <task name>
- Files: <created/modified list>
- Tests: <passed/failed>
- AC: AC-XXX — PASSED
- (Next: T-YYY — <next task name>)
```

---

# Verification Checklist

Before writing any code, the AI must:
- [ ] Domain classification completed (Step 0)
- [ ] `plan.md` exists with all sections filled AND user-approved
- [ ] `design.md` exists with architecture defined AND user-approved
- [ ] `tasks.md` exists with dependency graph AND user-approved
- [ ] All dependencies in `plan.md` verified available (check `package.json` etc.)
- [ ] No other plugin config files will be modified
- [ ] File structure projection matches domain conventions
