---
inclusion: agent
---

# Discovery Output Template

**Output File**: `.kiro/specs/[feature-name]/discovery.md`

---

## File Template

```markdown
# Discovery: [Feature Name]

**Created**: [Date]
**Status**: In Progress | Completed

---

## 1. Project Overview

**Project Name**: [Name]
**Business Context**: [Brief description]
**Project Goals**: [What success looks like]

---

## 2. Stakeholders

### Power-Interest Matrix

\`\`\`mermaid
quadrantChart
    title Stakeholder Analysis
    x-axis Low Interest --> High Interest
    y-axis Low Power --> High Power
    quadrant-1 Manage Closely
    quadrant-2 Keep Satisfied
    quadrant-3 Monitor
    quadrant-4 Keep Informed
    Stakeholder1: [0.8, 0.9]
    Stakeholder2: [0.6, 0.4]
\`\`\`

### Stakeholder List

| Name/Role | Power | Interest | Strategy | Contact |
|-----------|-------|----------|----------|---------|
| [Name] | High/Medium/Low | High/Medium/Low | [Strategy] | [Contact] |

---

## 3. User Personas

### Persona 1: [Name]

| Attribute | Description |
|-----------|-------------|
| **Role** | [Job title/role] |
| **Goals** | [Primary goals] |
| **Pain Points** | [Key frustrations] |
| **Tech Proficiency** | Novice/Intermediate/Expert |

**Quote**: "[Representative quote]"

---

## 4. User Journey Map

\`\`\`mermaid
journey
    title [User Journey Name]
    section Discovery
      Task 1: 5: User
      Task 2: 3: User
    section Usage
      Task 3: 4: User, System
      Task 4: 2: User
    section Completion
      Task 5: 5: User
\`\`\`

### Journey Details

| Stage | Actions | Thoughts | Pain Points | Opportunities |
|-------|---------|----------|-------------|---------------|
| [Stage] | [Actions] | [Thoughts] | [Pain] | [Opportunity] |

---

## 5. Competitive Analysis

| Feature | Our Product | Competitor A | Competitor B |
|---------|-------------|--------------|--------------|
| [Feature 1] | ❓ Planned | ✅ Yes | ❌ No |
| [Feature 2] | ❓ Planned | ✅ Yes | ✅ Yes |

### Differentiation Opportunities
1. [Opportunity 1]
2. [Opportunity 2]

---

## 6. Raw Requirements List

| ID | Requirement | Source | Priority | Notes |
|----|-------------|--------|----------|-------|
| REQ-001 | [Description] | [Stakeholder] | High/Medium/Low | [Notes] |

---

## 7. Key Pain Points

1. **[Pain Point 1]**: [Description and impact]
2. **[Pain Point 2]**: [Description and impact]

---

## Next Steps

- [ ] Proceed to Phase 2: Sort (Value Sorting)
```
