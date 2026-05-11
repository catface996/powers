# Waiver Protocol

**Purpose**: A uniform mechanism for explicitly accepting deviations from AI-DLC rules (testability constraints, quality gates, coverage claims, test-quality checklist items). Without this, "waiver" becomes an undocumented escape hatch used by default.

**Scope**: Any AI-DLC rule that can fail a check (testability constraints, quality gates, test-quality validation, coverage claims, AC traceability). Does NOT apply to user approval of stage completion — those are recorded in `audit.md`.

---

## MANDATORY: Rules for Waivers

1. **Waivers are explicit, not implicit.** A missing assertion or a silently skipped test is not a waiver — it is a defect.
2. **Waivers have owners.** Every waiver names a human owner accountable for the decision.
3. **Waivers expire.** Every waiver has a review date. Expired waivers are re-evaluated, not auto-renewed.
4. **Waivers do not block other gates.** One waived gate cannot cascade into silent acceptance of others.
5. **Waivers require user approval.** AI never waives rules on its own authority — it can only propose a waiver for user approval.

---

## Waiver File

**Location**: `aidlc-docs/waivers/{WAV-ID}.md` (one file per waiver)

**Index**: `aidlc-docs/waivers/INDEX.md` (one-line summary per waiver, auto-updated)

**ID Scheme**: `WAV-nnn` (zero-padded 3 digits, monotonic, never reused)

## Waiver File Format

```markdown
---
id: WAV-007
status: active | expired | revoked
created: 2026-05-11
review_by: 2026-08-11
owner: [human name or role]
approver: [human name or role]
rule_type: testability-constraint | quality-gate | test-quality-check | coverage-claim | traceability | other
rule_reference: [file:section:rule-id, e.g., inception-test-strategy.md:testability-constraints:TCON-03]
scope: [unit-name | system-wide | specific-test-id | specific-ac-id]
---

# WAV-007: [One-line title]

## Rule Being Waived
[Quote the exact rule text, or cite by ID with enough context to understand]

## What Is Being Accepted
[Concrete description of the deviation: what does reality look like, how does it differ from the rule]

## Reason
[Why the rule cannot or should not be followed in this scope. Must be a technical or business reason, not "running out of time"]

## Risk Accepted
[What could go wrong in production as a result. Be specific about failure modes, not generic hand-waving]

## Mitigation
[Compensating controls: monitoring, manual checks, documentation, follow-up tickets]

## Expiration Behavior
- **Review date**: [date, typically 3-6 months]
- **On expiration**: [re-evaluate / auto-revoke / force re-approval]
- **Revocation trigger**: [conditions that void this waiver before expiration, e.g., "if the underlying vendor API gains a proper sandbox"]

## History
- 2026-05-11: Created by [owner], approved by [approver]
- [future amendments appended; never edit prior entries]
```

## Index File Format

`aidlc-docs/waivers/INDEX.md`:

```markdown
# Waiver Index

| ID      | Status  | Scope            | Rule                           | Review By   | Owner    |
|---------|---------|------------------|--------------------------------|-------------|----------|
| WAV-001 | active  | order-svc        | Unit branch coverage >= 70%    | 2026-08-01  | Alice    |
| WAV-002 | expired | system-wide      | Zero flaky tests on main       | 2026-03-15  | Bob      |
| WAV-007 | active  | AC-019 (manual)  | AC automated test evidence     | 2026-11-01  | Carol    |
```

---

## How AI-DLC Proposes a Waiver

When AI-DLC encounters a rule it cannot satisfy without user input:

1. **Do NOT silently proceed.** The work is blocked.
2. **Draft a waiver file** at `aidlc-docs/waivers/WAV-{next-id}.md.draft` with all fields AI can infer, `status: draft`.
3. **Explain to the user**:
   - Which rule is blocking
   - Why AI cannot satisfy it automatically
   - What the proposed waiver accepts and mitigates
4. **Wait for explicit user approval**. No approval = no waiver = no progress past the blocked gate.
5. On approval:
   - Rename `.draft` -> `.md`
   - Set `status: active`, fill `approver` field
   - Update `INDEX.md`
   - Log the waiver ID in `audit.md`
6. On rejection:
   - Delete the `.draft`
   - Return to the stage that produced the violation and fix at source

---

## When Waivers Are Valid (and When They Are Not)

### Valid waiver reasons

- Vendor limitation outside team control (e.g., API has no sandbox)
- Hardware constraint (e.g., cannot load-test on CI hardware)
- Legacy code scheduled for replacement (with referenced migration ticket)
- One-time operation (e.g., data migration script used once)
- Regulatory obligation conflicting with rule (e.g., real production data required for specific audit test)

### Invalid waiver reasons (reject)

- "Running out of time"
- "Fix later" without a referenced ticket and target date
- "Team prefers this way"
- "Other teams do it this way"
- "The test is flaky so we skip it" — flakiness is fixed, not waived
- "Coverage dropped; we will address in next sprint" without a specific plan

AI-DLC should push back on invalid reasons rather than accept them.

---

## Waiver Lifecycle

```
draft  -->  active  -->  expired  -->  revoked (if not re-approved)
                  \--->  revoked (if trigger fires)
```

- **draft**: AI proposed, user not yet approved
- **active**: User approved, within review date
- **expired**: Review date passed; must be re-evaluated before downstream work trusts it
- **revoked**: Explicitly canceled by user or by revocation trigger

Build and Test quality gate MUST:
- Honor `active` waivers
- Treat `expired` waivers as `active` only for 14 days past review date, then as `revoked`
- Never honor `draft` or `revoked` waivers

---

## Waiver Usage by Stage

| Stage                       | What a waiver can cover                                           |
|-----------------------------|-------------------------------------------------------------------|
| Application Design          | A testability-review finding that cannot be remediated            |
| Test Strategy               | A traceability gap (AC without test-layer assignment)             |
| Test Design                 | A coverage-claim gap, a mock without a contract anchor            |
| Code Generation             | A testability-constraint violation                                |
| Build and Test quality gate | Any gate failure (coverage, mutation, flakiness, AC coverage, NFR)|

---

## Integration With Other Rules

- Referenced by `inception-test-strategy.md` (testability constraint deviations)
- Referenced by `construction-test-design.md` (coverage gaps, unanchored mocks)
- Referenced by `construction-build-and-test.md` (quality gate failures)
- Referenced by `common-test-quality.md` (forbidden smell exceptions for legacy tests)
- Audit entries per waiver creation/expiration/revocation logged in `audit.md`
