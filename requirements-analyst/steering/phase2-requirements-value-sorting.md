---
inclusion: agent
---

# Phase 4: Prioritization

**Phase Objective**: Prioritize requirements and develop release plans.
**Time Allocation**: 10% of total effort
**Your Role**: Professional Requirements Analyst

---

## Quick Reference

| Method | Focus | Output | When to Use |
|--------|-------|--------|-------------|
| MoSCoW | Categorical priority | MUST/SHOULD/COULD/WONT list | All projects |
| RICE Scoring | Quantitative ranking | Scored priority list | Many requirements (>20) |
| Value-Cost Matrix | Trade-off visualization | Quadrant placement | Resource constraints |
| Weighted Scoring | Multi-factor evaluation | Composite scores | Complex decisions |

**CRITICAL CONSTRAINT**: MUST requirements MUST NOT exceed 30% of total.

---

## Pre-Check (GATE CHECK)

**MUST pass this check before starting**:

- [ ] **Phase 3 completed?** All requirements analyzed with dependencies mapped?
- [ ] **Inputs available?** Domain model, feasibility assessment, dependency graph ready?
- [ ] **Unclear items identified?** Any requirements with unclear business value flagged?

**If ANY check fails**: STOP. NEVER proceed. Return to Phase 3.

---

## Your Tasks (NON-NEGOTIABLE)

1. **MoSCoW Classification**: Classify ALL requirements into MUST/SHOULD/COULD/WONT
2. **RICE Scoring**: Use RICE method for quantitative evaluation
3. **Value-Cost Analysis**: Use value-cost matrix for trade-off decisions
4. **Develop Release Plan**: Plan MVP and subsequent versions

## What You MUST NEVER Do

- ❌ NEVER prioritize based on intuition alone - use scientific methods
- ❌ NEVER let MUST priorities exceed 30% - this is a hard limit
- ❌ NEVER ignore requirement dependencies - validate against dependency graph
- ❌ NEVER develop release plan without stakeholder input

---

## Method 1: MoSCoW Classification

### MoSCoW Categories

| Category | Definition | Guidance | Typical % |
|----------|------------|----------|-----------|
| **Must Have** | Cannot launch without these | Core functionality, legal/compliance | ≤30% |
| **Should Have** | Important but not critical | Significant value, can workaround | 20-30% |
| **Could Have** | Nice to have if time permits | Enhances experience, low urgency | 20-30% |
| **Won't Have** | Not in this release | Future consideration, descoped | 10-20% |

### MoSCoW Decision Questions

| Question | If Yes → |
|----------|----------|
| Does the product fail without it? | MUST |
| Is there a legal/regulatory requirement? | MUST |
| Is there a workaround possible? | SHOULD (not MUST) |
| Will users be significantly impacted without it? | SHOULD |
| Is it a "delight" feature? | COULD |
| Can it wait for next release? | COULD or WON'T |

### MoSCoW Template

```markdown
## MoSCoW Classification: [Release/Version]

### MUST Have (≤30% of total)
| Req ID | Requirement | Justification |
|--------|-------------|---------------|
| REQ-001 | [Description] | [Why it's MUST] |
| REQ-002 | [Description] | [Why it's MUST] |

**MUST Count**: X / Y total = Z% ✅/❌ (must be ≤30%)

### SHOULD Have
| Req ID | Requirement | Impact if Deferred |
|--------|-------------|-------------------|
| REQ-003 | [Description] | [Impact] |
| REQ-004 | [Description] | [Impact] |

### COULD Have
| Req ID | Requirement | Value Add |
|--------|-------------|-----------|
| REQ-005 | [Description] | [Benefit] |

### WON'T Have (This Release)
| Req ID | Requirement | Reason for Exclusion |
|--------|-------------|---------------------|
| REQ-006 | [Description] | [Why not now] |
```

---

## Method 2: RICE Scoring

### RICE Formula

```
RICE Score = (Reach × Impact × Confidence) / Effort
```

### RICE Factors

| Factor | Scale | Description | How to Estimate |
|--------|-------|-------------|-----------------|
| **Reach** | Number | Users affected per quarter | Analytics, user research |
| **Impact** | 0.25, 0.5, 1, 2, 3 | Per-user impact | Minimal(0.25) → Massive(3) |
| **Confidence** | 0-100% | How certain are we | Data-backed(100%) → Gut(20%) |
| **Effort** | Person-months | Development cost | Engineering estimate |

### Impact Scale Guide

| Score | Level | Description | Example |
|-------|-------|-------------|---------|
| 3 | Massive | Fundamental improvement | Core workflow optimization |
| 2 | High | Significant improvement | Major pain point solved |
| 1 | Medium | Noticeable improvement | Useful enhancement |
| 0.5 | Low | Minor improvement | Small convenience |
| 0.25 | Minimal | Barely noticeable | Micro optimization |

### RICE Scoring Template

```markdown
## RICE Scoring Results

| Req ID | Reach | Impact | Confidence | Effort | RICE Score | Rank |
|--------|-------|--------|------------|--------|------------|------|
| REQ-001 | 10,000 | 2 | 80% | 2 | 8,000 | 1 |
| REQ-002 | 5,000 | 3 | 90% | 3 | 4,500 | 2 |
| REQ-003 | 8,000 | 1 | 70% | 1 | 5,600 | 3 |
| REQ-004 | 2,000 | 2 | 50% | 4 | 500 | 4 |

### Calculation Example
REQ-001: (10,000 × 2 × 0.80) / 2 = 8,000

### Priority Recommendation
1. REQ-001 (Score: 8,000) - Highest impact per effort
2. REQ-003 (Score: 5,600) - Quick win
3. REQ-002 (Score: 4,500) - High value but costly
4. REQ-004 (Score: 500) - Defer to later release
```

---

## Method 3: Value-Cost Matrix

### Value-Cost Quadrants

```
                    High Value
                        │
           ┌────────────┼────────────┐
           │     P1     │     P0     │
           │  Strategic │  Quick Win │
           │            │            │
           │ High Cost  │  Low Cost  │
           │ High Value │ High Value │
    ───────┼────────────┼────────────┼───────
           │     P3     │     P2     │
           │   Avoid    │  Fill-in   │
           │            │            │
           │ High Cost  │  Low Cost  │
           │ Low Value  │ Low Value  │
           └────────────┼────────────┘
                        │
                    Low Value
```

### Decision Rules

| Quadrant | Strategy | Action |
|----------|----------|--------|
| **P0 (Quick Win)** | Do First | High value, low effort - prioritize immediately |
| **P1 (Strategic)** | Plan Carefully | High value, high effort - worth investment but plan |
| **P2 (Fill-in)** | If Time Permits | Low value, low effort - easy add-ons |
| **P3 (Avoid)** | Deprioritize | Low value, high effort - usually not worth it |

### Value-Cost Matrix Template

```markdown
## Value-Cost Analysis

### Scoring Criteria
- **Value**: Business impact (1-10)
- **Cost**: Development effort (1-10, where 10 = highest cost)

### Requirements Placement
| Req ID | Value (1-10) | Cost (1-10) | Quadrant | Action |
|--------|--------------|-------------|----------|--------|
| REQ-001 | 9 | 3 | P0 (Quick Win) | Do First |
| REQ-002 | 8 | 8 | P1 (Strategic) | Plan Carefully |
| REQ-003 | 3 | 2 | P2 (Fill-in) | If Time Permits |
| REQ-004 | 4 | 9 | P3 (Avoid) | Deprioritize |

### Visual Placement
[Draw or describe the quadrant placement]
```

---

## Method 4: Release Planning

### MVP Definition

```markdown
## MVP (Minimum Viable Product)

**Goal**: Validate core hypotheses with minimum feature set

### MVP Criteria
- [ ] Solves the core user problem
- [ ] Technically feasible within timeline
- [ ] Provides basis for learning/iteration
- [ ] Contains only MUST requirements

### MVP Scope
| Req ID | Requirement | Why MVP |
|--------|-------------|---------|
| REQ-001 | [Description] | [Core to value proposition] |
| REQ-002 | [Description] | [Required for basic flow] |

### Not in MVP (Explicitly Excluded)
| Req ID | Requirement | Deferred To |
|--------|-------------|-------------|
| REQ-003 | [Description] | V1.1 |
| REQ-004 | [Description] | V2.0 |

### MVP Success Metrics
- [ ] [Metric 1]: [Target]
- [ ] [Metric 2]: [Target]
```

### Release Roadmap

```markdown
## Release Roadmap

### MVP (Target: [Date])
**Theme**: Core functionality
**Scope**:
- [Feature 1]
- [Feature 2]
- [Feature 3]
**Success Criteria**: [Metrics]

### Version 1.1 (Target: [Date])
**Theme**: Enhanced usability
**Scope**:
- [Feature 4]
- [Feature 5]
**Dependencies**: MVP complete

### Version 2.0 (Target: [Date])
**Theme**: Scale and advanced features
**Scope**:
- [Feature 6]
- [Feature 7]
**Dependencies**: V1.1 complete, [External dependency]

### Release Timeline
```
MVP ──────► V1.1 ──────► V2.0 ──────► V3.0
[Date]      [Date]       [Date]       [Date]
```

### Risk Factors
| Release | Risk | Mitigation |
|---------|------|------------|
| MVP | [Risk] | [Plan] |
| V1.1 | [Risk] | [Plan] |
```

---

## Stakeholder Alignment

### Priority Review Session

```markdown
## Priority Review Meeting

**Date**: [Date]
**Attendees**: [List]

### Decisions Made
1. [Decision 1]
2. [Decision 2]

### Conflicts Resolved
| Issue | Resolution | Rationale |
|-------|------------|-----------|
| [Conflict] | [How resolved] | [Why] |

### Open Items
1. [Item needing follow-up]

### Approvals
- [ ] Product Owner: _______________
- [ ] Technical Lead: _______________
- [ ] Business Stakeholder: _______________
```

---

## Exit Criteria (NON-NEGOTIABLE)

| Criteria | Standard | Verification | Status |
|----------|----------|--------------|--------|
| MoSCoW Classification | 100% requirements classified | MUST ≤ 30% | [ ] |
| RICE Scoring | Core requirements scored | Scores documented | [ ] |
| Priority List | Ranked by final score | No dependency conflicts | [ ] |
| Release Plan | MVP and versions defined | Timeline clear | [ ] |
| Stakeholder Approval | Priorities confirmed | Sign-off obtained | [ ] |

---

## Next Step

After completing this phase, proceed to:

**Phase 5: Validation**
- Requirements review meetings
- GWT acceptance criteria
- Prototype testing
- Traceability matrix
