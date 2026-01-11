---
inclusion: agent
---

# Value Sorting Output Template

**Output File**: `.kiro/specs/[feature-name]/sort.md`

---

## File Template

```markdown
# Value Sorting: [Feature Name]

**Created**: [Date]
**Status**: In Progress | Completed

---

## 1. MoSCoW Classification

### Summary

| Category | Count | Percentage | Status |
|----------|-------|------------|--------|
| MUST | X | X% | ✅ ≤30% |
| SHOULD | X | X% | - |
| COULD | X | X% | - |
| WON'T | X | X% | - |

### MUST Have (≤30%)

| Req ID | Requirement | Justification |
|--------|-------------|---------------|
| REQ-001 | [Description] | [Why MUST] |

### SHOULD Have

| Req ID | Requirement | Impact if Deferred |
|--------|-------------|-------------------|
| REQ-002 | [Description] | [Impact] |

### COULD Have

| Req ID | Requirement | Value Add |
|--------|-------------|-----------|
| REQ-003 | [Description] | [Benefit] |

### WON'T Have (This Release)

| Req ID | Requirement | Reason |
|--------|-------------|--------|
| REQ-004 | [Description] | [Why not now] |

---

## 2. RICE Scoring

| Req ID | Reach | Impact | Confidence | Effort | Score | Rank |
|--------|-------|--------|------------|--------|-------|------|
| REQ-001 | [num] | [0.25-3] | [%] | [months] | [calc] | 1 |

**Formula**: Score = (Reach × Impact × Confidence) / Effort

---

## 3. Value-Cost Matrix

\`\`\`mermaid
quadrantChart
    title Value-Cost Analysis
    x-axis Low Cost --> High Cost
    y-axis Low Value --> High Value
    quadrant-1 P0: Quick Win
    quadrant-2 P1: Strategic
    quadrant-3 P2: Fill-in
    quadrant-4 P3: Avoid
    REQ001: [0.2, 0.9]
    REQ002: [0.8, 0.8]
    REQ003: [0.3, 0.3]
\`\`\`

| Priority | Requirements | Action |
|----------|--------------|--------|
| P0 (Quick Win) | REQ-001 | Do First |
| P1 (Strategic) | REQ-002 | Plan Carefully |
| P2 (Fill-in) | REQ-003 | If Time Permits |
| P3 (Avoid) | REQ-004 | Deprioritize |

---

## 4. Release Plan

### MVP (v1.0)

**Target**: [Date]
**Theme**: Core functionality

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| REQ-001 | [Description] | MUST |

### Version 1.1

**Target**: [Date]
**Theme**: Enhanced usability

| Req ID | Requirement | Priority |
|--------|-------------|----------|
| REQ-002 | [Description] | SHOULD |

### Roadmap

\`\`\`mermaid
gantt
    title Release Roadmap
    dateFormat YYYY-MM-DD
    section MVP
    Core Features    :a1, 2024-01-01, 60d
    section v1.1
    Enhancements     :a2, after a1, 30d
    section v2.0
    Advanced Features :a3, after a2, 45d
\`\`\`

---

## Next Steps

- [ ] Proceed to Phase 3: Analyze (Requirements Analysis)
```
