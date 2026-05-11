# Code Generation - Detailed Steps

## Overview
This stage generates code for each unit of work through two integrated parts:
- **Part 1 - Planning**: Create detailed code generation plan with explicit steps
- **Part 2 - Generation**: Execute approved plan to generate code, tests, and artifacts

**Note**: For brownfield projects, "generate" means modify existing files when appropriate, not create duplicates.

## Prerequisites
- Unit Design Generation must be complete for the unit
- NFR Implementation (if executed) must be complete for the unit
- All unit design artifacts must be available
- Unit is ready for code generation

---

# PART 1: PLANNING

## Step 1: Analyze Unit Context
- [ ] Read unit design artifacts from Unit Design Generation
- [ ] Read unit story map to understand assigned stories
- [ ] Identify unit dependencies and interfaces
- [ ] Validate unit is ready for code generation

## Step 2: Create Detailed Unit Code Generation Plan
- [ ] Read workspace root and project type from `aidlc-docs/aidlc-state.md`
- [ ] Determine code location (see Critical Rules for structure patterns)
- [ ] **Brownfield only**: Review reverse engineering code-structure.md for existing files to modify
- [ ] Document exact paths (never aidlc-docs/)
- [ ] **Load test artifacts** (if Test Design stage was executed for this unit):
  - `aidlc-docs/construction/{unit-name}/test-design/test-cases.md` - source of truth for what tests to write
  - `aidlc-docs/construction/{unit-name}/test-design/test-doubles.md` - mock/stub/fake strategy per collaborator
  - `aidlc-docs/construction/{unit-name}/test-design/test-data.md` - fixture and factory plan
  - `aidlc-docs/construction/{unit-name}/test-design/coverage-claim.md` - AC/BR/INV coverage contract
- [ ] **Load test strategy** (if executed):
  - `aidlc-docs/inception/test-strategy/test-strategy.md` - TDD policy, coverage gates, speed budget
  - `aidlc-docs/inception/test-strategy/testability-constraints.md` - architectural constraints to honor
- [ ] **Load common-test-quality.md** and apply its Pre-Write Validation Checklist to every test artifact produced
- [ ] Create explicit steps for unit generation:
  - Project Structure Setup (greenfield only)
  - Business Logic: Test Implementation (from test-cases.md)
  - Business Logic: Production Code (to satisfy tests)
  - Business Logic Summary
  - API Layer: Test Implementation (from test-cases.md)
  - API Layer: Production Code (to satisfy tests)
  - API Layer Summary
  - Repository Layer: Test Implementation (from test-cases.md)
  - Repository Layer: Production Code (to satisfy tests)
  - Repository Layer Summary
  - Contract Tests (if unit participates in cross-service contracts)
  - Database Migration Scripts (if data models exist)
  - Documentation Generation (API docs, README updates)
  - Deployment Artifacts Generation
- [ ] **Step ordering rule**: per TDD policy in test strategy, tests are either written before production code (TDD) or atomically alongside it (test-after). Never after.
- [ ] Number each step sequentially
- [ ] Include story mapping references: each step lists the ACs (AC-nnn) and test cases (TC-nnn) it implements
- [ ] Add checkboxes [ ] for each step

## Step 3: Include Unit Generation Context
- [ ] For this unit, include:
  - Stories implemented by this unit
  - Dependencies on other units/services
  - Expected interfaces and contracts
  - Database entities owned by this unit
  - Service boundaries and responsibilities

## Step 4: Create Unit Plan Document
- [ ] Save complete plan as `aidlc-docs/construction/plans/{unit-name}-code-generation-plan.md`
- [ ] Include step numbering (Step 1, Step 2, etc.)
- [ ] Include unit context and dependencies
- [ ] Include story traceability
- [ ] Ensure plan is executable step-by-step
- [ ] Emphasize that this plan is the single source of truth for Code Generation

## Step 5: Summarize Unit Plan
- [ ] Provide summary of the unit code generation plan to the user
- [ ] Highlight unit generation approach
- [ ] Explain step sequence and story coverage
- [ ] Note total number of steps and estimated scope

## Step 6: Log Approval Prompt
- [ ] Before asking for approval, log the prompt with timestamp in `aidlc-docs/audit.md`
- [ ] Include reference to the complete unit code generation plan
- [ ] Use ISO 8601 timestamp format

## Step 7: Wait for Explicit Approval
- [ ] Do not proceed until the user explicitly approves the unit code generation plan
- [ ] Approval must cover the entire plan and generation sequence
- [ ] If user requests changes, update the plan and repeat approval process

## Step 8: Record Approval Response
- [ ] Log the user's approval response with timestamp in `aidlc-docs/audit.md`
- [ ] Include the exact user response text
- [ ] Mark the approval status clearly

## Step 9: Update Progress
- [ ] Mark Code Planning complete in `aidlc-state.md`
- [ ] Update the "Current Status" section
- [ ] Prepare for transition to Code Generation

---

# PART 2: GENERATION

## Step 10: Load Unit Code Generation Plan
- [ ] Read the complete plan from `aidlc-docs/construction/plans/{unit-name}-code-generation-plan.md`
- [ ] Identify the next uncompleted step (first [ ] checkbox)
- [ ] Load the context for that step (unit, dependencies, stories)

## Step 11: Execute Current Step
- [ ] Verify target directory from plan (never aidlc-docs/)
- [ ] **Brownfield only**: Check if target file exists
- [ ] Generate exactly what the current step describes:
  - **If file exists**: Modify it in-place (never create `ClassName_modified.java`, `ClassName_new.java`, etc.)
  - **If file doesn't exist**: Create new file
- [ ] Write to correct locations:
  - **Application Code**: Workspace root per project structure
  - **Test Code**: Workspace root per project structure (same commit as production code)
  - **Documentation**: `aidlc-docs/construction/{unit-name}/code/` (markdown only)
  - **Build/Config Files**: Workspace root
- [ ] Follow unit story requirements
- [ ] Respect dependencies and interfaces
- [ ] **For any test code generated**, apply the `common-test-quality.md` Pre-Write Validation Checklist. Reject and regenerate if any item fails.
- [ ] **Atomic rule**: a production-code step is not complete until its tests exist, were applicable tests from test-cases.md have been implemented, and tests pass locally. Do not defer tests to "a later step".

## Step 12: Update Progress
- [ ] Mark the completed step as [x] in the unit code generation plan
- [ ] Mark associated unit stories as [x] when their generation is finished
- [ ] Update `aidlc-docs/aidlc-state.md` current status
- [ ] **Brownfield only**: Verify no duplicate files created (e.g., no `ClassName_modified.java` alongside `ClassName.java`)
- [ ] Save all generated artifacts

## Step 13: Continue or Complete Generation
- [ ] If more steps remain, return to Step 10
- [ ] If all steps complete, run the test-case-spec drift check (Step 13a), then proceed to present completion message

## Step 13a: Test-Case-Spec Drift Check (MANDATORY if Test Design was executed)
- [ ] For every test case TC-{unit}-nnn in `test-cases.md`, verify a corresponding implemented test exists in the codebase
- [ ] For every AC, BR, INV, and NFR listed in `coverage-claim.md`, verify at least one implemented test references it (by ID in name or comment)
- [ ] For every double in `test-doubles.md` requiring a contract anchor, verify the CT-nnn / IT-nnn referenced actually exists (contract test, real-integration test, or approved waiver WAV-nnn per `common-waiver.md`)
- [ ] Any drift is a blocker:
  - Missing TC implementations → implement them, or amend `test-cases.md` with deferral rationale (see Amendment Protocol)
  - Orphan tests (in code but not in spec) → MUST amend `test-cases.md` via the Amendment Protocol in `construction-test-design.md`. Silent orphan tests are prohibited.
  - Unanchored doubles → add the anchor test, replace with a real collaborator, or file a WAV waiver

## Step 13b: Test Design Amendment Protocol (IF gaps discovered during Code Generation)

If during Code Generation you discover gaps in `test-cases.md` that require new test cases not covered by the approved Test Design, follow the **Amendment Protocol** in `construction-test-design.md`:

1. Add new TC-{unit}-nnn entries to `test-cases.md` with `Source: amended-during-codegen` and `Amendment Reason`
2. Pause Code Generation
3. Present a compact amendment batch message to the user (list of new TC IDs with reasons)
4. Wait for user approval of the amendment batch
5. On approval: continue; log the approval and amendment IDs in `audit.md`
6. On rejection: either remove the amendments (and associated production code) or return to Test Design for redesign

**Rate limit**: if amendments exceed 10% of the original test case count for this unit, stop amending and return to Test Design. At this workflow position Test Design has full visibility into all design outputs, so systematic shortfall indicates a real Test Design gap (or an unloaded design artifact) — not normal codegen discovery.

**Update downstream**: amendments that close previously-declared gaps in `coverage-claim.md` must update that file to reflect reduced gaps.

## Step 14: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# 💻 Code Generation Complete - [unit-name]
```

     2. **AI Summary** (optional): Provide structured bullet-point summary
        - **Brownfield**: Distinguish modified vs created files (e.g., "• Modified: `src/services/user-service.ts`", "• Created: `src/services/auth-service.ts`")
        - **Greenfield**: List created files with paths (e.g., "• Created: `src/services/user-service.ts`")
        - List tests, documentation, deployment artifacts with paths
        - Keep factual, no workflow instructions
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**  
> Please examine the generated code at:
> - **Application Code**: `[actual-workspace-path]`
> - **Documentation**: `aidlc-docs/construction/[unit-name]/code/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the generated code based on your review  
> ✅ **Continue to Next Stage** - Approve code generation and proceed to **[next-unit/Build & Test]**

---
```

## Step 15: Wait for Explicit Approval
- Do not proceed until the user explicitly approves the generated code
- Approval must be clear and unambiguous
- If user requests changes, update the code and repeat the approval process

## Step 16: Record Approval and Update Progress
- Log approval in audit.md with timestamp
- Record the user's approval response with timestamp
- Mark Code Generation stage as complete for this unit in aidlc-state.md

---

## Critical Rules

### Code Location Rules
- **Application code**: Workspace root only (NEVER aidlc-docs/)
- **Documentation**: aidlc-docs/ only (markdown summaries)
- **Read workspace root** from aidlc-state.md before generating code

**Structure patterns by project type**:
- **Brownfield**: Use existing structure (e.g., `src/main/java/`, `lib/`, `pkg/`)
- **Greenfield single unit**: `src/`, `tests/`, `config/` in workspace root
- **Greenfield multi-unit (microservices)**: `{unit-name}/src/`, `{unit-name}/tests/`
- **Greenfield multi-unit (monolith)**: `src/{unit-name}/`, `tests/{unit-name}/`

### Brownfield File Modification Rules
- Check if file exists before generating
- If exists: Modify in-place (never create copies like `ClassName_modified.java`)
- If doesn't exist: Create new file
- Verify no duplicate files after generation (Step 12)

### Planning Phase Rules
- Create explicit, numbered steps for all generation activities
- Include story traceability in the plan
- Document unit context and dependencies
- Get explicit user approval before generation

### Generation Phase Rules
- **NO HARDCODED LOGIC**: Only execute what's written in the unit plan
- **FOLLOW PLAN EXACTLY**: Do not deviate from the step sequence
- **UPDATE CHECKBOXES**: Mark [x] immediately after completing each step
- **STORY TRACEABILITY**: Mark unit stories [x] when functionality is implemented
- **RESPECT DEPENDENCIES**: Only implement when unit dependencies are satisfied
- **TESTS ARE PRIMARY ARTIFACTS, NOT BYPRODUCTS**: Test code is produced under the same discipline as production code, reviewed to the same standard, and committed together with the production code it covers
- **NO "TESTS LATER"**: A code step is not complete until its tests exist and pass locally
- **SPEC-DRIVEN TESTS**: Tests are implemented from `test-cases.md`, not invented during coding (when Test Design was executed)

## Completion Criteria
- Complete unit code generation plan created and approved
- All steps in unit code generation plan marked [x]
- All unit stories implemented according to plan
- All code and tests generated and **passing locally** (do not defer test execution to Build & Test)
- **Test-case-spec drift check passed** (Step 13a): no missing TC implementations, no orphan tests, no unanchored mocks
- Deployment artifacts generated
- Complete unit ready for build and quality-gate verification
