---
inclusion: agent
---

# Validation Output Template

**Output File**: `.kiro/specs/[feature-name]/05-validation.md`

**Standards**: Must validate 5 dimensions from `phase5-requirements-validation.md`

---

## File Template

```markdown
# Validation Report: [Feature Name]

**Feature**: [feature-name]
**Date**: YYYY-MM-DD
**Validator**: [Name]
**Status**: In Progress | Completed

---

## Executive Summary

[2-3 sentences summarizing validation outcome]

**Overall Status**: ✅ Validated / ⚠️ Conditional / ❌ Failed

---

## 1. Validation Dimension Summary

| Dimension | Status | Score | Critical Issues | Notes |
|-----------|--------|-------|-----------------|-------|
| **Authenticity** | ✅/⚠️/❌ | [%] | [Count] | [Brief note] |
| **Completeness** | ✅/⚠️/❌ | [%] | [Count] | [Brief note] |
| **Consistency** | ✅/⚠️/❌ | [%] | [Count] | [Brief note] |
| **Feasibility** | ✅/⚠️/❌ | [Rating] | [Count] | [Brief note] |
| **Verifiability** | ✅/⚠️/❌ | [%] | [Count] | [Brief note] |

---

## 2. Authenticity Validation (真实性)

### Source Verification

| Req ID | Origin | Evidence | Stakeholder Confirmed | Status |
|--------|--------|----------|----------------------|--------|
| REQ-001 | User Interview #12 | Interview transcript | ✅ Yes | ✅ Valid |
| REQ-002 | Support Ticket #456 | Ticket link | ✅ Yes | ✅ Valid |
| REQ-003 | Assumption | None | ❌ No | ❌ Needs validation |

### Red Flags Identified

| Req ID | Red Flag | Action Required |
|--------|----------|-----------------|
| REQ-003 | No user evidence | Conduct user research |

### Authenticity Score: [X]%

---

## 3. Completeness Validation (完整性)

### Coverage Metrics

| Category | Total Items | Specified | Complete (%) | Target | Status |
|----------|-------------|-----------|--------------|--------|--------|
| Functional | [N] | [N] | [%] | ≥95% | ✅/❌ |
| Data | [N] | [N] | [%] | ≥95% | ✅/❌ |
| Flows | [N] | [N] | [%] | ≥90% | ✅/❌ |
| States | [N] | [N] | [%] | ≥90% | ✅/❌ |
| Errors | [N] | [N] | [%] | ≥85% | ✅/❌ |
| NFRs | [N] | [N] | [%] | ≥90% | ✅/❌ |

### Gaps Identified

| Gap ID | Category | Description | Impact | Action |
|--------|----------|-------------|--------|--------|
| GAP-001 | [Category] | [What's missing] | [Impact] | [Action] |

### Completeness Score: [X]%

---

## 4. Consistency Validation (一致性)

### Terminology Check

| Term | Definition | Used Consistently | Issues |
|------|------------|-------------------|--------|
| [Term 1] | [Definition] | ✅ Yes | None |
| [Term 2] | [Definition] | ⚠️ Partial | [Issue] |

### Conflict Detection

| Req A | Req B | Conflict Type | Description | Resolution |
|-------|-------|---------------|-------------|------------|
| REQ-001 | REQ-005 | Logic | [Description] | [How resolved] |

### Consistency Score: [X]%

---

## 5. Feasibility Validation (可行性)

### 5.1 Technical Feasibility

| Area | Rating | Notes |
|------|--------|-------|
| Technology Maturity | High/Medium/Low | [Notes] |
| Team Capability | High/Medium/Low | [Notes] |
| Architecture Fit | High/Medium/Low | [Notes] |
| Integration Complexity | High/Medium/Low | [Notes] |

**Technical Verdict**: ✅ Feasible / ⚠️ Risks / ❌ Not Feasible

### 5.2 Economic Feasibility

| Cost/Benefit | Estimate | Confidence |
|--------------|----------|------------|
| Development Cost | [Amount] | High/Medium/Low |
| Annual Operational Cost | [Amount] | High/Medium/Low |
| Annual Benefit | [Amount] | High/Medium/Low |
| **ROI (3-Year)** | **[%]** | |
| **Payback Period** | **[Months]** | |

**Economic Verdict**: ✅ Viable / ⚠️ Marginal / ❌ Not Viable

### 5.3 Operational Feasibility

| Area | Assessment | Risk |
|------|------------|------|
| Process Impact | [Description] | High/Medium/Low |
| Training Required | [Hours/Cost] | High/Medium/Low |
| Change Management | [Complexity] | High/Medium/Low |

**Operational Verdict**: ✅ Feasible / ⚠️ Risks / ❌ Not Feasible

### 5.4 Schedule Feasibility

| Milestone | Required | Achievable | Gap | Risk |
|-----------|----------|------------|-----|------|
| Design | [Date] | [Date] | [Days] | High/Medium/Low |
| Development | [Date] | [Date] | [Days] | High/Medium/Low |
| Release | [Date] | [Date] | [Days] | High/Medium/Low |

**Schedule Verdict**: ✅ Achievable / ⚠️ At Risk / ❌ Not Achievable

### 5.5 Compliance Feasibility

| Regulation | Status | Gap | Action |
|------------|--------|-----|--------|
| [Regulation] | Compliant/Gap | [Description] | [Action] |

**Overall Feasibility**: ✅ Feasible / ⚠️ Conditional / ❌ Not Feasible

---

## 6. Verifiability Validation (可验证性)

### Verification Method Assignment

| Req ID | Method | Test Cases | GWT Criteria | Status |
|--------|--------|------------|--------------|--------|
| REQ-001 | Test | TC-001~003 | AC-001~003 | ✅ Verifiable |
| REQ-002 | Demo | Demo-001 | AC-004~005 | ✅ Verifiable |
| REQ-003 | Inspection | Review-001 | AC-006 | ⚠️ Needs work |

### GWT Coverage

| Req ID | Happy Path | Error Scenarios | Edge Cases | Status |
|--------|------------|-----------------|------------|--------|
| REQ-001 | ✅ | ✅ (3) | ✅ (2) | ✅ Complete |
| REQ-002 | ✅ | ✅ (2) | ❌ Missing | ⚠️ Incomplete |

### Sample GWT Scenarios

\`\`\`gherkin
## REQ-001: [Requirement Name]

### AC-001: Happy Path
Given [precondition]
When [action]
Then [expected result]
  And [measurable outcome]

### AC-002: Error Handling
Given [precondition]
When [error condition]
Then [error response]
  And [user notification]
\`\`\`

### Verifiability Score: [X]%

---

## 7. Multi-Role Validation

### Role Sign-Off Matrix

| Req ID | PM | RA | SA | SE | TE | Overall |
|--------|----|----|----|----|-----|---------|
| REQ-001 | ✅ | ✅ | ⚠️ | ✅ | ✅ | ⚠️ |
| REQ-002 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**Legend**: ✅ Pass | ⚠️ Issues | ❌ Fail

### Role-Specific Concerns

| Role | Req ID | Concern | Resolution |
|------|--------|---------|------------|
| SA | REQ-001 | Architecture impact | [Resolution] |

---

## 8. Traceability Matrix

| Req ID | Business Goal | User Story | Use Case | Test Case | Status |
|--------|---------------|------------|----------|-----------|--------|
| REQ-001 | BG-001 | US-001 | UC-001 | TC-001~005 | ✅ |
| REQ-002 | BG-001 | US-002 | UC-002 | TC-006~010 | ✅ |

**Traceability Coverage**: [X]% fully traced

---

## 9. Outstanding Issues

| ID | Dimension | Severity | Description | Owner | Due | Status |
|----|-----------|----------|-------------|-------|-----|--------|
| V-001 | Authenticity | Critical | [Desc] | [Name] | [Date] | Open |
| V-002 | Completeness | Major | [Desc] | [Name] | [Date] | Open |
| V-003 | Feasibility | Major | [Desc] | [Name] | [Date] | Resolved |

---

## 10. Sign-Off

| Role | Name | Decision | Date | Comments |
|------|------|----------|------|----------|
| Product Owner | [Name] | Approved/Rejected | [Date] | [Comments] |
| Technical Lead | [Name] | Approved/Conditional/Rejected | [Date] | [Conditions] |
| QA Lead | [Name] | Approved/Rejected | [Date] | [Comments] |

---

## Next Steps Available

**What would you like to do next?**

| Option | Action | When to Choose |
|--------|--------|----------------|
| **A** | **Specify** (Proceed) | All 5 dimensions pass, no critical issues, sign-off obtained |
| **B** | **Validate** (Continue) | Critical/major issues remain, feasibility concerns need resolution |
| **C** | **Clarify** (Return) | New ambiguities discovered, authenticity gaps need stakeholder input |

### Recommendation

[Based on Validation Dimension Summary above, recommend Option A/B/C]

**Reason**: [Explain why this option is recommended based on validation results]

---
**Reply with A, B, or C to proceed.**
```
