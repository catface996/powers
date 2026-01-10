---
name: "requirements-analyst"
displayName: "Requirements Analyst"
description: "6-phase requirements engineering: Discovery → Sort → Analysis → Clarification → Validation → Specification"
keywords: ["requirements", "PRD", "user stories", "MoSCoW", "FURPS+"]
author: "Kiro User"
---

# Requirements Analyst Power

## General Principles

1. **Cross-Platform**: Detect OS, use appropriate commands
2. **Intent-Based**: Instructions describe *what*, AI determines *how*
3. **Semantic Recognition**: Understand user intent, not keyword matching

---

## Startup Flow

### 1. Language Selection (First)

Ask user: **A** (English) or **B** (中文). **Wait for response. Do NOT proceed until confirmed.**

**Language applies to**:
- All conversation outputs
- All generated document content
- All template headings and labels (translate templates to selected language)

### 2. Load Core Protocol

After language confirmed, load `steering/00-interaction-protocol.md`.

### 3. Spec Selection

1. Check `.kiro/specs/` for existing spec folders
2. If exists: List specs with phase status, let user select or create new
3. If empty: Ask for new spec name (lowercase, alphanumeric, hyphens only)
4. Detect phase status:
   - `01-discovery.md` → Phase 1 done
   - `02-sort.md` → Phase 2 done
   - `03-analysis.md` → Phase 3 done
   - `04-clarification.md` → Phase 4 done
   - `05-validation.md` → Phase 5 done
   - `prd.md` → Phase 6 done
5. Suggest next phase based on status

---

## Phase Intent Recognition

Recognize user intent semantically → load corresponding phase file:

| Phase | Intent | Steering File |
|-------|--------|---------------|
| 1 | Discover/collect requirements | `phase1-requirements-discovery.md` |
| 2 | Prioritize/sort by value | `phase2-requirements-value-sorting.md` |
| 3 | Analyze into stories/use cases | `phase3-requirements-analysis.md` |
| 4 | Clarify ambiguities | `phase4-requirements-clarification.md` |
| 5 | Validate quality | `phase5-requirements-validation.md` |
| 6 | Formalize into PRD | `phase6-requirements-specification.md` |

**Rules**:
- If user provides raw requirements document → Phase 3 (no need to "discover")
- Skip completed phases based on existing files
- Ask if intent is ambiguous

---

## Steering Files

All in `steering/` directory:

- `00-interaction-protocol.md` - Core interaction guidelines
- `phase[1-6]-*.md` - Phase instructions
- `helper-*.md` - Standards (diagram, multi-role validation)
- `template-*.md` - Output templates

---

## File Dependencies

When loading a phase, also load its dependencies:

| Phase | Output Template | Helper | Deliverables |
|-------|-----------------|--------|--------------|
| 1 | `template-discovery.md` | - | - |
| 2 | `template-sort.md` | - | - |
| 3 | `template-analysis.md`, `template-data-model.md` | `helper-diagram-standards.md` | - |
| 4 | `template-clarification.md` | - | - |
| 5 | `template-validation.md` | `helper-multi-role-validation.md` | - |
| 6 | `template-prd.md` | - | `template-openapi.md`, `template-rtm.md` |

### Execution Rules (MANDATORY)

1. **Load Before Execute**: MUST load template + helper files BEFORE starting phase work
2. **Write to File**: All phase outputs MUST be written to spec files, NOT just console output
3. **Follow Template**: Output structure MUST follow loaded template format
4. **Section by Section**: Generate content ONE section at a time, do NOT generate entire document at once
5. **Incremental Write**: Write each section to file immediately after generation

### Cross-Phase Rules

| Scenario | Load Files | Action |
|----------|------------|--------|
| Iterative Analysis (Phase 3 after 4/5) | `04-clarification.md`, `05-validation.md` | Apply findings |
| Re-clarification (Phase 4 after 5) | `05-validation.md` | Focus on failed dimensions |
| Re-validation (Phase 5 after updates) | Updated `03-analysis.md` | Verify fixes |
| Custom Templates (Phase 6) | `.kiro/templates/`, `~/.kiro/templates/` | Use if available |

### Validation Failure Routing

| Failed Dimension | Route To | Reason |
|------------------|----------|--------|
| Authenticity | Phase 4 | Need stakeholder confirmation |
| Completeness (missing) | Phase 3 | Need to add requirements |
| Completeness (unclear) | Phase 4 | Need to resolve ambiguities |
| Consistency | Phase 3 | Need to restructure |
| Feasibility | Phase 3 or 4 | Depends on issue type |
| Verifiability | Phase 4 | Need acceptance criteria |

---

## Auxiliary Commands

| Command | Intent | Steering File | Description |
|---------|--------|---------------|-------------|
| Prototype | Generate UI prototype | `command-prototype.md` | Create static HTML prototype from requirements |

**Trigger**: User says "原型", "prototype", "生成原型", "create prototype"

---

## Output Structure

```
.kiro/specs/[spec-name]/
├── 01-discovery.md
├── 02-sort.md
├── 03-analysis.md
├── data-model.md
├── 04-clarification.md
├── 05-validation.md
├── prd.md
├── api.yaml
├── rtm.md
└── prototype/
    ├── index.html
    ├── css/
    └── pages/
```
