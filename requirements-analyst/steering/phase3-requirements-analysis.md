---
inclusion: agent
---

# Phase 3: Requirements Analysis

**Phase Objective**: Deep analysis of dependencies, feasibility, and implementation approaches.
**Time Allocation**: 20% of total effort
**Your Role**: Professional Requirements Analyst

---

## Quick Reference

| Method | Focus | Output | When to Use |
|--------|-------|--------|-------------|
| User Story Mapping | User activities and priorities | Story map with MVP | All projects |
| Use Case Analysis | Actor-system interactions | Use case documents | Complex interactions |
| Event Storming | Domain events and commands | Domain model | Complex business logic |
| DDD Strategic Design | Bounded contexts | Context map | Large-scale systems |

---

## Pre-Check (GATE CHECK)

**MUST pass this check before starting**:

- [ ] **Phase 2 completed?** All requirements classified and categorized?
- [ ] **Inputs available?** Classification matrix and hierarchy from Phase 2 ready?
- [ ] **Unclear items identified?** Any requirements needing deeper clarification flagged?

**If ANY check fails**: STOP. NEVER proceed. Return to Phase 2.

---

## Your Tasks (NON-NEGOTIABLE)

1. **User Story Mapping**: Create complete user story maps
2. **Use Case Analysis**: Draw main use case diagrams and write use case documents
3. **Dependency Analysis**: Map requirement dependencies and identify conflicts
4. **Feasibility Assessment**: Evaluate technical feasibility and risks

## Professional Qualities You MUST Demonstrate

- ✅ Use professional methods (user story mapping, use case analysis, event storming)
- ✅ Deep analysis (requirement dependencies, technical feasibility)
- ✅ Domain modeling (identify bounded contexts, aggregates)
- ✅ Visual output (story maps, use case diagrams, domain models)

## What You MUST NEVER Do

- ❌ NEVER be superficial - deep analysis is mandatory
- ❌ NEVER ignore requirement dependencies - document all relationships
- ❌ NEVER skip technical feasibility assessment - it is required
- ❌ NEVER force-fit DDD just to use it (DDD suits complex business; simple projects can use simplified models)

---

## Method 1: User Story Mapping

### User Story Format

```
As a [role],
I want [feature/capability],
So that [business value/benefit].
```

### INVEST Criteria

Each user story MUST be:
- **I**ndependent: Can be developed separately
- **N**egotiable: Details can be discussed
- **V**aluable: Delivers value to user/business
- **E**stimable: Can be sized/estimated
- **S**mall: Fits within a sprint
- **T**estable: Has clear acceptance criteria

### User Story Map Template

```
┌─────────────────────────────────────────────────────────────────────┐
│                         USER ACTIVITY FLOW                          │
├─────────────┬─────────────┬─────────────┬─────────────┬────────────┤
│  Activity 1 │  Activity 2 │  Activity 3 │  Activity 4 │ Activity 5 │
│  (Browse)   │  (Select)   │  (Purchase) │  (Receive)  │ (Support)  │
├─────────────┼─────────────┼─────────────┼─────────────┼────────────┤
│ ─── MVP ─── │ ─── MVP ─── │ ─── MVP ─── │ ─── MVP ─── │ ────────── │
│ Story 1.1   │ Story 2.1   │ Story 3.1   │ Story 4.1   │            │
│ Story 1.2   │ Story 2.2   │ Story 3.2   │             │            │
├─────────────┼─────────────┼─────────────┼─────────────┼────────────┤
│ ─── V1.1 ── │ ─── V1.1 ── │ ─── V1.1 ── │ ─── V1.1 ── │ ─── V1.1 ─ │
│ Story 1.3   │ Story 2.3   │ Story 3.3   │ Story 4.2   │ Story 5.1  │
│             │             │ Story 3.4   │             │            │
├─────────────┼─────────────┼─────────────┼─────────────┼────────────┤
│ ─── V2.0 ── │ ─── V2.0 ── │ ─── V2.0 ── │ ─── V2.0 ── │ ─── V2.0 ─ │
│ Story 1.4   │ Story 2.4   │ Story 3.5   │ Story 4.3   │ Story 5.2  │
└─────────────┴─────────────┴─────────────┴─────────────┴────────────┘
```

### Story Map Documentation

```markdown
## User Story Map: [Feature/Epic Name]

### User Activities (Left to Right = User Flow)
1. **[Activity 1]**: [Description of what user is trying to do]
2. **[Activity 2]**: [Description]
3. **[Activity 3]**: [Description]

### MVP Stories (Minimum to launch)
| Activity | Story ID | Story | Priority |
|----------|----------|-------|----------|
| Activity 1 | US-001 | As a [role], I want... | P0 |
| Activity 2 | US-002 | As a [role], I want... | P0 |

### V1.1 Stories (First enhancement)
| Activity | Story ID | Story | Priority |
|----------|----------|-------|----------|
| Activity 1 | US-003 | As a [role], I want... | P1 |

### V2.0 Stories (Future)
| Activity | Story ID | Story | Priority |
|----------|----------|-------|----------|
| Activity 1 | US-004 | As a [role], I want... | P2 |
```

---

## Method 2: Use Case Analysis

### Use Case Diagram Elements

```
┌─────────────────────────────────────────┐
│              System Boundary            │
│                                         │
│    ┌─────────┐      ┌─────────┐        │
│    │ Use Case│      │ Use Case│        │
│    │    A    │─────►│    B    │        │
│    └─────────┘      └─────────┘        │
│         │                │              │
│         │ <<include>>    │ <<extend>>   │
│         ▼                ▼              │
│    ┌─────────┐      ┌─────────┐        │
│    │ Use Case│      │ Use Case│        │
│    │    C    │      │    D    │        │
│    └─────────┘      └─────────┘        │
│                                         │
└─────────────────────────────────────────┘
     │                           │
     │                           │
  ┌──┴──┐                     ┌──┴──┐
  │Actor│                     │Actor│
  │  1  │                     │  2  │
  └─────┘                     └─────┘
```

### Use Case Document Template

```markdown
## Use Case: [UC-XXX] [Use Case Name]

### Basic Information
| Field | Value |
|-------|-------|
| **Use Case ID** | UC-XXX |
| **Name** | [Descriptive name] |
| **Primary Actor** | [Who initiates] |
| **Secondary Actors** | [Other participants] |
| **Level** | User Goal / Subfunction |
| **Priority** | P0 / P1 / P2 |

### Description
[Brief description of what this use case accomplishes]

### Preconditions
1. [Condition that must be true before starting]
2. [Another precondition]

### Postconditions (Success)
1. [State after successful completion]
2. [Another post-condition]

### Main Flow (Happy Path)
| Step | Actor | System |
|------|-------|--------|
| 1 | [Actor action] | |
| 2 | | [System response] |
| 3 | [Actor action] | |
| 4 | | [System response] |

### Alternative Flows
**A1: [Alternative scenario name]**
- Branches from step: [X]
- Condition: [When this alternative applies]
- Steps:
  1. [Alternative step]
  2. [Alternative step]
- Rejoins at step: [Y] or ends

### Exception Flows
**E1: [Error scenario name]**
- Trigger: [What causes this exception]
- Steps:
  1. System displays error message: "[Exact message]"
  2. [Recovery action]
- End state: [How it ends]

### Business Rules
| Rule ID | Rule Description |
|---------|------------------|
| BR-001 | [Rule that applies to this use case] |
| BR-002 | [Another rule] |

### Non-Functional Requirements
- **Performance**: [Specific metrics]
- **Security**: [Security requirements]
```

---

## Method 3: Event Storming (for Complex Systems)

### Event Storming Elements

| Element | Color | Description | Example |
|---------|-------|-------------|---------|
| **Domain Event** | Orange | Something that happened | "Order Placed" |
| **Command** | Blue | Action that triggers event | "Place Order" |
| **Aggregate** | Yellow | Entity that receives command | "Order" |
| **Policy** | Purple | Reaction rule | "When order placed, notify warehouse" |
| **Read Model** | Green | Data needed for decision | "Available inventory" |
| **External System** | Pink | Third-party integration | "Payment Gateway" |
| **User/Actor** | Small yellow | Who triggers command | "Customer" |
| **Hot Spot** | Red | Unresolved question | "How to handle split shipment?" |

### Event Storming Output

```markdown
## Event Storming Results: [Domain Name]

### Timeline (Left to Right)
```
[User] → [Command] → [Aggregate] → [Domain Event] → [Policy] → [Next Command]
```

### Domain Events Identified
| Event | Aggregate | Triggered By | Triggers |
|-------|-----------|--------------|----------|
| Order Created | Order | Place Order command | Inventory Reserved |
| Payment Received | Payment | Process Payment command | Order Confirmed |
| Order Shipped | Order | Ship Order command | Customer Notified |

### Commands Identified
| Command | Actor | Aggregate | Preconditions |
|---------|-------|-----------|---------------|
| Place Order | Customer | Order | Cart not empty |
| Process Payment | System | Payment | Order created |
| Ship Order | Warehouse Staff | Order | Payment received |

### Aggregates Identified
| Aggregate | Responsibilities | Key Attributes |
|-----------|------------------|----------------|
| Order | Manage order lifecycle | items, status, total |
| Payment | Handle payment processing | amount, status, method |
| Inventory | Track stock levels | quantity, reserved |

### Hot Spots (Unresolved Questions)
1. 🔴 [Question 1 - needs clarification]
2. 🔴 [Question 2 - needs decision]
```

---

## Method 4: Dependency Analysis

### Dependency Types

| Type | Description | Example | Risk Level |
|------|-------------|---------|------------|
| **Mandatory** | Must complete A before B | Login before checkout | High |
| **Optional** | A enhances B | Search filters enhance search | Low |
| **Conflicting** | A and B cannot coexist | Two auth methods | Critical |
| **External** | Depends on outside system | Payment gateway | High |

### Dependency Matrix

```markdown
## Requirements Dependency Matrix

| Req ID | Depends On | Dependency Type | Impact if Delayed |
|--------|------------|-----------------|-------------------|
| REQ-005 | REQ-001, REQ-002 | Mandatory | Blocks entire feature |
| REQ-008 | REQ-005 | Mandatory | Blocks payment flow |
| REQ-010 | External API | External | Risk: API availability |
| REQ-012 | REQ-003 | Optional | Degraded experience |

### Dependency Graph
```
REQ-001 ──┐
          ├──► REQ-005 ──► REQ-008 ──► REQ-011
REQ-002 ──┘        │
                   └──► REQ-009
REQ-003 ──────────────► REQ-012 (optional)
```

### Critical Path
REQ-001 → REQ-005 → REQ-008 → REQ-011 (blocks release)

### Risks Identified
| Risk | Requirements | Mitigation |
|------|--------------|------------|
| Circular dependency | [List] | [Solution] |
| External dependency | [List] | [Fallback plan] |
```

---

## Exit Criteria (NON-NEGOTIABLE)

| Criteria | Standard | Verification | Status |
|----------|----------|--------------|--------|
| User Story Map | Core user journeys mapped | Verify activity flow | [ ] |
| Use Case Diagrams | Main use cases documented | Review interactions | [ ] |
| Domain Model | Bounded contexts identified (if applicable) | Verify aggregates | [ ] |
| Dependency Graph | Dependencies mapped | Check for circular | [ ] |
| Feasibility Assessment | Technical risks evaluated | Risk assessment complete | [ ] |

---

## Next Step

After completing this phase, proceed to:

**Phase 4: Prioritization**
- MoSCoW classification
- RICE scoring
- Release planning
