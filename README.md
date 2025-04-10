# AI Agile Standards (v1.0)

> This document defines the core standards for implementing the **AI Agile methodology** — a fully autonomous, multi-agent framework for software development without human involvement.

---

## 📘 Table of Contents

- [1. Task Specification Standard](#1-task-specification-standard)
- [2. Agent Role Definitions](#2-agent-role-definitions)
- [3. Confidence Score Guidelines](#3-confidence-score-guidelines)
- [4. Validation Pipeline](#4-validation-pipeline)
- [5. Commit & Traceability](#5-commit--traceability)
- [6. Project Structure Convention](#6-project-structure-convention)
- [7. Memory & Feedback Logging](#7-memory--feedback-logging)
- [8. Time & Sync Rhythm](#8-time--sync-rhythm)
- [9. Changelog](#9-changelog)

---

## 1. Task Specification Standard

All tasks must follow a structured JSON format to ensure clarity and interoperability between agents.

```json
{
  "task_id": "T0001",
  "title": "Implement login form",
  "description": "Create a responsive login form with email/password inputs.",
  "role": "developer",
  "priority": "high",
  "status": "pending",
  "linked_epic": "E001",
  "dependencies": ["T0002"],
  "acceptance_criteria": [
    "Form must be mobile-friendly",
    "Password must be masked",
    "Submit button should trigger POST"
  ],
  "created_by": "project_owner",
  "confidence_threshold": 0.85
}
```

---

## 2. Agent Role Definitions

| Role | Functions | Input | Output |
|------|-----------|--------|--------|
| `business_analyst` | Translate intent → user goals | `intent` | `goals.json` |
| `project_owner` | Goals → Epics/Tasks | `goals.json` | `task_list.json` |
| `architect` | Plan stack/system | `task_list.json` | `architecture.yaml` |
| `software_manager` | Validate hierarchy, assign stories | `architecture.yaml` | `sprint_plan.json` |
| `developer` | Implement features/tests | `task.json` | `code/`, `test/` |
| `reviewer` | Code review + test analysis | `code/` | `review.json` |
| `integrator` | Merge, deploy, log | `approved_code/` | `deployment.yaml` |
| `meta_agent` | Strategy optimizer | `logs/`, `status/` | `updates.json` |

> Each role will have a dedicated spec file in `/agents/<role>.md`

---

## 3. Confidence Score Guidelines

Each agent attaches a confidence score (float between `0.0` and `1.0`) to its output.

| Range | Meaning |
|-------|---------|
| 0.90–1.00 | High confidence → auto-merge allowed |
| 0.70–0.89 | Moderate → needs review |
| < 0.70 | Retry or escalate to another agent |

---

## 4. Validation Pipeline

Each output must pass a standardized validation process.

**Requirements:**
- JSON schema conformity
- Code linting / formatting
- Test coverage threshold
- Acceptance criteria match
- Architecture & file location compliance

Each task must include a `validation_report.json` file:

```json
{
  "lint_passed": true,
  "tests_passed": true,
  "coverage": 94,
  "accepted": true
}
```

---

## 5. Commit & Traceability

All commits should follow this pattern:

```
<type>(<scope>): <description> [task_id]
```

**Example:**
```
feat(auth): Add login form [T0001]
Agent: dev-frontend-v2 | Confidence: 0.91 | Review: Passed
```

Link to issue/task system for full traceability.

---

## 6. Project Structure Convention

```
/project-root
  /agents
  /epics
  /tasks
  /src
    /components
    /pages
    /utils
  /tests
  /memory
  /logs
```

---

## 7. Memory & Feedback Logging

Agents must record metadata for each task:

- Decision rationale
- Errors encountered
- Improvements made
- Final result (and confidence)

Memory is stored in both text and vector format for future agent reference.

---

## 8. Time & Sync Rhythm

Instead of sprints, AI Agile uses system ticks:

- `tick`: Every 10 mins → agents report status
- `cycle`: Every hour → backlog re-evaluated

This allows continuous adaptation and near real-time progress.

---

## 9. Changelog

### v1.0
- Initial version of AI Agile standards.
- Includes task schema, role definitions, validation rules, confidence scoring, and sync rhythm.

