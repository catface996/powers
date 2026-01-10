---
inclusion: agent
---

# Analysis Output Template

**Output File**: `.kiro/specs/[feature-name]/03-analysis.md`

**Standards**: Must follow `helper-diagram-standards.md`

---

## File Template

```markdown
# Analysis: [Feature Name]

**Created**: [Date]
**Status**: In Progress | Completed

---

## 1. User Personas

| Persona | Description | Key Goals |
|---------|-------------|-----------|
| [Persona 1] | [Brief description] | [Primary goals] |
| [Persona 2] | [Brief description] | [Primary goals] |

---

## 2. Core User Activity Flow

### Activity Diagram

\`\`\`mermaid
stateDiagram-v2
    [*] --> Activity1: Start

    Activity1 --> Decision1
    state Decision1 <<choice>>
    Decision1 --> Activity2: [Condition A]
    Decision1 --> Activity3: [Condition B]

    state ParallelProcessing {
        direction LR
        [*] --> Task1
        [*] --> Task2
        Task1 --> [*]
        Task2 --> [*]
    }

    Activity2 --> ParallelProcessing
    Activity3 --> Activity4
    ParallelProcessing --> Activity5

    Activity4 --> Activity5
    Activity5 --> [*]: End
\`\`\`

### Activity Details

| Activity | Description | Input | Output | Participants |
|----------|-------------|-------|--------|--------------|
| **Activity 1** | [Description] | [Input] | [Output] | [Who] |
| **Activity 2** | [Description] | [Input] | [Output] | [Who] |

---

## 3. User Story Map

### Release Planning

| Activity | MVP | v1.1 | v2.0 |
|----------|-----|------|------|
| **[Activity 1]** | US-001, US-002 | US-003 | US-004 |
| **[Activity 2]** | US-005 | US-006, US-007 | - |

---

## 4. User Stories

### Activity 1: [Activity Name]

#### US-001: [Story Title]

**Priority**: P0 | P1 | P2
**Persona**: [Which persona]
**Release**: MVP | v1.1 | v2.0

**Story**:
> As a [role],
> I want [feature/capability],
> So that [business value/benefit].

**Acceptance Criteria**:

\`\`\`gherkin
Scenario: [Scenario name]
  Given [precondition]
  When [action]
  Then [expected result]
\`\`\`

**INVEST Check**:
- [ ] **I**ndependent
- [ ] **N**egotiable
- [ ] **V**aluable
- [ ] **E**stimable
- [ ] **S**mall
- [ ] **T**estable

---

## 5. Use Case Diagram

\`\`\`mermaid
graph TB
    subgraph SystemBoundary["System Boundary"]
        direction TB
        UC1((UC-001<br/>Use Case 1))
        UC2((UC-002<br/>Use Case 2))
        UC3((UC-003<br/>Use Case 3))
        UC4((UC-004<br/>Use Case 4))

        UC1 -->|<<include>>| UC2
        UC3 -.->|<<extend>>| UC1
    end

    Actor1[/"👤 Actor 1"\]
    Actor2[/"👤 Actor 2"\]
    External[/"🔌 External System"\]

    Actor1 --> UC1
    Actor1 --> UC3
    Actor2 --> UC2
    UC4 --> External

    style UC1 fill:#e1f5fe,stroke:#01579b
    style UC2 fill:#e1f5fe,stroke:#01579b
    style UC3 fill:#fff3e0,stroke:#e65100
    style UC4 fill:#e1f5fe,stroke:#01579b
\`\`\`

### Use Case List

| UC ID | Name | Primary Actor | Priority | Description |
|-------|------|---------------|----------|-------------|
| **UC-001** | [Name] | [Actor] | P0 | [Brief description] |
| **UC-002** | [Name] | [Actor] | P0 | [Brief description] |

---

## 6. Use Case Details

### UC-001: [Use Case Name]

| Field | Value |
|-------|-------|
| **Use Case ID** | UC-001 |
| **Name** | [Descriptive name] |
| **Primary Actor** | [Who initiates] |
| **Secondary Actors** | [Other participants] |
| **Priority** | P0 / P1 / P2 |

#### Main Flow Sequence Diagram

\`\`\`mermaid
sequenceDiagram
    autonumber

    actor User as 👤 User
    participant UI as 🖥️ Interface
    participant System as ⚙️ System
    participant Agent as 🤖 Agent
    participant DB as 🗄️ Database

    User->>UI: 1. Initiate Request
    activate UI
    UI->>System: 2. Forward Request
    activate System

    par Parallel Processing
        System->>Agent: 3a. Analyze Request
        activate Agent
        Agent-->>System: 3a. Analysis Result
        deactivate Agent
    and
        System->>DB: 3b. Query Data
        activate DB
        DB-->>System: 3b. Return Data
        deactivate DB
    end

    alt Success
        System-->>UI: 4. Success Response
        UI-->>User: 5. Display Result
    else Failure
        System-->>UI: 4. Error Response
        UI-->>User: 5. Display Error
    end

    deactivate System
    deactivate UI
\`\`\`

#### Preconditions
1. [Condition that must be true before starting]

#### Postconditions (Success)
1. [State after successful completion]

#### Alternative Flows

**A1: [Alternative scenario name]**
- **Trigger**: [When this alternative applies]
- **Description**: [What happens]

#### Exception Flows

**E1: [Error scenario name]**
- **Trigger**: [What causes this exception]
- **System Response**: "[Error message]"
- **Recovery**: [How to recover]

---

## 7. Success Criteria

### Success Criteria Summary

| SC ID | Requirement | Category | Metric | Target | Verification |
|-------|-------------|----------|--------|--------|--------------|
| **SC-001** | US-001 | Functional | [Metric] | [Target] | [Method] |
| **SC-002** | US-001 | Performance | [Metric] | [Target] | [Method] |
| **SC-003** | US-002 | Usability | [Metric] | [Target] | [Method] |
| **SC-004** | REQ-001 | Business | [Metric] | [Target] | [Method] |

### SC-001: [Criterion Name]

| Field | Value |
|-------|-------|
| **Requirement** | US-001 / REQ-XXX |
| **Category** | Functional / Performance / Usability / Business / Quality |
| **Metric** | [What to measure] |
| **Target** | [Quantified goal] |
| **Baseline** | [Current state, if applicable] |
| **Measurement Method** | [How to measure] |
| **Verification Point** | [When to verify: Development / Testing / Post-launch] |

**Definition of Success**:
> [Clear statement describing what success looks like for this criterion]

**Definition of Failure**:
> [Clear statement describing what constitutes failure]

### Success Criteria Traceability

\`\`\`mermaid
graph LR
    subgraph Requirements
        REQ[REQ-001]
        US1[US-001]
        US2[US-002]
    end

    subgraph SuccessCriteria[Success Criteria]
        SC1[SC-001<br/>Functional]
        SC2[SC-002<br/>Performance]
        SC3[SC-003<br/>Usability]
        SC4[SC-004<br/>Business]
    end

    subgraph Verification
        TC[Test Cases]
        KPI[KPIs]
        MON[Monitoring]
    end

    US1 --> SC1
    US1 --> SC2
    US2 --> SC3
    REQ --> SC4

    SC1 --> TC
    SC2 --> MON
    SC3 --> TC
    SC4 --> KPI

    style SC1 fill:#e8f5e9,stroke:#1b5e20
    style SC2 fill:#e8f5e9,stroke:#1b5e20
    style SC3 fill:#e8f5e9,stroke:#1b5e20
    style SC4 fill:#e8f5e9,stroke:#1b5e20
\`\`\`

---

## 8. Dependency Analysis

### Dependency Graph

\`\`\`mermaid
graph TD
    REQ001[REQ-001<br/>Foundation]
    REQ002[REQ-002<br/>Depends on 001]
    REQ003[REQ-003<br/>Depends on 001]
    REQ004[REQ-004<br/>Depends on 002,003]
    EXT[External API]

    REQ001 --> REQ002
    REQ001 --> REQ003
    REQ002 --> REQ004
    REQ003 --> REQ004
    EXT -.-> REQ003

    style REQ001 fill:#e1f5fe,stroke:#01579b
    style REQ004 fill:#e8f5e9,stroke:#1b5e20
    style EXT fill:#fff3e0,stroke:#e65100
\`\`\`

### Dependency Matrix

| Req ID | Depends On | Type | Impact if Delayed |
|--------|------------|------|-------------------|
| **REQ-002** | REQ-001 | Mandatory | Blocks feature |
| **REQ-003** | REQ-001, External API | Mandatory + External | High risk |
| **REQ-004** | REQ-002, REQ-003 | Mandatory | Blocks release |

### Critical Path

**Path**: REQ-001 → REQ-002 → REQ-004

---

## 9. Feasibility Assessment

| Requirement | Technical Feasibility | Risk Level | Notes |
|-------------|----------------------|------------|-------|
| **REQ-001** | High | Low | Standard implementation |
| **REQ-002** | Medium | Medium | Requires new integration |
| **REQ-003** | Low | High | External dependency |

---

## 10. Analysis Update Log (If Iterating)

> **Note**: Complete this section ONLY if `04-clarification.md` or `05-validation.md` already exist.

### Applied from 04-clarification.md

| Q# | Clarification Summary | Applied To | Section Updated |
|----|----------------------|------------|-----------------|
| Q1 | [Brief summary of clarification] | US-XXX | User Stories |
| Q2 | [Brief summary of clarification] | UC-XXX | Use Cases |

### Applied from 05-validation.md

| Issue ID | Validation Finding | Applied To | Section Updated |
|----------|-------------------|------------|-----------------|
| V-001 | [Brief summary of finding] | SC-XXX | Success Criteria |
| V-002 | [Brief summary of finding] | REQ-XXX | Dependency Analysis |

### Iteration History

| Version | Date | Trigger | Changes Made |
|---------|------|---------|--------------|
| v1.0 | [Date] | Initial analysis | Created |
| v1.1 | [Date] | Post-clarification | Updated per Q1-Q3 |
| v1.2 | [Date] | Post-validation | Addressed V-001, V-002 |

---

## 11. Analysis Summary

**User Roles Identified**:
- [Role 1]
- [Role 2]
- [Role 3]

**Core Activities**:
- [Activity 1]
- [Activity 2]
- [Activity 3]

**Key Findings**:
- **Finding 1**: [Description]
- **Finding 2**: [Description]

**Risks Identified**:
- **Risk 1**: [Description and mitigation]
- **Risk 2**: [Description and mitigation]

---

## 12. Next Steps

- [ ] Proceed to Phase 4: Clarify (Requirements Clarification)
- [ ] OR if iterating: Return to Phase 4/5 with updated analysis
```
