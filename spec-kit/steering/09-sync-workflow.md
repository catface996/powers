---
inclusion: auto
globs: ["**/*.md"]
description: "Sync workflow - synchronize documentation with implementation and generate retrospective report"
keywords: ["sync", "synchronize", "documentation", "retrospective", "deviation", "implementation", "同步", "回顾", "文档"]
---

# Sync Workflow

This workflow synchronizes project documentation with actual implementation after development completion, generating a comprehensive retrospective report.

## Purpose

After a feature implementation is complete, align all documentation to reflect the actual state of the codebase:
- **Non-destructive by default**: Show proposed changes before applying
- **Comprehensive detection**: Scan all relevant documentation files
- **Retrospective analysis**: Compare planned vs actual implementation
- **Knowledge preservation**: Capture lessons learned and deviations

## When to Use

- After completing feature implementation
- After a deployment or release
- When documentation may be out of sync with code
- To generate lessons learned for retrospectives
- Before handoff or team transitions

## Prerequisites

**No strict prerequisites** - this command runs at any time. Missing files will be noted but won't block execution.

**Files scanned if present**:
- `requirements.md` - Feature specification
- `design.md` - Implementation plan
- `tasks.md` - Task list
- `.kiro/steering/product.md` - Product principles
- `.kiro/steering/tech.md` - Technology principles
- `.kiro/steering/structure.md` - Project structure
- `README.md` - Project documentation

## Operating Constraints

**NON-DESTRUCTIVE BY DEFAULT**: Show proposed changes before applying; require user confirmation for modifications.

**Update Modes**:
- **Interactive** (default): Ask for confirmation before each change
- **Preview Only**: Show all proposed changes without applying
- **Report Only**: Only generate sync report, don't propose updates

## Execution Flow

### Step 1: Initialize Sync Context

Identify the feature directory and gather paths:
- Feature specification directory (`.kiro/specs/[###-feature-name]/`)
- Steering files location (`.kiro/steering/`)
- README and other project docs

**File Existence Check**:
For each missing file:
- Log it in the sync report under "Missing Artifacts"
- Skip related analysis steps
- Continue with available files

### Step 2: Scan Implementation State

Analyze the actual codebase to understand what was implemented:

**Code Analysis**:
- Scan source directories for implemented features, components, and modules
- Identify public APIs, endpoints, and interfaces
- Detect technology stack actually used (frameworks, libraries, versions)
- Map file structure and architecture patterns

**Git Analysis (if available)**:
- Review recent commits related to the feature
- Identify files changed since feature branch creation
- Note any hotfixes or post-implementation changes

### Step 3: Compare Plan vs Reality

Create a deviation analysis by comparing:

| Aspect | Planned (from docs) | Actual (from code) | Status |
|--------|--------------------|--------------------|--------|
| Architecture | From design.md | Detected patterns | MATCH / DEVIATION |
| Tech Stack | From design.md | Package files, imports | MATCH / DEVIATION |
| API Endpoints | From requirements.md/contracts | Actual routes/handlers | MATCH / DEVIATION |
| Data Models | From requirements.md/data-model.md | Actual schemas/entities | MATCH / DEVIATION |
| Features | From requirements.md user stories | Implemented functionality | MATCH / DEVIATION / PARTIAL |

**Deviation Categories**:
- **MATCH**: Implementation matches documentation
- **DEVIATION**: Implementation differs from documentation
- **PARTIAL**: Partially implemented or modified scope
- **ADDED**: Implemented but not in original spec (scope creep or enhancement)
- **REMOVED**: In spec but not implemented (descoped)

### Step 4: Detect Documentation Requiring Updates

Scan each documentation file and identify sections needing updates:

#### A. requirements.md Updates
- Features that were descoped or modified
- New features added during implementation
- Updated acceptance criteria based on actual behavior
- Edge cases discovered during development

#### B. design.md Updates
- Architecture changes from original design
- Technology substitutions or version changes
- Modified file structure
- Updated dependency list

#### C. Steering Files Updates
- New architectural principles established
- Modified coding standards based on learnings
- Updated quality gates or review processes

#### D. README.md Updates
- Installation/setup changes
- Updated usage examples
- New configuration options
- Changed prerequisites

### Step 5: Generate Sync Report

Create a comprehensive sync report at `[FEATURE_DIR]/sync-report.md`:

```markdown
# Sync Report: [FEATURE_NAME]

**Generated**: [TIMESTAMP]
**Feature Directory**: [FEATURE_DIR]
**Implementation Status**: [COMPLETED/PARTIAL]

## Executive Summary

[Brief 2-3 sentence summary of sync findings]

## Deviation Analysis

### Matched Items
| Item | Document | Status |
|------|----------|--------|

### Deviations
| Item | Planned | Actual | Impact | Recommendation |
|------|---------|--------|--------|----------------|

### Scope Changes
- **Added**: [Features added beyond original spec]
- **Removed**: [Features descoped]
- **Modified**: [Features with changed behavior]

## Documentation Updates Required

| File | Section | Change Type | Priority |
|------|---------|-------------|----------|

## Lessons Learned

### What Went Well
- [Positive observations]

### Challenges Encountered
- [Deviations that required workarounds]

### Recommendations for Future
- [Suggestions based on deviations and challenges]

## Technical Debt Identified

| Item | Description | Priority | Suggested Resolution |
|------|-------------|----------|---------------------|

## Next Actions

- [ ] [Action items based on findings]
```

### Step 6: Display Terminal Summary

Output a concise summary:

```text
Sync Analysis Complete
======================

Feature: [FEATURE_NAME]
Status: [X] deviations found, [Y] docs need updates

Deviations:
  - HIGH: [count]
  - MEDIUM: [count]
  - LOW: [count]

Documentation Updates:
  - design.md: [sections needing update]
  - requirements.md: [sections needing update]
  - README.md: [sections needing update]

Full report: [FEATURE_DIR]/sync-report.md
```

### Step 7: Propose Documentation Updates

For each file requiring updates, show the proposed changes:

```text
Proposed Updates for design.md:
-------------------------------
Section: ## Architecture
Change: Update to reflect actual implementation pattern

[Show diff or before/after preview]

Apply this change? (yes/no/skip)
```

### Step 8: Apply Updates (with confirmation)

After user approval:
1. Create backup of original files (optional)
2. Apply approved modifications
3. Verify changes were applied correctly
4. Update sync-report.md with applied changes log

### Step 9: Final Summary

Output completion status:

```text
Sync Complete
=============

Documents Updated:
  [x] design.md - Architecture section
  [x] requirements.md - User stories
  [ ] README.md - Skipped by user

Sync Report: [FEATURE_DIR]/sync-report.md

Suggested commit message:
  docs: sync documentation with [feature-name] implementation

  - Updated architecture in design.md
  - Added new user stories to requirements.md
  - Generated sync report with lessons learned
```

## Operating Principles

### Documentation Accuracy
- **Reflect reality**: Ensure all docs match the current implementation state
- **Preserve history**: Don't delete original intent; document what changed and why
- **Actionable updates**: Each proposed change should be specific and immediately applicable

### Knowledge Preservation
- **Capture decisions**: Record architectural decisions made during implementation
- **Document deviations**: Explain why implementation differs from plan
- **Lessons learned**: Extract reusable insights for future projects

### Analysis Guidelines
- **NEVER auto-apply changes** without user confirmation
- **NEVER hallucinate implementation details** (only report what's actually in the code)
- **Prioritize high-impact deviations** (architecture > API > minor details)
- **Report zero issues gracefully** (emit success report with alignment statistics)

## Severity Reference

**HIGH** (significant deviation):
- Architecture pattern differs from design
- Major API changes from specification
- Core features modified or removed

**MEDIUM** (notable change):
- Technology version changes
- Additional features beyond spec
- File structure reorganization

**LOW** (minor adjustment):
- Configuration differences
- Documentation formatting
- Non-functional improvements

## Output

After completing this workflow:
- `sync-report.md` generated in feature directory
- Proposed documentation updates displayed
- Changes applied only with user confirmation

## Next Steps

Suggest to the user:
```
Sync complete.

Next, you can:
1. Review the sync report for lessons learned
2. Commit documentation updates
3. Share findings in team retrospective
4. Archive the feature spec for reference
```
