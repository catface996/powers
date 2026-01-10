---
name: "requirements-analyst"
displayName: "Requirements Analyst"
description: "Complete requirements engineering power with 6-phase methodology: Discovery, Value Sorting, Analysis, Clarification, Validation, and Specification"
keywords: ["requirements", "analysis", "clarification", "validation", "user stories", "acceptance criteria", "specification", "PRD", "BRD", "FURPS+", "KANO", "MoSCoW", "BDD", "GWT"]
author: "Kiro User"
---

# Requirements Analyst Power

A comprehensive requirements engineering power that guides you through the complete lifecycle of requirements management—from initial discovery to formal specification and baseline establishment.

---

## MANDATORY FIRST STEP: Language Selection

**CRITICAL**: You MUST ask user to select language BEFORE any other interaction. This is NON-NEGOTIABLE.

When user activates this power, you MUST first display this prompt:

```
Requirements Analyst Power activated.

Please select your preferred language / 请选择您的首选语言:

► **A** - English
  _All conversations and generated documents will be in English_

► **B** - 中文
  _所有对话和生成的文档都将使用中文_

---
Reply with "A" or "B" / 请回复 "A" 或 "B"
```

**WAIT for user response before proceeding.**

**Do NOT proceed with ANY workflow steps until language is confirmed.**

Once language is selected:
1. Use the selected language for ALL subsequent outputs
2. Proceed to Spec Selection (next section)

---

## MANDATORY SECOND STEP: Spec Selection

**CRITICAL**: After language selection, you MUST check for existing specs and prompt user to select or create.

### Step 1: Check for Existing Specs

Check if `.kiro/specs/` directory exists and contains any spec folders:

```bash
ls -d .kiro/specs/*/ 2>/dev/null
```

### Step 2: Prompt Based on Results

#### If Specs Exist:

Display the following prompt (use selected language):

```
Found existing specs in .kiro/specs/:

| # | Spec Name | Last Modified | Status |
|---|-----------|---------------|--------|
| 1 | [folder-name-1] | [date] | [phase status] |
| 2 | [folder-name-2] | [date] | [phase status] |
| ... | ... | ... | ... |

**What would you like to do?**

> **[1-N]** - Continue working on an existing spec (enter number)
> **N** - Create a **N**ew spec

---
Reply with a number to select existing spec, or "N" to create new.
```

#### If No Specs Exist:

Display the following prompt:

```
No existing specs found.

**Please provide a name for your new spec:**

> Example: "user-authentication", "payment-system", "dashboard-redesign"

---
Enter spec name (lowercase, use hyphens for spaces):
```

### Step 3: Handle User Response

#### If User Selects Existing Spec:

1. Set working spec to selected folder
2. Detect current phase status by checking which files exist:
   - `01-discovery.md` exists → Phase 1 completed
   - `02-sort.md` exists → Phase 2 completed
   - `03-analysis.md` exists → Phase 3 completed
   - `04-clarification.md` exists → Phase 4 completed
   - `05-validation.md` exists → Phase 5 completed
   - `prd.md` exists → Phase 6 completed
3. Suggest next phase or show phase menu

#### If User Creates New Spec:

1. Validate spec name (lowercase, alphanumeric, hyphens only)
2. Create directory: `.kiro/specs/[spec-name]/`
3. Confirm creation and proceed to Phase 1 (Discovery)

### Step 4: Confirm and Proceed

Display confirmation (use selected language):

```
Working spec: [spec-name]
Location: .kiro/specs/[spec-name]/
Current status: [Phase X completed / New spec]

Ready to proceed. Type a phase command or describe your requirements.
```

---

## Phase Intent Recognition

**CRITICAL**: Use semantic understanding to recognize user intent, NOT keyword matching.

When user expresses intent to perform a specific phase, load the corresponding steering file.

| Phase | User Intent | Example Expressions |
|-------|-------------|---------------------|
| Phase 1 | Want to **discover/collect** requirements from stakeholders | "帮我做需求发现", "收集用户需求", "I need to gather requirements", "了解用户需要什么" |
| Phase 2 | Want to **prioritize/sort** requirements by value | "给需求排优先级", "哪些需求更重要", "prioritize these requirements", "做价值排序" |
| Phase 3 | Want to **analyze** requirements into stories/use cases | "进行需求分析", "分析这个需求", "analyze the requirements", "写用户故事" |
| Phase 4 | Want to **clarify** ambiguous requirements | "澄清一下需求", "这个需求不清楚", "clarify requirements", "有些地方需要确认" |
| Phase 5 | Want to **validate/review** requirements quality | "验证需求", "检查需求是否完整", "validate requirements", "审查需求质量" |
| Phase 6 | Want to **formalize/specify** requirements into PRD | "生成PRD", "输出需求规格", "create specification", "写需求文档" |

### Intent Recognition Rules

1. **Understand meaning, not keywords**: "进行需求分析" and "analyze the requirements" have the same intent → Phase 3
2. **Context matters**: If user provides raw requirements and asks to "analyze", go to Phase 3 directly
3. **Skip completed phases**: If analysis file exists and user asks to "validate", go to Phase 5
4. **Ask when ambiguous**: If intent is unclear, ask user which phase they want

---

## Steering Files

All detailed methodologies are in the `steering/` directory:

**Core Protocol**:
- `00-interaction-protocol.md` - Interaction guidelines, workflow options, output directory structure

**Phase Instructions**:
- `phase1-requirements-discovery.md` - Discovery methods
- `phase2-requirements-value-sorting.md` - MoSCoW, RICE, value prioritization
- `phase3-requirements-analysis.md` - User stories, use cases, domain modeling
- `phase4-requirements-clarification.md` - Systematic questioning
- `phase5-requirements-validation.md` - Review, acceptance criteria
- `phase6-requirements-specification.md` - PRD, BDD scenarios

**Helper Files**:
- `helper-multi-role-validation.md` - Multi-role validation perspectives
- `helper-diagram-standards.md` - UML diagram and documentation standards

**Output Templates** (prefix: `template-`):
- `template-discovery.md` - Discovery output template
- `template-sort.md` - Value sorting output template
- `template-analysis.md` - Analysis output template
- `template-data-model.md` - Data model output template
- `template-clarification.md` - Clarification output template
- `template-validation.md` - Validation output template
- `template-prd.md` - PRD document template (Phase 6 primary output)

**Deliverable Templates**:
- `template-openapi.md` - OpenAPI specification template
- `template-bdd.md` - BDD/Gherkin scenario template
- `template-rtm.md` - Requirements Traceability Matrix template

---

## File Dependencies (CRITICAL)

**When loading a phase file, you MUST also load its dependencies.**

### Dependency Matrix

| Phase File | Output Template | Helper Files | Deliverable Templates |
|------------|-----------------|--------------|----------------------|
| `phase1-requirements-discovery.md` | `template-discovery.md` | - | - |
| `phase2-requirements-value-sorting.md` | `template-sort.md` | - | - |
| `phase3-requirements-analysis.md` | `template-analysis.md`, `template-data-model.md` | `helper-diagram-standards.md` | - |
| `phase4-requirements-clarification.md` | `template-clarification.md` | - | - |
| `phase5-requirements-validation.md` | `template-validation.md` | `helper-multi-role-validation.md` | - |
| `phase6-requirements-specification.md` | `template-prd.md` | - | `template-openapi.md`, `template-bdd.md`, `template-rtm.md` |

### Loading Rules

1. **When entering a phase**: Load phase file + all its dependencies from the matrix above
2. **Output template**: Defines the structure of the phase output file (e.g., `03-analysis.md`)
3. **Helper files**: Provide standards and guidelines that MUST be followed during execution
4. **Deliverable templates**: Reference templates for creating standalone deliverables (PRD, API spec, BDD)

### Cross-Phase References

| Scenario | Required Files | Action |
|----------|----------------|--------|
| **Iterative Analysis** (Phase 3 after Phase 4/5) | Load `04-clarification.md` and/or `05-validation.md` | Apply clarifications and validation findings |
| **Re-clarification** (Phase 4 after Phase 5) | Load `05-validation.md` | Focus on failed validation dimensions |
| **Re-validation** (Phase 5 after updates) | Load updated `03-analysis.md` | Verify fixes address previous failures |
| **Custom Templates** (Phase 6) | Check `.kiro/templates/` and `~/.kiro/templates/` | Use user templates if available |

### Validation Failure Routing

When validation fails, route to appropriate phase:

| Failed Dimension | Route To | Reason |
|------------------|----------|--------|
| Authenticity | Phase 4 (Clarify) | Need stakeholder confirmation |
| Completeness (missing) | Phase 3 (Analyze) | Need to add requirements |
| Completeness (unclear) | Phase 4 (Clarify) | Need to resolve ambiguities |
| Consistency | Phase 3 (Analyze) | Need to restructure requirements |
| Feasibility | Phase 3 (Analyze) or Phase 4 (Clarify) | Depends on issue type |
| Verifiability | Phase 4 (Clarify) | Need acceptance criteria |

### Output Directory Structure

```
.kiro/specs/[feature-name]/
├── 01-discovery.md      ← Phase 1 output
├── 02-sort.md           ← Phase 2 output
├── 03-analysis.md       ← Phase 3 output
├── data-model.md        ← Phase 3 output (data structure definitions)
├── 04-clarification.md  ← Phase 4 output
├── 05-validation.md     ← Phase 5 output
├── prd.md               ← Phase 6 output (Product Requirements Document)
├── api.yaml             ← Phase 6 deliverable (OpenAPI)
├── rtm.md               ← Phase 6 deliverable (RTM)
└── features/            ← Phase 6 deliverable (BDD)
    └── *.feature
```
