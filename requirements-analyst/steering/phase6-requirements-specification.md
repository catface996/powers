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
| Requirements Baseline | Version controlled | Change management | ✅ Yes |
| Traceability Matrix | Table | Requirements tracking | ✅ Yes |

**Baseline Establishment Process**:
1. Requirements Freeze → 2. Formal Review → 3. Stakeholder Approval → 4. Version Release → 5. Change Control

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

## Your Tasks (NON-NEGOTIABLE)

1. **PRD Document**: Write complete Product Requirements Document
2. **API Specification**: Define API design document (if applicable)
3. **BDD Scenarios**: Write BDD test scenarios in Gherkin format
4. **Requirements Baseline**: Establish formal requirements baseline with version control

## What You MUST NEVER Do

- ❌ NEVER use non-standard formats - MUST follow industry standards
- ❌ NEVER omit version control - MUST establish baseline
- ❌ NEVER ignore change management processes - MUST define change procedures
- ❌ NEVER over-pursue document perfection while ignoring actual value

---

## Method 1: PRD Document

### PRD Template

```markdown
# Product Requirements Document (PRD)

## Document Information
| Field | Value |
|-------|-------|
| **Product Name** | [Name] |
| **Version** | v1.0.0 |
| **Creation Date** | [Date] |
| **Last Updated** | [Date] |
| **Owner** | [Name] |
| **Status** | Draft / In Review / Approved |

---

## 1. Executive Summary
[2-3 paragraphs summarizing the product, its purpose, and key features]

---

## 2. Product Overview

### 2.1 Product Vision
[What is the long-term vision for this product?]

### 2.2 Product Objectives
| Objective | Success Metric | Target |
|-----------|----------------|--------|
| [Objective 1] | [Metric] | [Target Value] |
| [Objective 2] | [Metric] | [Target Value] |

### 2.3 Target Users
| Persona | Description | Key Needs |
|---------|-------------|-----------|
| [Persona 1] | [Description] | [Needs] |
| [Persona 2] | [Description] | [Needs] |

### 2.4 Scope
#### In Scope
- [Feature/Capability 1]
- [Feature/Capability 2]

#### Out of Scope
- [Excluded item 1]
- [Excluded item 2]

---

## 3. Functional Requirements

### 3.1 Feature: [Feature Name]

#### 3.1.1 Overview
[Description of the feature]

#### 3.1.2 User Stories
| Story ID | User Story | Priority |
|----------|------------|----------|
| US-001 | As a [role], I want [feature] so that [benefit] | P0 |

#### 3.1.3 Acceptance Criteria
**US-001**:
```gherkin
Given [precondition]
When [action]
Then [expected result]
```

#### 3.1.4 Business Rules
| Rule ID | Rule Description |
|---------|------------------|
| BR-001 | [Rule] |

#### 3.1.5 Data Requirements
| Field | Type | Required | Validation | Description |
|-------|------|----------|------------|-------------|
| [field] | [type] | Y/N | [rules] | [description] |

---

## 4. Non-Functional Requirements

### 4.1 Performance Requirements
| Requirement | Metric | Target |
|-------------|--------|--------|
| Response Time | Page load | < 2 seconds |
| Throughput | Concurrent users | 1,000 |
| Capacity | Data records | 1 million |

### 4.2 Security Requirements
- [ ] Authentication: [Method]
- [ ] Authorization: [Method]
- [ ] Data encryption: [Standard]
- [ ] Compliance: [Standards]

### 4.3 Reliability Requirements
| Requirement | Target |
|-------------|--------|
| Availability | 99.9% |
| Recovery Time | < 1 hour |
| Data Backup | Daily |

### 4.4 Usability Requirements
- [ ] Accessibility: [Standard, e.g., WCAG 2.1 AA]
- [ ] Browser Support: [List]
- [ ] Mobile Support: [Y/N, devices]
- [ ] Internationalization: [Languages]

---

## 5. User Experience

### 5.1 User Flows
[Include flow diagrams or descriptions]

### 5.2 Wireframes/Mockups
[Link to design files or embed images]

### 5.3 Navigation Structure
[Site map or navigation hierarchy]

---

## 6. Technical Specifications

### 6.1 System Architecture
[High-level architecture diagram or description]

### 6.2 Integration Requirements
| System | Integration Type | Purpose |
|--------|-----------------|---------|
| [System] | API / Webhook / File | [Purpose] |

### 6.3 Data Model
[Entity relationship diagram or key data structures]

---

## 7. Release Plan

### 7.1 MVP (v1.0)
**Target Date**: [Date]
**Features**:
- [Feature 1]
- [Feature 2]

### 7.2 Version 1.1
**Target Date**: [Date]
**Features**:
- [Feature 3]
- [Feature 4]

### 7.3 Roadmap
[Timeline visualization]

---

## 8. Dependencies and Risks

### 8.1 Dependencies
| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| [Dependency] | Internal/External | [Team] | [Status] |

### 8.2 Risks
| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| [Risk] | H/M/L | H/M/L | [Strategy] |

---

## 9. Appendices

### 9.1 Glossary
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

### 9.2 References
- [Reference 1]
- [Reference 2]

### 9.3 Version History
| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0.0 | [Date] | [Name] | Initial release |

---

## Approvals

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Owner | | | |
| Technical Lead | | | |
| Business Stakeholder | | | |
```

---

## Method 2: API Specification (OpenAPI)

### OpenAPI Template

```yaml
openapi: 3.0.0
info:
  title: [API Name]
  version: 1.0.0
  description: |
    [API description]
  contact:
    name: [Team Name]
    email: [Email]

servers:
  - url: https://api.example.com/v1
    description: Production
  - url: https://api-staging.example.com/v1
    description: Staging

paths:
  /users:
    get:
      summary: List users
      description: Returns a list of users
      operationId: listUsers
      tags:
        - Users
      parameters:
        - name: page
          in: query
          schema:
            type: integer
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
            maximum: 100
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/User'
                  pagination:
                    $ref: '#/components/schemas/Pagination'
        '401':
          $ref: '#/components/responses/Unauthorized'
        '500':
          $ref: '#/components/responses/InternalError'

    post:
      summary: Create user
      description: Creates a new user
      operationId: createUser
      tags:
        - Users
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateUserRequest'
      responses:
        '201':
          description: User created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '400':
          $ref: '#/components/responses/BadRequest'
        '409':
          description: User already exists

components:
  schemas:
    User:
      type: object
      required:
        - id
        - email
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
        name:
          type: string
        createdAt:
          type: string
          format: date-time

    CreateUserRequest:
      type: object
      required:
        - email
        - password
      properties:
        email:
          type: string
          format: email
        password:
          type: string
          minLength: 8
        name:
          type: string

    Pagination:
      type: object
      properties:
        page:
          type: integer
        limit:
          type: integer
        total:
          type: integer

  responses:
    Unauthorized:
      description: Authentication required
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
    BadRequest:
      description: Invalid request
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
    InternalError:
      description: Internal server error
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'

  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security:
  - bearerAuth: []
```

---

## Method 3: BDD Scenarios (Gherkin)

### Feature File Template

```gherkin
# File: features/user_login.feature

@authentication @priority-high
Feature: User Login
  As a registered user
  I want to log into the system
  So that I can access my account and features

  Background:
    Given the system is available
    And the user database contains test users

  @happy-path
  Scenario: Successful login with valid credentials
    Given a user exists with email "user@example.com" and password "SecurePass123"
    And the user account is active and not locked
    When the user navigates to the login page
    And enters email "user@example.com"
    And enters password "SecurePass123"
    And clicks the "Login" button
    Then the user should be redirected to the dashboard
    And should see "Welcome back" message
    And a session should be created

  @error-handling
  Scenario: Login fails with invalid password
    Given a user exists with email "user@example.com"
    When the user attempts to login with email "user@example.com"
    And enters incorrect password "WrongPassword"
    Then the system should display "Invalid email or password"
    And the user should remain on the login page
    And no session should be created

  @security
  Scenario: Account lockout after multiple failed attempts
    Given a user exists with email "user@example.com"
    And the user has failed login 4 times
    When the user attempts to login with incorrect password
    Then the account should be locked for 15 minutes
    And the system should display "Account locked. Try again in 15 minutes."
    And a security notification should be sent to the user's email

  @security
  Scenario Outline: Password validation rules
    Given a user is on the registration page
    When the user enters password "<password>"
    Then the system should <result>

    Examples:
      | password      | result                                    |
      | short         | display "Password must be at least 8 characters" |
      | NoNumbers!    | display "Password must contain a number"  |
      | nonumbers123  | display "Password must contain uppercase" |
      | ValidPass123! | accept the password                       |

  @edge-case
  Scenario: Login attempt with locked account
    Given a user exists with email "locked@example.com"
    And the account is locked with 10 minutes remaining
    When the user attempts to login with correct credentials
    Then the system should display "Account locked. Try again in 10 minutes."
    And should not create a session
```

---

## Method 4: Requirements Baseline Management

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
- [ ] ✅ Requirements classification matrix (FURPS+, KANO)
- [ ] ✅ User story maps and use case diagrams
- [ ] ✅ Priority ranking and release plans
- [ ] ✅ Validation report and traceability matrix
- [ ] ✅ PRD document
- [ ] ✅ API specification (if applicable)
- [ ] ✅ BDD scenarios
- [ ] ✅ Requirements baseline with version control

---

## Exit Criteria (NON-NEGOTIABLE)

| Criteria | Standard | Verification | Status |
|----------|----------|--------------|--------|
| PRD Document | Complete and reviewed | Checklist verified | [ ] |
| API Specification | OpenAPI format (if applicable) | Schema validated | [ ] |
| BDD Scenarios | Core features covered | Syntax validated | [ ] |
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
- Traceability matrix for ongoing tracking

**Remember**: Requirements specification is not the end, but the starting point of continuous evolution. Establish good change management mechanisms to ensure requirements documentation always reflects the latest understanding.
