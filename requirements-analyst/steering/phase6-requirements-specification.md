---
inclusion: agent
---

# Phase 6: Requirements Specification

**Phase Objective**: Formalize validated requirements into unified documentation, establish requirements baseline.
**Time Allocation**: 10% of total effort
**Your Role**: Professional Requirements Analyst

---

## Quick Reference

| Deliverable | Format | Purpose | Mandatory? |
|-------------|--------|---------|------------|
| PRD Document | Markdown/PDF | Complete product requirements | ✅ Yes |
| API Specification | OpenAPI YAML | API contract definition | If API-heavy |
| BDD Scenarios | Gherkin | Executable test scenarios | ✅ Yes |
| RTM | Markdown | Requirements traceability matrix | ✅ Yes |
| Requirements Baseline | Version controlled | Change management | ✅ Yes |

**Baseline Establishment Process**:
1. Requirements Freeze → 2. Formal Review → 3. Stakeholder Approval → 4. Version Release → 5. Change Control

---

## Output

**Primary Output**: `.kiro/specs/[feature-name]/prd.md` (Product Requirements Document)

**Additional Deliverables**:
- `.kiro/specs/[feature-name]/api.yaml` - OpenAPI specification (if applicable)
- `.kiro/specs/[feature-name]/rtm.md` - Requirements Traceability Matrix
- `.kiro/specs/[feature-name]/features/*.feature` - BDD scenarios

> **Dependencies**: See `POWER.md` → File Dependencies for required template and helper files.

---

## Pre-Check (GATE CHECK)

**MUST satisfy these conditions before starting**:

| Check Item | Requirement | Status |
|-----------|-------------|--------|
| Phase 5 Complete | ALL Phase 5 validation criteria satisfied | [ ] |
| All Requirements Validated | Validated and approved requirements | [ ] |
| Stakeholder Alignment | Consensus on requirements | [ ] |

**If check fails**: STOP. Return to Phase 5 and complete validation.

---

## Custom Template Support (MUST ASK FIRST)

**CRITICAL**: Before generating any specification documents, you MUST ask the user about custom templates.

### Template Inquiry (MANDATORY)

```markdown
---
## Specification Template Selection

Before I generate the specification documents, I need to know your template preferences.

**Do you want to use a custom specification template?**

| Option | Description |
|--------|-------------|
| **A** | **Use Default Templates** - Use the built-in PRD, API, and BDD templates |
| **B** | **Use Custom Template** - Provide your own specification template |
| **C** | **Use Both** - Start with custom template, supplement with default sections |

---
Reply with **A**, **B**, or **C**.

If you choose **B** or **C**, please provide:
- Template file path (e.g., `/path/to/template.md`)
- Or template name if stored in `.kiro/templates/` directory
```

### Custom Template Handling

#### If User Chooses B or C:

1. **Request Template Location**:
```markdown
Please provide the custom template:

**Option 1**: File path
> Example: `/Users/you/templates/prd-template.md`
> Example: `./templates/my-spec-template.md`

**Option 2**: Template name (if in `.kiro/templates/`)
> Example: `company-prd` (will look for `.kiro/templates/company-prd.md`)

**Option 3**: Paste template content directly
> You can paste your template content here if it's short.
```

2. **Validate Template**:
   - Check if file exists
   - Read and parse template structure
   - Identify placeholders (e.g., `[Product Name]`, `{{feature}}`, `$VARIABLE`)
   - Report template structure to user

3. **Apply Custom Template**:
```markdown
### Template Analysis

I've analyzed your custom template. Here's what I found:

| Aspect | Finding |
|--------|---------|
| **Template Path** | [Path] |
| **Sections Found** | [List of sections] |
| **Placeholders** | [List of variables to fill] |
| **Compatible With** | PRD / API / BDD / Other |

**Missing Sections** (compared to standard):
- [Section 1] - Recommend adding for completeness
- [Section 2] - Optional but valuable

Shall I proceed with this template? (Yes/No)
```

### Template Storage Locations

| Priority | Location | Description |
|----------|----------|-------------|
| 1 | User-provided path | Explicit file path from user |
| 2 | `.kiro/templates/` | Project-specific templates |
| 3 | `~/.kiro/templates/` | User-global templates |
| 4 | Built-in templates | Default templates in this document |

### Custom Template Placeholders

Support these placeholder formats:

| Format | Example | Description |
|--------|---------|-------------|
| `[Brackets]` | `[Product Name]` | Simple placeholder |
| `{{Mustache}}` | `{{feature_name}}` | Mustache-style |
| `$VARIABLE` | `$PRODUCT_NAME` | Shell-style |
| `<%=ERB%>` | `<%=product.name%>` | ERB-style |

---

## Your Tasks (NON-NEGOTIABLE)

1. **PRD Document**: Write complete Product Requirements Document
2. **API Specification**: Define API design document (if applicable)
3. **BDD Scenarios**: Write BDD test scenarios in Gherkin format
4. **RTM**: Create Requirements Traceability Matrix linking requirements to design, code, and tests
5. **Requirements Baseline**: Establish formal requirements baseline with version control

## What You MUST NEVER Do

- ❌ NEVER use non-standard formats - MUST follow industry standards
- ❌ NEVER omit version control - MUST establish baseline
- ❌ NEVER ignore change management processes - MUST define change procedures
- ❌ NEVER over-pursue document perfection while ignoring actual value

---

## Method 1: PRD Document

### Purpose

Create a complete Product Requirements Document that serves as the authoritative source for product definition.

### PRD Structure Overview

| Section | Content |
|---------|---------|
| Document Information | Version, owner, status |
| Executive Summary | 2-3 paragraph overview |
| Product Overview | Vision, objectives, target users, scope |
| Functional Requirements | Features, user stories, acceptance criteria, business rules |
| Non-Functional Requirements | Performance, security, reliability, usability |
| User Experience | Flows, wireframes, navigation |
| Technical Specifications | Architecture, integrations, data model |
| Release Plan | MVP, versions, roadmap |
| Dependencies and Risks | Dependencies, risk matrix |
| Appendices | Glossary, references, version history |
| Approvals | Stakeholder sign-off |

### When to Use PRD

- New product development
- Major feature releases
- Stakeholder alignment needed
- Formal documentation required

---

## Method 2: API Specification (OpenAPI)

### Purpose

Define API contracts using OpenAPI 3.0 specification for development and documentation.

### OpenAPI Structure Overview

| Section | Content |
|---------|---------|
| `info` | API name, version, description, contact |
| `servers` | Production and staging URLs |
| `paths` | Endpoints with operations (GET, POST, PUT, DELETE) |
| `components/schemas` | Data models and request/response objects |
| `components/responses` | Reusable response definitions |
| `components/securitySchemes` | Authentication methods |
| `security` | Global security requirements |

### When to Use OpenAPI

- API-first development
- Microservices architecture
- Third-party integrations
- API documentation generation

---

## Method 3: BDD Scenarios (Gherkin)

### Purpose

Write executable test scenarios in Gherkin format for behavior-driven development.

### BDD Structure Overview

| Element | Syntax | Purpose |
|---------|--------|---------|
| Feature | `Feature: [Name]` | Describe the feature being tested |
| Background | `Background:` | Common preconditions for all scenarios |
| Scenario | `Scenario: [Name]` | Single test case |
| Scenario Outline | `Scenario Outline:` | Parameterized test with Examples |
| Given | `Given [context]` | Preconditions |
| When | `When [action]` | Action being tested |
| Then | `Then [outcome]` | Expected result |
| And/But | `And [additional]` | Additional steps |
| Tags | `@tag` | Categorization (e.g., `@happy-path`, `@security`) |

### Recommended Tags

| Tag | Purpose |
|-----|---------|
| `@happy-path` | Main success scenarios |
| `@error-handling` | Error and validation scenarios |
| `@security` | Security-related scenarios |
| `@edge-case` | Boundary and edge cases |
| `@performance` | Performance requirements |
| `@priority-high/medium/low` | Priority classification |

### When to Use BDD

- Test-driven development
- Acceptance testing
- Stakeholder communication
- Living documentation

---

## Method 4: Requirements Traceability Matrix (RTM)

### Purpose

Create a comprehensive traceability matrix that links requirements to design, implementation, and test artifacts throughout the project lifecycle.

### RTM Structure Overview

| Section | Content |
|---------|---------|
| Forward Traceability | Requirements → Design → Code → Tests |
| Backward Traceability | Implementation → Requirements |
| Test Traceability | Test Cases → Requirements Coverage |
| Coverage Summary | Progress metrics and gap analysis |
| Change Impact | Impact analysis for requirement changes |
| Verification Status | Sign-off and approval tracking |

### Key Traceability Links

| Link Type | From | To | Purpose |
|-----------|------|-----|---------|
| **Derives** | Business Req | Functional Req | Decomposition tracking |
| **Implements** | Requirement | Code Location | Implementation tracking |
| **Verifies** | Test Case | Requirement | Test coverage tracking |
| **Depends** | Requirement | Requirement | Dependency management |

### Coverage Metrics

Track these metrics for each requirement:

| Status | Definition |
|--------|------------|
| Designed | Has design reference |
| Implemented | Has code reference |
| Tested | Has test case(s) |
| Verified | Stakeholder approved |

### When to Use RTM

- Complex projects with many requirements
- Regulatory/compliance requirements
- Multi-team development
- Long-term maintenance planning
- Audit and verification needs

---

## Method 5: Requirements Baseline Management

### Version Numbering

**Semantic Versioning**: MAJOR.MINOR.PATCH

| Component | When to Increment | Example |
|-----------|-------------------|---------|
| **MAJOR** | Incompatible changes, major scope changes | 1.0.0 → 2.0.0 |
| **MINOR** | New features, backward compatible | 1.0.0 → 1.1.0 |
| **PATCH** | Bug fixes, clarifications | 1.0.0 → 1.0.1 |

### Baseline Record Template

```markdown
## Requirements Baseline Record

### Baseline Information
| Field | Value |
|-------|-------|
| **Baseline Version** | v1.0.0 |
| **Baseline Date** | [Date] |
| **Approved By** | [Names] |
| **Status** | Active |

### Included Requirements
| Req ID Range | Count | Category |
|--------------|-------|----------|
| REQ-001 ~ REQ-050 | 50 | Functional |
| NFR-001 ~ NFR-015 | 15 | Non-Functional |
| **Total** | **65** | |

### Change Control Process
1. **Change Request**: Submit via [system/form]
2. **Impact Analysis**: Technical and schedule assessment
3. **CCB Review**: Change Control Board approval
4. **Implementation**: Approved changes implemented
5. **Documentation**: Requirements updated, new baseline

### Change Request Template
| Field | Value |
|-------|-------|
| **CR ID** | CR-XXX |
| **Requester** | [Name] |
| **Date** | [Date] |
| **Requirements Affected** | [List] |
| **Change Description** | [Description] |
| **Justification** | [Why needed] |
| **Impact Assessment** | [Schedule, cost, risk] |
| **Decision** | Approved / Rejected / Deferred |
| **Approved By** | [Names] |

### Version History
| Version | Date | Author | Changes | Approved By |
|---------|------|--------|---------|-------------|
| 1.0.0 | [Date] | [Name] | Initial baseline | [Names] |
| 1.0.1 | [Date] | [Name] | [Changes] | [Names] |
| 1.1.0 | [Date] | [Name] | [Changes] | [Names] |
```

---

## Complete Process Deliverables Checklist

After completing all 6 phases, verify:

- [ ] ✅ Stakeholder list and interview records
- [ ] ✅ User personas and journey maps
- [ ] ✅ Requirements value sorting matrix (MoSCoW, RICE)
- [ ] ✅ User story maps and use case diagrams
- [ ] ✅ Priority ranking and release plans
- [ ] ✅ Validation report
- [ ] ✅ PRD document
- [ ] ✅ API specification (if applicable)
- [ ] ✅ BDD scenarios
- [ ] ✅ Requirements Traceability Matrix (RTM)
- [ ] ✅ Requirements baseline with version control

---

## Exit Criteria (NON-NEGOTIABLE)

| Criteria | Standard | Verification | Status |
|----------|----------|--------------|--------|
| PRD Document | Complete and reviewed | Checklist verified | [ ] |
| API Specification | OpenAPI format (if applicable) | Schema validated | [ ] |
| BDD Scenarios | Core features covered | Syntax validated | [ ] |
| RTM | All requirements traced | Coverage > 80% | [ ] |
| Requirements Baseline | Version established | Git tagged | [ ] |
| Version Control | Under management | Repository confirmed | [ ] |
| Stakeholder Sign-off | Formal approval | Signatures obtained | [ ] |

---

## Congratulations!

You have completed all 6 phases of requirements engineering.

**Next Steps**: Proceed to design phase with:
- Approved PRD as input
- BDD scenarios for test-driven development
- API specifications for development contracts
- RTM for ongoing traceability and change impact analysis

**Remember**: Requirements specification is not the end, but the starting point of continuous evolution. Establish good change management mechanisms to ensure requirements documentation always reflects the latest understanding.
