---
inclusion: auto
globs: ["**/*.md", "**/*.json", "**/*.yaml", "**/*.yml", "**/*.toml"]
description: "Discover workflow - reverse engineer existing projects to generate steering files and product specification"
keywords: ["discover", "reverse", "bootstrap", "analyze", "existing", "project", "逆向", "发现", "分析", "现有项目"]
---

# Discover Workflow

This workflow analyzes existing projects to reverse-engineer steering files (product.md, tech.md, structure.md) and generate a comprehensive product specification document.

## Purpose

Bootstrap SDD methodology for existing projects by:
- **Analyzing codebase**: Understand technology stack, architecture, and patterns
- **Extracting product context**: Identify purpose, users, and business logic
- **Documenting structure**: Map project layout and conventions
- **Generating specification**: Create product documentation from code analysis

## When to Use

- Onboarding to an existing project without documentation
- Adopting SDD methodology for legacy codebases
- Creating documentation for undocumented projects
- Understanding unfamiliar codebases quickly
- Preparing for major refactoring or modernization

## Prerequisites

**Required**:
- An existing codebase to analyze
- Access to source files, configuration files, and package manifests

**Helpful but optional**:
- Existing README or documentation
- Git history for context
- Running application for behavior observation

## Operating Constraints

**NON-DESTRUCTIVE**: This workflow only reads and analyzes; it generates new files but does NOT modify existing code.

**USER CONFIRMATION**: All generated files require user review and approval before saving.

**ITERATIVE REFINEMENT**: Generated files are drafts; expect multiple rounds of refinement with user input.

## Execution Flow

### Step 1: Project Discovery

Scan the project to gather initial context:

**File System Analysis**:
- Identify root directory and project boundaries
- Detect monorepo vs single project structure
- Find configuration files (package.json, pyproject.toml, Cargo.toml, etc.)
- Locate source directories and entry points

**Version Control Analysis** (if available):
- Check git history for project age and activity
- Identify main contributors
- Review recent changes for active areas

**Output**: Project overview summary for user confirmation

```markdown
## Project Overview

**Root**: [path]
**Type**: [monorepo/single-project/library/application]
**Primary Language**: [detected language]
**Package Manager**: [npm/pip/cargo/etc.]
**Age**: [first commit date if available]
**Activity**: [last commit, commit frequency]
```

### Step 2: Technology Stack Analysis

Analyze dependencies and configuration to determine the tech stack:

**Dependency Analysis**:
- Parse package manifests (package.json, requirements.txt, Cargo.toml, go.mod, etc.)
- Identify frameworks (React, Django, Spring, etc.)
- Detect testing frameworks
- Find build tools and CI/CD configuration

**Configuration Analysis**:
- Parse config files (tsconfig.json, .eslintrc, pytest.ini, etc.)
- Identify linting and formatting tools
- Detect environment configuration patterns

**Infrastructure Detection**:
- Find Dockerfile, docker-compose.yml
- Detect cloud provider configurations (AWS, GCP, Azure)
- Identify database configurations

**Output**: Technology inventory for tech.md generation

### Step 3: Architecture Analysis

Understand the project's architecture and patterns:

**Directory Structure Analysis**:
- Map folder hierarchy
- Identify architectural patterns (MVC, Clean Architecture, Hexagonal, etc.)
- Detect module boundaries
- Find shared/common code locations

**Code Pattern Detection**:
- Identify naming conventions (files, functions, classes)
- Detect API patterns (REST, GraphQL, gRPC)
- Find data access patterns (ORM, raw SQL, repositories)
- Identify error handling approaches

**Dependency Graph**:
- Map internal module dependencies
- Identify circular dependencies
- Find entry points and core modules

**Output**: Architecture summary for structure.md generation

### Step 4: Product Context Extraction

Understand what the product does and who it serves:

**Documentation Analysis**:
- Parse existing README files
- Extract from code comments and docstrings
- Review API documentation if present
- Check for user guides or wikis

**Code Semantics Analysis**:
- Analyze route handlers/controllers for features
- Identify domain models and their relationships
- Extract business logic from service layers
- Detect user-facing functionality

**Configuration Clues**:
- Environment variables for feature flags
- Localization files for user-facing text
- Permission/role configurations

**Output**: Product context summary for product.md generation

### Step 5: Generate Steering Files

Based on analysis, generate three steering files:

#### A. Generate product.md

```markdown
# Product Steering

## Vision
[Extracted or inferred product purpose]

## Target Users
[Identified from code analysis, auth systems, UI patterns]

## Business Constraints
[Inferred from code patterns, validations, limits]

## Success Metrics
[Suggested based on tracked analytics, logs, or metrics code]

## Non-Functional Requirements
### Performance
[From caching patterns, optimization code]

### Security
[From auth implementation, validation patterns]

### Compliance
[From data handling, audit logs if present]

## Feature Prioritization
[Based on code complexity, test coverage, usage patterns]
```

#### B. Generate tech.md

```markdown
# Technology Steering

## Stack
- **Language**: [detected with version]
- **Framework**: [detected with version]
- **Database**: [detected from config/code]
- **Cache**: [detected or N/A]
- **Testing**: [detected testing framework]
- **CI/CD**: [detected from workflow files]

## Development Principles
[Inferred from code patterns and existing standards]

## Coding Standards
### Naming
[Detected conventions]

### Error Handling
[Detected patterns]

### Logging
[Detected approach]

## Quality Gates
[Based on existing CI/CD, linting, test setup]

## Dependency Rules
[Based on existing dependency management]
```

#### C. Generate structure.md

```markdown
# Structure Steering

## Project Layout
[Actual detected structure with descriptions]

## Naming Conventions
### Files
[Detected pattern]

### Components/Classes
[Detected pattern]

### Functions
[Detected pattern]

### Constants
[Detected pattern]

## Module Organization
[Detected module patterns and rules]

## API Patterns
[Detected from route definitions]

## Database Conventions
[Detected from models/migrations]

## Documentation
[Detected documentation locations and patterns]
```

### Step 6: Generate Product Specification

Create a comprehensive product specification document:

```markdown
# Product Specification: [PROJECT_NAME]

**Generated**: [TIMESTAMP]
**Version**: [detected version or 1.0.0]
**Status**: Draft - Requires Review

---

## Executive Summary

[2-3 paragraph overview of what the product does, who it serves, and its key value proposition]

---

## Product Overview

### Purpose
[Why this product exists]

### Target Audience
[Who uses this product and their needs]

### Key Features
[List of main features with descriptions]

---

## Feature Inventory

| Feature | Description | Location | Status |
|---------|-------------|----------|--------|
| [Feature 1] | [Description] | [Files/Modules] | [Active/Deprecated] |

---

## Architecture Overview

### System Diagram
[Text-based or mermaid diagram of system architecture]

### Component Breakdown
[Description of major components and their responsibilities]

### Data Flow
[How data moves through the system]

---

## Technical Summary

### Technology Stack
[Summary table of technologies used]

### External Dependencies
[Third-party services and APIs]

### Infrastructure Requirements
[Deployment and runtime requirements]

---

## API Reference

### Endpoints
[List of API endpoints with methods and descriptions]

### Data Models
[Key data models and their fields]

---

## Quality & Testing

### Test Coverage
[Detected test types and coverage if measurable]

### Quality Gates
[Existing quality checks]

---

## Deployment & Operations

### Build Process
[Detected build steps]

### Deployment
[Detected deployment approach]

### Monitoring
[Detected monitoring/logging setup]

---

## Known Issues & Technical Debt

[Detected TODO comments, deprecated code, known issues from code analysis]

---

## Recommendations

### Documentation Gaps
[What documentation is missing]

### Suggested Improvements
[Technical improvements based on analysis]

### SDD Adoption Path
[Recommended next steps for adopting SDD methodology]
```

### Step 7: Present Results

Display analysis results and generated files to user:

```text
Project Discovery Complete
==========================

Project: [PROJECT_NAME]
Language: [PRIMARY_LANGUAGE]
Framework: [MAIN_FRAMEWORK]
Type: [APPLICATION_TYPE]

Analysis Summary:
  - Files scanned: [N]
  - Modules detected: [N]
  - Features identified: [N]
  - API endpoints found: [N]

Generated Files:
  1. .kiro/steering/product.md
  2. .kiro/steering/tech.md
  3. .kiro/steering/structure.md
  4. .kiro/specs/000-product-spec/product-spec.md

Would you like to:
  A) Review each file before saving
  B) Save all files and review later
  C) Regenerate specific sections
  D) Ask questions about the analysis
```

### Step 8: Interactive Refinement

Allow user to refine generated content:

**Review Mode**:
- Display each generated file section by section
- Allow user to approve, modify, or regenerate each section
- Incorporate user corrections into final output

**Question Mode**:
- Answer questions about detected patterns
- Explain reasoning for specific conclusions
- Provide evidence from code for each assertion

**Regeneration Mode**:
- Re-analyze specific aspects with user guidance
- Incorporate additional context provided by user
- Update generated files with new information

### Step 9: Save and Summarize

After user approval, save files and provide summary:

```text
Discovery Complete
==================

Files Created:
  [x] .kiro/steering/product.md
  [x] .kiro/steering/tech.md
  [x] .kiro/steering/structure.md
  [x] .kiro/specs/000-product-spec/product-spec.md

Next Steps:
  1. Review generated files and refine as needed
  2. Run **Specify** to document individual features
  3. Use **Plan** to create implementation plans for new work
  4. Consider **Analyze** to validate consistency

Suggested commit message:
  docs: add steering files and product spec from project discovery

  - Generated product.md with vision and constraints
  - Generated tech.md with stack and standards
  - Generated structure.md with layout and conventions
  - Created initial product specification
```

## Analysis Guidelines

### Evidence-Based Conclusions
- **Every assertion must have code evidence**
- Quote specific files and line numbers when possible
- Mark uncertain conclusions with [INFERRED] tag
- Distinguish between detected facts and assumptions

### Handling Ambiguity
- When patterns are inconsistent, document all variations
- Ask user to clarify when multiple interpretations exist
- Default to most common pattern when choosing conventions
- Mark areas needing user input with [NEEDS CLARIFICATION]

### Scope Boundaries
- Focus on primary application code, not vendored/generated code
- Skip node_modules, __pycache__, build artifacts
- Respect .gitignore patterns for exclusion
- Limit analysis depth for very large monorepos

## Output Files

After completing this workflow:
- `.kiro/steering/product.md` - Product vision and constraints
- `.kiro/steering/tech.md` - Technology stack and standards
- `.kiro/steering/structure.md` - Project layout and conventions
- `.kiro/specs/000-product-spec/product-spec.md` - Comprehensive product specification

## Next Steps

Suggest to the user:
```
Discovery complete.

Next, you can:
1. Review and refine the generated steering files
2. Run **Specify** to document specific features in detail
3. Run **Analyze** to check for consistency
4. Share product-spec.md with stakeholders for review
5. Begin new development using the established SDD methodology
```
