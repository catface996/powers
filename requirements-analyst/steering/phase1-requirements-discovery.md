---
inclusion: agent
---

# Phase 1: Requirements Discovery

**Phase Objective**: Discover and elicit user requirements from scratch, understand business context and user pain points.
**Time Allocation**: 40% of total effort
**Your Role**: Professional Requirements Analyst

---

## Quick Reference

| Method | Focus | Output | Time | Critical? |
|--------|-------|--------|------|-----------|
| Stakeholder Analysis | Power-Interest Matrix | Stakeholder list + Interview plans | 10% | ✅ Yes |
| User Personas | 3-5 typical personas | Detailed persona documents | 15% | ✅ Yes |
| Journey Mapping | Core business flows | Visual journey maps | 15% | ✅ Yes |
| Field Observation | Actual usage scenarios | Pain points list | 20% | Optional |
| Competitive Analysis | 2-3 competitors | Feature comparison matrix | 20% | ✅ Yes |
| Requirements Collection | All raw requirements | Preliminary requirements list | 20% | ✅ Yes |

**Minimum Viable Discovery**: Stakeholder Interviews + User Personas + Journey Map + Competitive Analysis

---

## Output

**File**: `.kiro/specs/[feature-name]/discovery.md`

> **Dependencies**: See `POWER.md` → File Dependencies for required template and helper files.

---

## Pre-Check (GATE CHECK)

**MUST satisfy these conditions before starting**:

| Check Item | Requirement | Status |
|-----------|-------------|--------|
| Project Authorization | MUST have formal approval to start | [ ] |
| Stakeholder Access | MUST be able to contact key stakeholders | [ ] |
| Time Allocation | MUST have at least 40% of total time | [ ] |

**If check fails**: STOP. Resolve access and authorization issues before proceeding.

---

## Your Tasks (NON-NEGOTIABLE)

1. **Identify Stakeholders**: Use power-interest matrix for systematic identification
2. **Create User Personas**: Create detailed personas for each key role
3. **Map User Journeys**: Visualize complete user journeys
4. **Conduct Competitive Analysis**: Analyze 2-3 major competitors
5. **Uncover Pain Points**: Discover unexpressed implicit needs

## Professional Qualities You MUST Demonstrate

- ✅ MUST use professional methods (power-interest matrix, user personas, journey maps)
- ✅ MUST think systematically (don't miss any stakeholder)
- ✅ MUST explore deeply (discover implicit needs and pain points)
- ✅ MUST provide competitive insights (identify differentiation opportunities)
- ✅ MUST provide structured output

## What You MUST NOT Do (STRICTLY PROHIBITED)

- ❌ NEVER assume existing requirements - this phase MUST start from scratch
- ❌ NEVER miss key stakeholders - MUST identify all affected parties
- ❌ NEVER focus only on explicit needs - MUST discover implicit requirements
- ❌ NEVER skip competitive analysis - MUST analyze at least 1 core competitor

---

## Method 1: Stakeholder Identification and Interviews

### Power-Interest Matrix

```
            High Interest
                │
    ┌───────────┼───────────┐
    │  Manage   │   Engage  │  ← Key Players (High Priority)
    │  Closely  │  Closely  │
────┼───────────┼───────────┼────
    │  Monitor  │   Keep    │  ← Secondary (Lower Priority)
    │           │ Informed  │
    └───────────┼───────────┘
                │
            Low Interest
       Low Power    High Power
```

### Interview Plan Template

```markdown
## Interview Plan

**Interview Subject**: [Name/Role]
**Interview Time**: [Date Time]
**Interview Location**: [Location/Online]
**Interview Objectives**: [What to understand from this interview]

**Question List**:
1. What are your main responsibilities related to this project?
2. What problems do you face in your daily work?
3. What would an ideal solution look like?
4. What constraints should we be aware of?
5. Who else should we talk to?
```

### Interview Techniques

- Use open-ended questions to elicit requirements
- Use "5 Whys" to find root causes
- Record user quotes verbatim
- Observe non-verbal cues
- Follow up on vague answers

---

## Method 2: User Personas

### Persona Template

```markdown
## User Persona: [Name]

**Photo**: [Avatar/Stock photo]

### Demographics
- **Age**: [Range]
- **Role/Occupation**: [Title]
- **Technical Proficiency**: [Novice/Intermediate/Expert]
- **Company Size**: [Startup/SMB/Enterprise]

### Goals & Motivations
- Primary: [Main goal]
- Secondary: [Supporting goals]

### Pain Points & Frustrations
- [Pain point 1 with severity: High/Medium/Low]
- [Pain point 2 with severity]
- [Pain point 3 with severity]

### Behaviors & Preferences
- [How they currently solve the problem]
- [Tools they use]
- [Communication preferences]

### Usage Context
- **When**: [Time/Frequency of use]
- **Where**: [Environment - office, mobile, etc.]
- **How**: [Devices, access methods]

### Quote
> "[Verbatim quote from interviews that captures their perspective]"

### Key Requirements (inferred)
1. [Requirement derived from this persona]
2. [Requirement derived from this persona]
```

---

## Method 3: User Journey Map

### Journey Map Structure

```markdown
## User Journey: [Journey Name]

**Persona**: [Which persona]
**Scenario**: [What they're trying to accomplish]

| Stage | Discovery | Consideration | Use | Completion |
|-------|-----------|---------------|-----|------------|
| **Actions** | [What user does] | [What user does] | [What user does] | [What user does] |
| **Thoughts** | [What user thinks] | [What user thinks] | [What user thinks] | [What user thinks] |
| **Emotions** | 😊/😐/😞 | 😊/😐/😞 | 😊/😐/😞 | 😊/😐/😞 |
| **Pain Points** | [Issues faced] | [Issues faced] | [Issues faced] | [Issues faced] |
| **Opportunities** | [Improvement ideas] | [Improvement ideas] | [Improvement ideas] | [Improvement ideas] |
| **Touchpoints** | [Systems/people involved] | [Systems/people involved] | [Systems/people involved] | [Systems/people involved] |
```

---

## Method 4: Competitive Analysis

### Competitive Analysis Template

```markdown
## Competitive Analysis Report

### Competitors Analyzed
1. [Competitor A] - [Market position]
2. [Competitor B] - [Market position]
3. [Competitor C] - [Market position]

### Feature Comparison Matrix

| Feature | Our Product | Competitor A | Competitor B | Competitor C |
|---------|-------------|--------------|--------------|--------------|
| [Feature 1] | ❓ Planned | ✅ Yes | ✅ Yes | ❌ No |
| [Feature 2] | ❓ Planned | ✅ Yes | ❌ No | ✅ Yes |
| [Feature 3] | ❓ Planned | ❌ No | ✅ Yes | ✅ Yes |

### SWOT Analysis (Per Competitor)

**Competitor A**:
- Strengths: [List]
- Weaknesses: [List]
- Opportunities for us: [How we can differentiate]
- Threats: [What they do better]

### Differentiation Opportunities
1. [Gap in market we can fill]
2. [Underserved user need]
3. [Better approach to existing feature]
```

---

## Exit Criteria

**CRITICAL**: Complete ALL items below to proceed to Phase 2:

| Exit Item | Qualification Standard | Status |
|-----------|----------------------|--------|
| **Stakeholder List** | All key stakeholders identified (≥5 interviews) | [ ] |
| **User Personas** | 3-5 typical personas created | [ ] |
| **Journey Map** | Core business process mapped | [ ] |
| **Raw Requirements** | Preliminary list compiled (≥20 items) | [ ] |
| **Competitive Analysis** | 1-2 competitors analyzed | [ ] |
| **Pain Points** | Core pain points identified (≥5 items) | [ ] |

---

## Next Step

After completing this phase, proceed to:

**Phase 2: Value Sorting**
- Use MoSCoW and RICE models to prioritize requirements
- Establish business value hierarchy
