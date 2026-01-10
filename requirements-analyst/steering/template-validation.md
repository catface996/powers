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

### Authenticity Score: [X]% - [Status]

### Score Calculation

- Total requirements evaluated: [N]
- Requirements with verified origin: [N]
- Requirements with stakeholder confirmation: [N]
- **Formula**: (Verified + Confirmed) / (Total × 2) × 100 = [X]%

### Source Verification (Positive Findings)

| Req ID | Origin | Evidence | Stakeholder Confirmed | Confidence |
|--------|--------|----------|----------------------|------------|
| REQ-001 | User Interview #12 | Interview transcript, 2024-XX-XX | ✅ Yes | High |
| REQ-002 | Support Ticket #456 | Ticket link, 50+ similar reports | ✅ Yes | High |

### Red Flags Identified (Negative Findings)

| Req ID | Red Flag | Impact | Action Required |
|--------|----------|--------|-----------------|
| REQ-003 | No user evidence, assumption-based | May build unwanted feature | Conduct user research |
| REQ-004 | Competitor feature copy | May not fit our users | Validate with target users |

### Authenticity Verdict

> [2-3 sentences explaining why this score is appropriate. Reference specific evidence above. Example: "Score of 85% reflects that 17 of 20 requirements have verified user origins. The 3 unverified requirements (REQ-003, REQ-004, REQ-012) are all P2 priority and can proceed with documented assumptions, but user validation is recommended before v2.0."]

---

## 3. Completeness Validation (完整性)

### Completeness Score: [X]% - [Status]

### Score Calculation

| Category | Total Items | Specified | Weight | Weighted Score | Target | Status |
|----------|-------------|-----------|--------|----------------|--------|--------|
| Functional | [N] | [N] | 30% | [%] | ≥95% | ✅/❌ |
| Data | [N] | [N] | 20% | [%] | ≥95% | ✅/❌ |
| Flows | [N] | [N] | 20% | [%] | ≥90% | ✅/❌ |
| States | [N] | [N] | 10% | [%] | ≥90% | ✅/❌ |
| Errors | [N] | [N] | 10% | [%] | ≥85% | ✅/❌ |
| NFRs | [N] | [N] | 10% | [%] | ≥90% | ✅/❌ |
| **Total** | | | 100% | **[X]%** | | |

### Complete Areas (Positive Findings)

- **Functional**: All [N] user stories have acceptance criteria, CRUD operations fully specified
- **Data**: All [N] entities have complete attribute definitions with types and constraints
- **Flows**: Main success scenarios and [N] alternative flows documented with clear triggers

### Gaps Identified (Negative Findings)

| Gap ID | Category | Missing Item | Impact | Severity | Action |
|--------|----------|--------------|--------|----------|--------|
| GAP-001 | Error | Error handling for API timeout | Users see blank screen | Major | Define timeout handling flow |
| GAP-002 | State | State transition "Pending" → "Cancelled" | Orphan records possible | Medium | Add state machine documentation |
| GAP-003 | NFR | Specific latency target for search | Cannot verify performance | Medium | Define: "Search results < 500ms" |

### Completeness Verdict

> [2-3 sentences explaining the score, highlighting critical gaps. Example: "Score of 91% indicates strong functional coverage but gaps in error handling (GAP-001) and NFR quantification (GAP-003). The error handling gap is Major severity as it affects user experience directly. Recommend addressing GAP-001 before development begins."]

---

## 4. Consistency Validation (一致性)

### Consistency Score: [X]% - [Status]

### Score Calculation

- Total consistency checks performed: [N]
- Checks passed: [N]
- Conflicts detected: [N]
- Conflicts resolved: [N]
- **Formula**: (Checks Passed + Resolved) / Total Checks × 100 = [X]%

### Consistent Areas (Positive Findings)

| Area | Items Checked | Status | Notes |
|------|---------------|--------|-------|
| Terminology | [N] terms | ✅ Consistent | Glossary maintained, no synonyms |
| Data Types | [N] fields | ✅ Consistent | All fields have matching types |
| Business Rules | [N] rules | ✅ Consistent | No contradictory rules found |

### Terminology Check

| Term | Definition | Used Consistently | Issues |
|------|------------|-------------------|--------|
| [Term 1] | [Definition] | ✅ Yes | None |
| [Term 2] | [Definition] | ⚠️ Partial | [Issue] |

### Conflicts Detected (Negative Findings)

| Conflict ID | Type | Req A | Req B | Description | Resolution Status |
|-------------|------|-------|-------|-------------|-------------------|
| CON-001 | Logic | REQ-001 | REQ-005 | REQ-001: "auto-approve < $100", REQ-005: "all orders need approval" | ✅ Resolved: REQ-005 updated |
| CON-002 | Terminology | REQ-002 | REQ-008 | "Customer" vs "Client" used interchangeably | ✅ Resolved: Standardized |
| CON-003 | Data | REQ-003 | REQ-010 | Email max length: 100 vs 255 chars | ⚠️ Pending |

### Consistency Verdict

> [2-3 sentences explaining the score. Example: "Score of 95% reflects 19 of 20 consistency checks passed. One data type conflict (CON-003) remains unresolved but is low risk as it only affects validation messages. The terminology conflict (CON-002) was critical and has been resolved by standardizing on 'Customer' throughout all documents."]

---

## 5. Feasibility Validation (可行性)

### Overall Feasibility Score: [Rating] - [Status]

### Score Calculation (Composite Rating)

| Sub-Dimension | Rating | Weight | Weighted Score | Key Factor |
|---------------|--------|--------|----------------|------------|
| Technical | High/Med/Low | 30% | [Score] | [Key factor] |
| Economic | Viable/Marginal/Not | 25% | [Score] | ROI: [X]% |
| Operational | High/Med/Low | 20% | [Score] | [Key factor] |
| Schedule | Achievable/Risk/Not | 15% | [Score] | Gap: [N] days |
| Compliance | Compliant/Gap/Non | 10% | [Score] | [Key factor] |
| **Overall** | | 100% | **[Rating]** | |

---

### 5.1 Technical Feasibility - [Rating]

| Area | Rating | Evidence |
|------|--------|----------|
| Technology Maturity | High/Medium/Low | [Specific evidence: e.g., "React 18 - widely adopted, team has 2 years experience"] |
| Team Capability | High/Medium/Low | [e.g., "Need 1 additional ML engineer for recommendation feature"] |
| Architecture Fit | High/Medium/Low | [e.g., "Microservices pattern aligns with existing architecture"] |
| Integration Complexity | High/Medium/Low | [e.g., "Payment gateway API has known rate limiting issues"] |

**Technical Verdict**: ✅ Feasible / ⚠️ Risks / ❌ Not Feasible

**Justification**: [Why this rating? e.g., "Rated High because core technologies are proven and team is experienced. Integration risk is mitigated by existing API wrapper library."]

---

### 5.2 Economic Feasibility - [Rating]

| Metric | Value | Benchmark | Assessment |
|--------|-------|-----------|------------|
| Development Cost | [Amount] | Budget: [Amount] | ✅/⚠️/❌ [Within/Over] budget |
| Annual Operational Cost | [Amount] | Industry avg: [Amount] | ✅/⚠️/❌ [Below/Above] average |
| Expected Annual Benefit | [Amount] | Required: [Amount] | ✅/⚠️/❌ [Exceeds/Meets/Below] threshold |
| **3-Year ROI** | **[%]** | Threshold: [%] | ✅/⚠️/❌ |
| **Payback Period** | **[Months]** | Threshold: [Months] | ✅/⚠️/❌ |

**Economic Verdict**: ✅ Viable / ⚠️ Marginal / ❌ Not Viable

**Justification**: [Why this rating? e.g., "ROI of 450% exceeds 100% threshold. Payback of 8 months is well within 18-month target. Development cost is 25% under budget."]

---

### 5.3 Operational Feasibility - [Rating]

| Area | Assessment | Risk | Evidence |
|------|------------|------|----------|
| Process Impact | [Description] | High/Medium/Low | [e.g., "Replaces manual approval workflow"] |
| Training Required | [Hours/Cost] | High/Medium/Low | [e.g., "16 hours per support staff, $5000 total"] |
| Change Management | [Complexity] | High/Medium/Low | [e.g., "Phased rollout over 3 departments"] |

**Operational Verdict**: ✅ Feasible / ⚠️ Risks / ❌ Not Feasible

**Justification**: [Why this rating? e.g., "Rated Medium due to training needs. Support team can scale, but 2-week onboarding period required."]

---

### 5.4 Schedule Feasibility - [Rating]

| Milestone | Required | Achievable | Gap | Risk | Mitigation |
|-----------|----------|------------|-----|------|------------|
| Design | [Date] | [Date] | [Days] | High/Medium/Low | [Mitigation if gap exists] |
| Development | [Date] | [Date] | [Days] | High/Medium/Low | [Mitigation if gap exists] |
| Release | [Date] | [Date] | [Days] | High/Medium/Low | [Mitigation if gap exists] |

**Schedule Verdict**: ✅ Achievable / ⚠️ At Risk / ❌ Not Achievable

**Justification**: [Why this rating? e.g., "2-week buffer exists before hard deadline. Parallel workstreams reduce critical path risk."]

---

### 5.5 Compliance Feasibility - [Rating]

| Regulation | Status | Gap | Impact | Action |
|------------|--------|-----|--------|--------|
| GDPR | Compliant/Gap | [Description] | [Impact if non-compliant] | [Action] |
| WCAG 2.1 | Compliant/Gap | [Description] | [Impact if non-compliant] | [Action] |
| [Industry Specific] | Compliant/Gap | [Description] | [Impact if non-compliant] | [Action] |

**Compliance Verdict**: ✅ Compliant / ⚠️ Gaps Exist / ❌ Non-compliant

**Justification**: [Why this rating? e.g., "GDPR compliant with existing data handling. Accessibility audit required before launch - scheduled for Week 6."]

---

### Feasibility Verdict

> [3-4 sentences summarizing overall feasibility. Example: "Overall feasibility rated HIGH based on strong technical foundation (mature stack, experienced team) and excellent economic outlook (450% ROI, 8-month payback). Schedule risk is mitigated by 2-week buffer. One compliance gap (accessibility audit) is non-blocking but must be addressed before public launch. No blocking issues identified."]

---

## 6. Verifiability Validation (可验证性)

### Verifiability Score: [X]% - [Status]

### Score Calculation

| Category | Total | Verifiable | Weight | Weighted Score |
|----------|-------|------------|--------|----------------|
| Quantified targets | [N] | [N] | 30% | [%] |
| Test cases designed | [N] | [N] | 30% | [%] |
| GWT criteria written | [N] | [N] | 25% | [%] |
| Verification method assigned | [N] | [N] | 15% | [%] |
| **Total** | | | 100% | **[X]%** |

---

### Verifiable Requirements (Positive Findings)

| Req ID | Verification Method | Test Cases | GWT Scenarios | Status | Why Verifiable |
|--------|---------------------|------------|---------------|--------|----------------|
| REQ-001 | Automated Test | TC-001~003 | 3 scenarios | ✅ Complete | Quantified: "Response < 2s" |
| REQ-002 | Performance Test | PT-001 | 2 scenarios | ✅ Complete | Measurable: "99.9% uptime" |
| REQ-003 | Manual Demo | Demo-001 | 1 scenario | ✅ Complete | Observable: "Button turns green" |

### Non-Verifiable Requirements (Negative Findings)

| Req ID | Issue | Why Not Verifiable | Impact | Recommendation |
|--------|-------|-------------------|--------|----------------|
| REQ-004 | Vague target | "System should be fast" - no metric | Cannot verify performance | Specify: "Response < 2s for 95th percentile" |
| REQ-005 | No test design | Complex integration scenario | Cannot prove completion | Design integration test with mock services |
| REQ-006 | Subjective criteria | "User-friendly interface" | Different interpretations | Define: "Task completion rate > 90%" |

---

### GWT Coverage Matrix

| Req ID | Happy Path | Error Scenarios | Edge Cases | Status |
|--------|------------|-----------------|------------|--------|
| REQ-001 | ✅ | ✅ (3) | ✅ (2) | ✅ Complete |
| REQ-002 | ✅ | ✅ (2) | ❌ Missing | ⚠️ Incomplete |
| REQ-003 | ✅ | ❌ Missing | ❌ Missing | ⚠️ Incomplete |

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

### Verifiability Verdict

> [2-3 sentences explaining the score. Example: "Score of 88% reflects strong test coverage for P0 requirements but 3 requirements (REQ-004, REQ-005, REQ-006) need refinement. REQ-004's vague performance target is critical - must be quantified before development. REQ-005 and REQ-006 are P2 and can be refined during implementation planning."]

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
