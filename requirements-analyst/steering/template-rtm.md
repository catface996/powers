# Requirements Traceability Matrix (RTM) Template

**Purpose**: Track requirements through design, implementation, and testing phases
**Output File**: `.kiro/specs/[feature-name]/rtm.md`

---

## 1. Document Information

| Field | Value |
|-------|-------|
| **Project** | [Project Name] |
| **Version** | v1.0.0 |
| **Last Updated** | [Date] |
| **Owner** | [Name] |
| **Status** | Draft / Under Review / Approved |

---

## 2. Traceability Matrix

### 2.1 Forward Traceability (Requirements → Implementation)

| Req ID | Requirement | Priority | Design Ref | Code Ref | Test Case | Status |
|--------|-------------|----------|------------|----------|-----------|--------|
| REQ-001 | [Brief description] | Must | DES-001 | `src/module/file.ts:L50` | TC-001, TC-002 | Implemented |
| REQ-002 | [Brief description] | Must | DES-002 | `src/auth/login.ts:L120` | TC-003 | In Progress |
| REQ-003 | [Brief description] | Should | DES-003 | - | TC-004 | Not Started |
| NFR-001 | [Brief description] | Must | DES-004 | `src/utils/cache.ts` | TC-005 | Implemented |

### 2.2 Backward Traceability (Implementation → Requirements)

| Component | Code Location | Implements | Test Coverage |
|-----------|---------------|------------|---------------|
| UserService | `src/services/user.ts` | REQ-001, REQ-002 | TC-001~TC-003 |
| AuthModule | `src/auth/` | REQ-004, NFR-002 | TC-010~TC-015 |
| API Gateway | `src/api/gateway.ts` | REQ-005, NFR-001 | TC-020~TC-025 |

### 2.3 Test Traceability

| Test Case ID | Test Name | Requirements Covered | Type | Status |
|--------------|-----------|---------------------|------|--------|
| TC-001 | User registration success | REQ-001 | Functional | Pass |
| TC-002 | User registration validation | REQ-001 | Functional | Pass |
| TC-003 | Login authentication | REQ-002, NFR-002 | Security | Pass |
| TC-004 | Response time under load | NFR-001 | Performance | Pending |

---

## 3. Coverage Summary

### 3.1 Requirements Coverage

| Category | Total | Designed | Implemented | Tested | Verified |
|----------|-------|----------|-------------|--------|----------|
| Functional (REQ) | 25 | 25 (100%) | 20 (80%) | 18 (72%) | 15 (60%) |
| Non-Functional (NFR) | 10 | 10 (100%) | 8 (80%) | 6 (60%) | 5 (50%) |
| **Total** | **35** | **35 (100%)** | **28 (80%)** | **24 (69%)** | **20 (57%)** |

### 3.2 Coverage Visualization

```
Requirements Coverage Progress
============================================================
Design:        [####################] 100% (35/35)
Implementation:[################----]  80% (28/35)
Testing:       [##############------]  69% (24/35)
Verification:  [###########---------]  57% (20/35)
============================================================
```

### 3.3 Gap Analysis

| Gap Type | Count | Requirements | Action Required |
|----------|-------|--------------|-----------------|
| No Design | 0 | - | - |
| No Implementation | 7 | REQ-021~REQ-025, NFR-009, NFR-010 | Sprint 3 planned |
| No Test Cases | 11 | [List] | Test plan update needed |
| Test Failures | 2 | REQ-015, NFR-007 | Bug fix in progress |

---

## 4. Traceability Links

### 4.1 Link Types

| Link Type | From | To | Description |
|-----------|------|-----|-------------|
| **Derives** | Business Req | Functional Req | Business requirement decomposed |
| **Implements** | Requirement | Code | Code implements requirement |
| **Verifies** | Test Case | Requirement | Test verifies requirement |
| **Depends** | Requirement | Requirement | Dependency relationship |

### 4.2 Dependency Chain

| Req ID | Requirement | Depends On | Depended By |
|--------|-------------|------------|-------------|
| REQ-001 | User Registration | - | REQ-002, REQ-003 |
| REQ-002 | Email Verification | REQ-001 | REQ-004 |
| REQ-003 | Profile Setup | REQ-001 | REQ-005 |
| REQ-004 | Account Activation | REQ-002 | REQ-006 |

---

## 5. Change Impact Analysis

### 5.1 Impact Matrix Template

When a requirement changes, use this matrix to assess impact:

| If Changed | Affects Design | Affects Code | Affects Tests | Risk Level |
|------------|---------------|--------------|---------------|------------|
| REQ-001 | DES-001, DES-002 | 5 files | 8 test cases | High |
| REQ-002 | DES-002 | 2 files | 3 test cases | Medium |
| NFR-001 | DES-004 | 3 files | 5 test cases | High |

### 5.2 Change Log

| Date | Req ID | Change Type | Description | Impact | Updated By |
|------|--------|-------------|-------------|--------|------------|
| [Date] | REQ-005 | Modified | Updated acceptance criteria | Low | [Name] |
| [Date] | REQ-012 | Added | New requirement from clarification | Medium | [Name] |
| [Date] | REQ-008 | Deleted | Descoped to v2.0 | Low | [Name] |

---

## 6. Verification Status

### 6.1 Verification Matrix

| Req ID | Requirement | Verification Method | Verified By | Date | Result |
|--------|-------------|--------------------:|-------------|------|--------|
| REQ-001 | User Registration | Test + Demo | QA Team | [Date] | Pass |
| REQ-002 | Email Verification | Test | QA Team | [Date] | Pass |
| NFR-001 | Response < 200ms | Performance Test | DevOps | [Date] | Pass |
| NFR-002 | 99.9% Uptime | Monitoring | SRE | [Date] | Pending |

### 6.2 Sign-off Status

| Stakeholder | Role | Requirements Verified | Sign-off Date | Status |
|-------------|------|----------------------|---------------|--------|
| [Name] | Product Owner | All Functional | [Date] | Approved |
| [Name] | Tech Lead | All Technical | [Date] | Approved |
| [Name] | QA Lead | All Test Coverage | [Date] | Pending |
| [Name] | Security | NFR-002~NFR-005 | [Date] | Approved |

---

## 7. RTM Maintenance

### 7.1 Update Triggers

| Event | Required Action |
|-------|-----------------|
| New requirement added | Add row to forward traceability |
| Requirement modified | Update all linked items, log change |
| Code committed | Update Code Ref column |
| Test case added/updated | Update Test Case column |
| Verification completed | Update status and sign-off |

### 7.2 Review Schedule

| Review Type | Frequency | Participants | Purpose |
|-------------|-----------|--------------|---------|
| Coverage Review | Weekly | Dev + QA | Track implementation progress |
| Gap Analysis | Bi-weekly | PM + Tech Lead | Identify missing coverage |
| Full RTM Review | Per Release | All Stakeholders | Release readiness |

---

## Appendix: Status Definitions

| Status | Definition |
|--------|------------|
| **Not Started** | Work has not begun |
| **In Progress** | Currently being worked on |
| **Implemented** | Code complete, awaiting test |
| **Tested** | Test cases executed |
| **Verified** | Stakeholder verified and approved |
| **Blocked** | Cannot proceed due to dependency |
| **Deferred** | Moved to future release |
