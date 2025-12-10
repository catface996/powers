---
inclusion: agent
---

# Phase 5: Requirements Validation

**Phase Objective**: Validate requirements authenticity, completeness, and testability.
**Time Allocation**: 10% of total effort
**Your Role**: Professional Requirements Analyst

---

## Quick Reference

| Method | Focus | Output | Mandatory? |
|--------|-------|--------|------------|
| Requirements Review | Formal inspection | Meeting minutes, issues list | ✅ Yes |
| GWT Acceptance Criteria | Testability | Given-When-Then scenarios | ✅ Yes |
| Prototype Testing | User validation | Test results, feedback | ✅ Yes (core functions) |
| Traceability Matrix | Coverage tracking | Complete trace links | ✅ Yes |

---

## Pre-Check (GATE CHECK)

**MUST pass this check before starting**:

- [ ] **Phase 4 completed?** All requirements prioritized with release plan approved?
- [ ] **Inputs available?** Priority list and release plan from Phase 4 ready?
- [ ] **Stakeholders available?** Real users and reviewers identified and available?

**If ANY check fails**: STOP. NEVER proceed. Return to Phase 4.

---

## Your Tasks (NON-NEGOTIABLE)

1. **Requirements Review**: Organize formal requirements review meetings
2. **GWT Acceptance Criteria**: Write acceptance criteria in Given-When-Then format for ALL requirements
3. **Prototype Testing**: Design and test prototypes for core functions
4. **Traceability Matrix**: Establish complete requirements traceability

## What You MUST NEVER Do

- ❌ NEVER skip user participation - real users MUST be involved
- ❌ NEVER ignore prototype testing - it is mandatory for core functions
- ❌ NEVER omit traceability relationships - complete coverage required
- ❌ NEVER mark validation complete if critical issues remain unresolved

---

## Method 1: Requirements Review Meeting

### Review Team

| Role | Responsibility | Required? |
|------|---------------|-----------|
| **Requirements Analyst** | Facilitate, present requirements | ✅ Yes |
| **Product Owner** | Validate business value | ✅ Yes |
| **Technical Lead** | Assess feasibility | ✅ Yes |
| **User Representative** | Validate user needs | ✅ Yes |
| **Test Lead** | Verify testability | ✅ Yes |

### Review Checklist

```markdown
## Requirements Review Checklist

### 1. Completeness
- [ ] All functional requirements defined
- [ ] All non-functional requirements clarified
- [ ] All constraints listed
- [ ] All user roles covered
- [ ] All states and transitions defined
- [ ] All error scenarios addressed

### 2. Consistency
- [ ] No conflicts between requirements
- [ ] Terminology used consistently
- [ ] Data definitions consistent
- [ ] Priorities are logical and justified
- [ ] No duplicate requirements

### 3. Correctness
- [ ] Requirements match stakeholder needs
- [ ] Business rules accurately captured
- [ ] Domain terms correctly used
- [ ] Regulatory requirements correctly stated

### 4. Feasibility
- [ ] Technically feasible
- [ ] Within resource constraints
- [ ] Timeline achievable
- [ ] Dependencies manageable

### 5. Testability
- [ ] Clear acceptance criteria exist
- [ ] Criteria are quantitatively verifiable
- [ ] Edge cases identified
- [ ] Error conditions specified
```

### Review Meeting Template

```markdown
## Requirements Review Meeting Minutes

**Date**: [Date]
**Duration**: [Time]
**Attendees**: [Names and Roles]

### Requirements Reviewed
| Req ID | Requirement | Status |
|--------|-------------|--------|
| REQ-001 | [Title] | ✅ Approved / ⚠️ Minor Issues / ❌ Major Issues |
| REQ-002 | [Title] | ✅ Approved / ⚠️ Minor Issues / ❌ Major Issues |

### Issues Found
| Issue ID | Req ID | Issue Description | Severity | Owner | Due Date |
|----------|--------|-------------------|----------|-------|----------|
| ISS-001 | REQ-001 | [Description] | Critical/Major/Minor | [Name] | [Date] |

### Decisions Made
1. [Decision and rationale]
2. [Decision and rationale]

### Action Items
| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| [Action] | [Name] | [Date] | Open |

### Next Steps
- [ ] Resolve critical issues before proceeding
- [ ] Schedule follow-up review if needed
```

---

## Method 2: Given-When-Then Acceptance Criteria

### GWT Format

```gherkin
Given [precondition/context]
When [action/trigger]
Then [expected outcome]
And [additional outcome]
```

### GWT Writing Guidelines

| Element | Description | Tips |
|---------|-------------|------|
| **Given** | Setup/precondition | Describe initial state clearly |
| **When** | Action/trigger | Single action per scenario |
| **Then** | Expected result | Observable, measurable outcome |
| **And** | Additional conditions | Use sparingly, keep focused |

### GWT Examples

```gherkin
## Requirement: User Login

### AC-1: Successful Login
Given the user is registered with email "user@example.com"
And the account is not locked
When the user enters email "user@example.com" and correct password
Then the system authenticates the user successfully
And redirects to the dashboard
And displays "Welcome back, [username]"

### AC-2: Invalid Password
Given the user is registered with email "user@example.com"
When the user enters email "user@example.com" and incorrect password
Then the system displays "Invalid email or password"
And the user remains on the login page
And the password field is cleared

### AC-3: Account Lockout
Given the user has entered incorrect password 4 times
When the user enters incorrect password the 5th time
Then the system locks the account for 15 minutes
And displays "Account locked. Try again in 15 minutes."
And sends a security alert email to the user

### AC-4: Locked Account Login Attempt
Given the user account is locked
When the user attempts to login with correct credentials
Then the system displays "Account locked. Try again in [remaining time] minutes."
And does not authenticate the user
```

### GWT Coverage Requirements

Every requirement MUST have:
- [ ] **Happy path** scenario (main success flow)
- [ ] **Error scenarios** (at least 2-3 per requirement)
- [ ] **Edge cases** (boundary conditions)
- [ ] **Permission scenarios** (if applicable)

---

## Method 3: Prototype Testing

### Prototype Types

| Type | Fidelity | When to Use | Tools |
|------|----------|-------------|-------|
| **Paper Prototype** | Low | Early concept validation | Paper, whiteboard |
| **Wireframe** | Low-Medium | Information architecture | Figma, Sketch |
| **Clickable Prototype** | Medium | User flow validation | Figma, InVision |
| **High-Fidelity** | High | Detailed usability testing | Figma, code |

### User Testing Plan

```markdown
## User Testing Plan

### Test Information
- **Prototype**: [Name/Link]
- **Fidelity Level**: [Low/Medium/High]
- **Test Objectives**: [What to validate]

### Participants
| # | User Type | Recruitment Criteria |
|---|-----------|---------------------|
| 1 | [Persona A] | [Criteria] |
| 2 | [Persona B] | [Criteria] |

**Target**: 5-8 participants per user type

### Test Scenarios
| Scenario | Task | Success Criteria | Metrics |
|----------|------|------------------|---------|
| S1 | [Task description] | [What defines success] | Time, completion, errors |
| S2 | [Task description] | [What defines success] | Time, completion, errors |

### Test Script
1. **Introduction** (5 min): Explain purpose, get consent
2. **Warm-up** (5 min): Background questions
3. **Tasks** (20-30 min): Execute test scenarios
4. **Debrief** (10 min): Post-task questions, overall feedback

### Success Criteria
- Task completion rate: ≥80%
- User satisfaction: ≥4/5
- Critical usability issues: 0
- Time on task: Within expected range
```

### Test Results Template

```markdown
## User Testing Results

### Summary
| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Completion Rate | ≥80% | XX% | ✅/❌ |
| Satisfaction | ≥4/5 | X.X | ✅/❌ |
| Critical Issues | 0 | X | ✅/❌ |

### Task Results
| Task | Completion Rate | Avg Time | Issues Found |
|------|-----------------|----------|--------------|
| T1 | XX% | X min | [List] |
| T2 | XX% | X min | [List] |

### Issues Identified
| Issue ID | Severity | Description | Recommendation |
|----------|----------|-------------|----------------|
| USR-001 | Critical | [Description] | [Fix] |
| USR-002 | Major | [Description] | [Fix] |
| USR-003 | Minor | [Description] | [Fix] |

### User Quotes
> "[Direct quote from user]" - Participant #X

### Recommendations
1. [Priority recommendation]
2. [Secondary recommendation]
```

---

## Method 4: Requirements Traceability Matrix

### Traceability Links

```
Business Req → User Story → Design Doc → Test Case → Code Module
    BR-001   →   US-001   →   DD-001   →  TC-001   →  UserService
```

### Traceability Matrix Template

```markdown
## Requirements Traceability Matrix

| Req ID | Business Req | User Story | Design Doc | Test Cases | Code Module | Status |
|--------|--------------|------------|------------|------------|-------------|--------|
| REQ-001 | BR-001 | US-001 | DD-001 | TC-001~005 | UserService | ✅ |
| REQ-002 | BR-001 | US-002 | DD-002 | TC-006~010 | AuthService | ✅ |
| REQ-003 | BR-002 | US-003 | DD-003 | TC-011~015 | PaymentService | ⚠️ |

### Coverage Summary
- Total Requirements: XX
- Fully Traced: XX (XX%)
- Partially Traced: XX (XX%)
- Not Traced: XX (XX%)

### Gaps Identified
| Req ID | Missing Link | Action Required |
|--------|--------------|-----------------|
| REQ-003 | Test Cases | Write test cases |
| REQ-005 | Design Doc | Complete design |
```

---

## Validation Report

```markdown
## Requirements Validation Report

**Project Name**: [Name]
**Validation Date**: [Date]
**Validation Team**: [Names]

### Executive Summary
[1-2 paragraph summary of validation results]

### Validation Activities
| Activity | Date | Participants | Result |
|----------|------|--------------|--------|
| Requirements Review | [Date] | [Names] | [Result] |
| Prototype Testing | [Date] | [Names] | [Result] |

### Validation Summary
| Category | Total | Validated | Passed | Failed | Pending |
|----------|-------|-----------|--------|--------|---------|
| Functional | XX | XX | XX | XX | XX |
| Non-Functional | XX | XX | XX | XX | XX |
| **Total** | **XX** | **XX** | **XX** | **XX** | **XX** |

### Key Findings
1. **Positive**: [What validated well]
2. **Concerns**: [Issues discovered]
3. **Risks**: [Potential problems]

### Outstanding Issues
| Issue ID | Severity | Description | Owner | Due Date |
|----------|----------|-------------|-------|----------|
| VAL-001 | Critical | [Description] | [Name] | [Date] |
| VAL-002 | Major | [Description] | [Name] | [Date] |

### Recommendations
1. [Prioritized recommendation]
2. [Secondary recommendation]

### Sign-Off
| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Owner | | | |
| Technical Lead | | | |
| Test Lead | | | |
```

---

## Exit Criteria (NON-NEGOTIABLE)

| Criteria | Standard | Verification | Status |
|----------|----------|--------------|--------|
| Requirements Review | Formal review completed | Minutes documented | [ ] |
| GWT Acceptance Criteria | All requirements have testable criteria | Each req has ≥1 GWT | [ ] |
| Prototype Testing | Core functions validated | ≥80% success rate | [ ] |
| Traceability Matrix | Complete traceability | All reqs traced | [ ] |
| Validation Report | Findings documented | No critical issues unresolved | [ ] |

**CRITICAL**: NEVER mark validation complete if critical issues remain unresolved.

---

## Next Step

After completing this phase, proceed to:

**Phase 6: Specification**
- PRD document writing
- API specification
- BDD scenarios
- Requirements baseline establishment
