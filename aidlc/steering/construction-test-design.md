# Test Design (Per-Unit)

**Purpose**: Derive concrete test cases from functional design and acceptance criteria, before writing test code.

**Distinction from Build & Test**: Test Design produces a *test case specification*. Build & Test *executes* tests. Writing test cases directly in code without design produces test suites that mirror implementation (and decay with it) instead of behavior.

**Position in workflow**: Construction per-unit loop. Fixed order: Functional Design -> NFR Requirements -> NFR Design -> Infrastructure Design -> **Test Design** -> Code Generation. See `core-workflow.md` for the authoritative per-unit sequence.

**Rationale for this position**: Test Design is the translation step. It converts every design decision into a verifiable assertion. To do that completely, it must run **after** all design stages have produced their outputs:
- Functional Design provides BRs, INVs, domain entities
- NFR Design introduces resilience components (circuit breaker, retry, cache, rate limit) that themselves have observable behaviors needing tests
- Infrastructure Design fixes storage, messaging, and protocol choices whose behaviors (conditional writes, message ordering, idempotency, timeout) must be tested

If Test Design ran earlier, resilience and infrastructure behaviors would be absent from `test-cases.md` and would rely on Amendment Protocol as the primary coverage mechanism — an anti-pattern.

System-level test-observability requirements do NOT depend on Test Design running first. They are captured in `inception-test-strategy.md` as TCON-nnn constraints and are honored by every design stage.

---

## Prerequisites

- Functional Design must be complete for this unit
- NFR Requirements must be complete for this unit (if executed)
- NFR Design must be complete for this unit (if executed) - its resilience components are test targets
- Infrastructure Design must be complete for this unit (if executed) - its choices introduce testable behaviors
- Test Strategy from Inception must be loaded (if Test Strategy was skipped, load available context: stories, NFRs)
- Story-to-AC mapping for this unit must be known

## When to Execute (CONDITIONAL, per-unit)

**Execute IF any of**:
- Unit implements business rules with multiple branches or states
- Unit owns acceptance criteria from user stories
- Unit has NFR targets that require automated verification
- Unit's NFR Design introduces resilience components (circuit breaker, retry, cache, rate limiter, bulkhead, fallback)
- Unit's Infrastructure Design chooses primitives with observable behaviors (conditional writes, queue semantics, idempotency, timeout handling)
- Unit is on a critical path (traceability matrix flags it)
- Unit exposes an API or contract consumed by another unit

**Skip IF**:
- Unit is pure infrastructure glue with no business logic AND no resilience patterns
- Unit is explicitly a throwaway prototype
- Test Strategy explicitly exempts this unit (rare; must be justified)

Skipping is an explicit decision recorded in the plan. Default to execute. Note that presence of NFR Design or non-trivial Infrastructure Design almost always triggers execution — those stages add testable behaviors.

---

## Execution Steps

### Step 1: Load Context

Load **every upstream design artifact** for this unit. Test Design is the integration point for all design decisions; missing an input produces a coverage gap.

System-level:
- `aidlc-docs/inception/test-strategy/test-strategy.md` - pyramid, policies, quality gates
- `aidlc-docs/inception/test-strategy/testability-constraints.md` - TCON-nnn rules to enforce
- `aidlc-docs/inception/test-strategy/traceability-matrix.md` - ACs owned by this unit
- Unit's assigned AC IDs from `aidlc-docs/inception/application-design/unit-of-work-story-map.md`

Per-unit design outputs (load all that exist):
- `aidlc-docs/construction/{unit-name}/functional-design/business-logic-model.md`
- `aidlc-docs/construction/{unit-name}/functional-design/business-rules.md` (BR-nnn IDs)
- `aidlc-docs/construction/{unit-name}/functional-design/domain-entities.md` (entities + INV-nnn invariants)
- `aidlc-docs/construction/{unit-name}/nfr-requirements/nfr-requirements.md` (NFR-nnn IDs, measurement methods)
- `aidlc-docs/construction/{unit-name}/nfr-design/nfr-design-patterns.md` (resilience patterns to test)
- `aidlc-docs/construction/{unit-name}/nfr-design/logical-components.md` (e.g., caches, queues)
- `aidlc-docs/construction/{unit-name}/infrastructure-design/infrastructure-design.md` (concrete tech choices and their observable behaviors)
- `aidlc-docs/construction/{unit-name}/infrastructure-design/deployment-architecture.md`

Quality rules:
- `common-test-quality.md` - applied to all outputs
- `common-waiver.md` - if any design element cannot be tested

### Step 2: Testability Conformance Check (MANDATORY)

**Purpose**: Verify **all** upstream design outputs for this unit comply with the system-level testability constraints (TCON-nnn) from Test Strategy. This is the **last chance** to catch untestable design before code is written.

**Three-layer testability model** (understand the division of labor):

| Layer                        | Location                                 | Responsibility                                         |
|------------------------------|------------------------------------------|--------------------------------------------------------|
| Architectural review         | `inception-application-design.md` Step 4a| Identify seams, injection points, hidden state at system level; produce `testability-review.md` |
| System-level constraints     | `inception-test-strategy.md` Step 5.5    | Publish enforceable rules as TCON-nnn in `testability-constraints.md` |
| Per-unit conformance check   | THIS STEP                                | Verify every design output for THIS unit honors all TCON-nnn |

**What this step does** (ONLY this - do not re-do upstream work):

Check every design artifact for this unit against every TCON-nnn:

1. **Functional Design conformance**: BRs, INVs, domain entities
   - Are external calls behind injectable ports? (TCON for external dependencies)
   - Is time/randomness/ID generation abstracted? (TCON-Clock, TCON-ID, etc.)
   - No hidden global state?
2. **NFR Design conformance**: resilience components
   - Circuit breaker state is observable (open / half-open / closed)?
   - Retry policy parameters are injectable (backoff, max attempts)?
   - Cache has deterministic invalidation hooks for tests?
   - Rate limiter exposes counters for verification?
3. **Infrastructure Design conformance**: tech choices
   - Chosen DB/queue/SDK has a test double strategy (fake, testcontainer, sandbox)?
   - Timeouts/retries/connection pools are configurable for test scenarios?
   - Deployment architecture does not hardcode production-only behaviors?

For every violation:
- **Preferred**: return to the responsible design stage for fix. Name the stage explicitly (Functional / NFR / Infrastructure).
- **If unavoidable**: propose waiver per `common-waiver.md` (e.g., vendor SDK with no test sandbox)

Record the check result per-artifact in `test-design-conformance.md`:

```markdown
# Testability Conformance Check

## Functional Design
- TCON-01 (injectable ports): PASS
- TCON-03 (Clock injection): PASS
- ...

## NFR Design
- TCON-01 (external calls through ports): PASS
- Observable circuit-breaker state: PASS
- Injectable retry policy: FAIL - see WAV-012

## Infrastructure Design
- TCON-01 (injectable ports): PASS
- Test double available for DynamoDB: PASS (DynamoDB Local)
- Injectable timeouts for SQS client: PASS
```

**Do NOT** in this step:
- Re-derive testability principles from scratch
- Propose new system-level constraints (that is Test Strategy's job; return to it if needed)
- Duplicate content from `testability-review.md` or `testability-constraints.md`

**Feedback loop** (which upstream stage to return to):

| Violation type                                  | Return to               |
|-------------------------------------------------|-------------------------|
| Business rule uses hidden global state          | Functional Design       |
| Entity lacks observable invariant               | Functional Design       |
| Resilience pattern has no observable state      | NFR Design              |
| Retry/cache parameters hardcoded                | NFR Design              |
| Chosen DB/SDK has no test double strategy       | Infrastructure Design   |
| Fundamental architectural defect                | Application Design (system-level) + Test Strategy |

**If Test Strategy was skipped** (no `testability-constraints.md` exists): fall back to the minimal defaults from `common-test-quality.md` (Determinism rules + Test Independence rules) and flag to user that Test Strategy should be added back to the workflow.

### Step 3: Systematic Test Case Derivation

Test case derivation has two orthogonal dimensions: **coverage targets** (what must be covered) and **design techniques** (how to derive the cases). Apply both.

#### 3A. Coverage Targets (what must be covered)

Every item in the following targets must map to at least one test case:

**From Functional Design**:
- **ACs**: each AC assigned to this unit (happy path and at least one failure path)
- **BRs**: each business rule's full branch space
- **INVs**: each domain invariant
- **Error Paths**: each thrown/returned error has a triggering test

**From NFR Requirements / NFR Design**:
- **NFRs**: each NFR with a quantitative target for this unit
- **Resilience patterns** (introduced by NFR Design): each pattern has observable-behavior tests
  - Circuit breaker: closed → open (after N failures), open → half-open (after timeout), half-open → closed (after success)
  - Retry: retries only on retryable errors, respects max attempts, applies backoff
  - Cache: hit, miss, invalidation, stale-while-revalidate if configured
  - Rate limiter: allow under threshold, reject above threshold, token replenishment
  - Fallback: fallback path triggered on dependency failure
  - Bulkhead / timeout: configured limits enforced

**From Infrastructure Design**:
- **Infrastructure behaviors**: each observable behavior of chosen primitives has a test
  - Conditional writes (optimistic lock) → concurrent update conflict test
  - Queue ordering / at-least-once → idempotency test
  - Connection timeout / retry → timeout recovery test
  - Transactional boundary → partial failure rollback test

**From Application Design / Test Strategy**:
- **Contracts**: each cross-unit interface this unit produces or consumes (per `unit-test-ownership.md`)

Completeness is verified by `coverage-claim.md` in Step 7. An AC/BR/INV/NFR/resilience-pattern/infrastructure-behavior/contract without at least one TC reference is a coverage gap that must either be filled or explicitly declared in Known Gaps with mitigation.

#### 3B. Design Techniques (how to derive the cases)

For each target above, apply the techniques that fit:

- **Equivalence Partitioning**: identify input classes; one representative per class
- **Boundary Value Analysis**: for every numeric/ordered input, test at min, min+1, nominal, max-1, max, and invalid just beyond boundaries
- **Decision Table**: for business rules with multiple conditions, enumerate condition combinations; collapse impossible combinations
- **State Transition**: for entities with lifecycle, test every legal transition + representative illegal transitions
- **Scenario-Based**: each AC drives at least one narrative scenario (happy + failure)
- **Property-Based**: identify invariants (INVs) suitable for property testing (optional per test-strategy.md)
- **Negative Path**: specifically construct inputs that should be rejected; verify rejection mode

Technique choice is documented per test case in the `Technique` field (see Step 4).

#### 3C. Minimum derivation checklist

- [ ] Every AC assigned to this unit has a scenario-based happy case and at least one failure case
- [ ] Every BR with >1 condition has a decision-table case set
- [ ] Every numeric/ordered input has boundary-value cases
- [ ] Every entity lifecycle has state-transition cases for each legal transition, plus representative illegal transitions
- [ ] Every INV has a property-based case OR an explicit waiver (per `common-waiver.md`) if property testing is not viable
- [ ] Every NFR with a numeric target has a measurement case
- [ ] Every produced/consumed contract has a contract test reference (CT-nnn)

### Step 4: Generate Test Case Specification

Create `aidlc-docs/construction/{unit-name}/test-design/test-cases.md`:

```markdown
## Test Case TC-{unit}-{nnn}
- **Layer**: Unit / Integration / Contract / E2E
- **Derived From**: BR-012 / AC-007 / INV-003 / NFR-002
- **Technique**: Boundary / Decision Table row 4 / State transition PENDING->APPROVED / Property
- **Preconditions**: ...
- **Input**: ...
- **Expected Observable Outcome**: ...
- **Failure Mode If Missing**: [what production bug would ship if this test did not exist]
```

**The "Failure Mode If Missing" field is mandatory.** If you cannot name a concrete production bug this test prevents, the test is noise. Delete it.

### Step 5: Test Double Strategy (Per Collaborator)

Create `aidlc-docs/construction/{unit-name}/test-design/test-doubles.md`:

For every collaborator crossing the unit boundary, specify exactly one approach:

```markdown
| Collaborator      | Approach | Rationale                                                    | Contract Anchor          |
|-------------------|----------|--------------------------------------------------------------|--------------------------|
| PaymentGateway    | Fake     | External vendor; in-process hand-rolled fake for speed       | CT-042 (Pact)            |
| Clock             | Stub     | Owned abstraction; stub returns fixed instant                | N/A (owned)              |
| UserRepository    | Fake     | In-memory impl; faster than real DB, exercises full protocol | N/A (owned)              |
| EmailSender       | Mock     | Side-effect-only call; interaction verification is the point | IT-017 (real SMTP smoke) |
| OrderValidator    | Real     | Pure function, no reason to replace                          | -                        |
```

**Principles** (enforced by `common-test-quality.md` Test Double Principles):
- Prefer state verification over interaction verification. Mocks only when the call itself is the observable outcome.
- Replace only at architectural seams. Never replace value objects, DTOs, or pure functions.
- Every double replacing a collaborator you do not control must have a contract anchor (CT-/IT- reference).
- Doubles replacing owned collaborators do not need an external anchor.

**Common mistake to avoid**: "Real (in-memory impl)" is not a separate category. An in-memory implementation of a real interface IS a fake. Use the Fake label.

### Step 6: Test Data Plan

Create `aidlc-docs/construction/{unit-name}/test-design/test-data.md`:

- Fixture catalog (named, minimal, purpose-built)
- Factory patterns for object construction (no giant setUp blocks)
- Sensitive data handling (follow `test-strategy.md` Test Data Strategy)
- Test data cleanup strategy (per-test isolation)

### Step 7: Coverage Claim

Create `aidlc-docs/construction/{unit-name}/test-design/coverage-claim.md`:

```markdown
## AC Coverage
- AC-007: TC-order-012 (happy), TC-order-013 (invalid amount)
- AC-008: TC-order-014 (state transition), TC-order-015 (concurrent update)

## Business Rule Coverage
- BR-012: TC-order-012, TC-order-016, TC-order-017 (full decision table)

## Invariant Coverage
- INV-003: property test TC-order-018

## NFR Coverage
- NFR-002 (p95 latency < 200ms): load test TC-order-perf-001

## Resilience Pattern Coverage (from NFR Design)
- Circuit breaker on PaymentGateway: TC-order-021 (opens after 5 failures), TC-order-022 (half-open recovery)
- Retry on transient DB error: TC-order-023 (retries on retryable), TC-order-024 (does not retry on 4xx)
- Cache on product catalog: TC-order-025 (hit), TC-order-026 (invalidation on update)

## Infrastructure Behavior Coverage (from Infrastructure Design)
- DynamoDB optimistic lock: TC-order-030 (concurrent update conflict returns 409)
- SQS at-least-once: TC-order-031 (idempotent handler on duplicate message)
- HTTP client timeout: TC-order-032 (timeout triggers circuit breaker)

## Contract Coverage (cross-unit)
- Produces contract auth.v1.verify: CT-007
- Consumes contract billing.v2.charge: CT-012

## Known Gaps and Justification
- BR-015 edge case "leap second during renewal": not automated; low probability, detected by monitoring alert ALT-007
- AC-019: manual test only; justified by one-time migration scenario; waiver WAV-019
- Chaos test for regional failover: deferred to E2E chaos suite (owned by platform team); tracked in ticket INFRA-234
```

Gaps must be listed explicitly with mitigation (monitoring alert, waiver ID, owning ticket). Undocumented gaps are hidden risk.

### Step 8: Apply Pre-Write Validation (MANDATORY)

Before writing any artifact to disk, apply the `common-test-quality.md` Pre-Write Validation Checklist to every test case. Reject and regenerate failures.

### Step 9: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# 🧪 Test Design Complete - [unit-name]
```

     2. **AI Summary** (optional): Provide structured bullet-point summary of test design
        - Format: "Test design has derived [description]:"
        - List counts: N test cases, M test doubles with K contract anchors (bullet points)
        - List coverage: ACs / BRs / INVs / NFRs mapped to test cases
        - Mention known gaps flagged and conformance check result
        - DO NOT include workflow instructions ("please review", "let me know", "proceed to next phase", "before we proceed")
        - Keep factual and content-focused
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**  
> Please examine test design at: `aidlc-docs/construction/[unit-name]/test-design/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the test design based on your review  
> ✅ **Continue to Next Stage** - Approve test design and proceed to **[NFR Design / Infrastructure Design / Code Generation]**

---
```

### Step 10: Wait for Explicit Approval and Record
- Do not proceed until the user explicitly approves the test design
- Approval must be clear and unambiguous
- If user requests changes, update the design and repeat the approval process
- Log approval prompt and user response in `audit.md` with ISO 8601 timestamp
- Mark Test Design stage complete for this unit in `aidlc-state.md`

---

## Amendment Protocol (For Code Generation Use)

Test Design's output (`test-cases.md`) is the source of truth that Code Generation consumes. However, Code Generation often uncovers missing cases: concurrency edges, error branches not anticipated in design, integration points discovered at coding time.

When Code Generation identifies a gap:

### Rule 1: Amend, do not silently add

Code Generation MUST NOT write a test that does not trace to an entry in `test-cases.md`. Orphan tests are caught by the drift check in `construction-code-generation.md` Step 13a.

### Rule 2: Amendment is lightweight, not a round-trip

Code Generation amends `test-cases.md` in-place, adding new TC-{unit}-nnn entries with:

```markdown
## Test Case TC-{unit}-{nnn}
- **Layer**: ...
- **Derived From**: ...
- **Source**: amended-during-codegen (not from original Test Design)
- **Amendment Reason**: [one-sentence: what gap was discovered]
- ...rest of fields as usual...
```

The `Source: amended-during-codegen` tag distinguishes amendments from original design.

### Rule 3: Amendments trigger a small user-approval burst

After amendments, Code Generation:

1. Pauses after the affected step
2. Lists amendments added in a compact message:
   ```
   Test Design was amended during Code Generation:
   - TC-order-023 (NEW): concurrency race on cart update
   - TC-order-024 (NEW): retry-after-timeout error branch

   Reason: discovered while implementing update flow.
   Proceed with implementation?
   ```
3. Waits for user approval of the amendment batch
4. On approval: continue; log in `audit.md`
5. On rejection: either remove amendments (and the feature they covered) or return to Test Design for proper redesign

### Rule 4: Rate limit on amendments

If amendments exceed **10%** of original test case count for a unit, that is a signal the Test Design was insufficient. Stop amending and return to Test Design for a proper redesign round.

The tighter threshold (compared to earlier drafts) reflects the new workflow position: Test Design now runs after all design stages, so it has full visibility into what must be tested. Systematic shortfall at this position almost always indicates one of:

- A design stage produced an output that Test Design failed to load (workflow defect — fix loading)
- An amendment protocol is being used to work around a real Test Design gap (return to Test Design)
- The unit is materially more complex than anticipated (split the unit)

One-off amendments (edge cases discovered at coding time) are still expected and welcome. Systemic shortfall is not.

### Rule 5: Amendments update `coverage-claim.md`

If an amendment adds coverage of a previously-declared gap in `coverage-claim.md`, update the Known Gaps section to remove or reduce that gap. Keep the claim in sync with reality.

---

## Critical Rules

- **Test design follows all design stages.** Functional, NFR, and Infrastructure Design must all be complete (or explicitly skipped) before Test Design runs. This is how full coverage is guaranteed.
- **Test design precedes test code.** Code Generation consumes `test-cases.md`; it does not invent tests.
- **Every test traces to a failure mode.** No "test the getter returns the value we set" noise.
- **Test doubles are architectural decisions, not convenience.** Document each one and anchor every mock.
- **Gaps are declared, not hidden.** `coverage-claim.md` is a contract with the reviewer.
- **Untestable design is a defect — return to the responsible design stage.** Functional / NFR / Infrastructure Design each own their own testability; Test Design's job is to catch violations, not fix them in place.
- **One unit, one test design.** Do not split a unit's tests across multiple ad-hoc specs.
- **Resilience and infrastructure behaviors are test targets.** Circuit breakers, retries, caches, queue semantics, optimistic locks — each of these introduces behavior that the suite must verify.

---

## Completion Criteria

- Testability conformance check passed or waiver filed per `common-waiver.md`
- Every AC/BR/INV/NFR assigned to this unit has at least one test case
- Every mock has a contract anchor
- `coverage-claim.md` is complete with explicit gap list
- All five artifacts written: `test-cases.md`, `test-doubles.md`, `test-data.md`, `coverage-claim.md`, `test-design-conformance.md`
- Pre-Write Validation Checklist passed
- User explicit approval recorded

## Artifacts Generated

| File                         | Purpose                                                          |
|------------------------------|------------------------------------------------------------------|
| `test-cases.md`              | Test case specification (TC-{unit}-nnn)                          |
| `test-doubles.md`            | Per-collaborator test double approach with contract anchors      |
| `test-data.md`               | Fixture catalog, factory patterns, sensitive data handling       |
| `coverage-claim.md`          | AC/BR/INV/NFR coverage with declared gaps                        |
| `test-design-conformance.md` | TCON-nnn conformance result (per Step 2); waiver refs if any     |
