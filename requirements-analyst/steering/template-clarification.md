---
inclusion: agent
---

# Clarification Output Template

**Output File**: `.kiro/specs/[feature-name]/clarification.md`

**Standards**: Must follow Ambiguity Taxonomy from `phase4-requirements-clarification.md`

---

## File Template

```markdown
# Clarification Log: [Feature Name]

**Feature**: [feature-name]
**Session Date**: YYYY-MM-DD
**Total Questions**: [N]
**Status**: In Progress | Completed

---

## Q1: [Question Title]

**Category**: Functional Scope / Domain & Data / Interaction & UX / Non-Functional / Integration / Edge Cases / Terminology

**Question**: [Complete question text that was asked]

**Options Presented**:
- **A**: [Option A - full description]
- **B**: [Option B - full description]
- **C**: [Option C - full description]
- **Other**: Custom answer allowed

**Recommended**: Option [X] - [Reason for this recommendation]

**User's Choice**: [The option letter user selected, or their custom answer]

**Resolution**: [How this clarification was applied to the analysis document]

**Applied To**: [Section in requirements.md that was updated]

---

## Q2: [Question Title]

**Category**: [Category]

**Question**: [Question text]

**Options Presented**:
- **A**: [Option A]
- **B**: [Option B]
- **C**: [Option C]
- **Other**: Custom answer allowed

**Recommended**: Option [X] - [Reason]

**User's Choice**: [Choice]

**Resolution**: [How applied]

**Applied To**: [Section updated]

---

## Summary

| # | Question | Category | Choice | Applied To |
|---|----------|----------|--------|------------|
| 1 | [Brief question summary] | [Category] | [A/B/C/Custom] | [Section in requirements.md] |
| 2 | [Brief question summary] | [Category] | [A/B/C/Custom] | [Section in requirements.md] |
| 3 | [Brief question summary] | [Category] | [A/B/C/Custom] | [Section in requirements.md] |

---

## Coverage Summary

| Category | Status | Notes |
|----------|--------|-------|
| **Functional Scope** | Resolved / Clear / Deferred | [Brief note] |
| **Domain & Data** | Resolved / Clear / Deferred | [Brief note] |
| **Interaction & UX** | Resolved / Clear / Deferred | [Brief note] |
| **Non-Functional** | Resolved / Clear / Deferred | [Brief note] |
| **Integration** | Resolved / Clear / Deferred | [Brief note] |
| **Edge Cases** | Resolved / Clear / Deferred | [Brief note] |
| **Terminology** | Resolved / Clear / Deferred | [Brief note] |

**Status Legend**:
- **Resolved**: Was ambiguous, now clarified through Q&A
- **Clear**: Already sufficient in analysis document
- **Deferred**: Non-blocking, can resolve during implementation

---

## Impact on Analysis Document

### Sections Modified

| Section | Change Description |
|---------|-------------------|
| [Section 1] | [Brief description of change] |
| [Section 2] | [Brief description of change] |

### User Stories Updated

| Story ID | Original | Updated |
|----------|----------|---------|
| US-XXX | [Original text] | [Updated based on clarification] |

### Success Criteria Updated

| SC ID | Original | Updated |
|-------|----------|---------|
| SC-XXX | [Original] | [Updated based on clarification] |

### New Requirements Added

| Req ID | Description | Source |
|--------|-------------|--------|
| REQ-XXX | [New requirement added based on clarification] | Q[N] |

---

## Deferred Items

Items that were identified but deferred for later resolution:

| Item | Category | Reason for Deferral | When to Resolve |
|------|----------|---------------------|-----------------|
| [Item 1] | [Category] | [Why deferred] | [Implementation / Design phase] |
| [Item 2] | [Category] | [Why deferred] | [Implementation / Design phase] |

---

## Assumptions Documented

| ID | Assumption | Related Req | Risk if Wrong | Validated |
|----|------------|-------------|---------------|-----------|
| ASM-001 | [Assumption made during clarification] | REQ-XXX | [Risk] | Yes/No |

---

## Out of Scope (Confirmed)

| Item | Reason | Future Consideration |
|------|--------|---------------------|
| [Item] | [Why out of scope] | v2.0 / Never |

---

## Session Notes

[Any additional notes about the clarification session, observations, or recommendations for future phases]

---

## Cross-References

- **Analysis Document**: [requirements.md](./requirements.md) - Updated with clarifications
- **Previous Phase**: [sort.md](./sort.md) - Value sorting reference
- **Next Phase**: [validation.md](./validation.md) - To be created

---

## Next Steps Available

**What would you like to do next?**

| Option | Action | When to Choose |
|--------|--------|----------------|
| **A** | **Clarify** (Continue) | Deferred items need resolution, or new ambiguities found |
| **B** | **Analyze** (Re-analyze) | Significant changes require updating analysis document |
| **C** | **Validate** (Proceed) | All critical ambiguities resolved, ready for validation |

### Recommendation

[Based on Coverage Summary above, recommend Option A/B/C]

**Reason**: [Explain why this option is recommended]

---
**Reply with A, B, or C to proceed.**
```
