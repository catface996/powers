# Test Quality Rules (Cross-Cutting)

**Purpose**: Rules that apply to every test, at every layer, in every unit.

**Scope**: This file defines *quality criteria* for tests. It does NOT define *what to test* (see `construction-test-design.md`) or *system-wide strategy* (see `inception-test-strategy.md`).

## Integration With Other Files

- Loaded alongside `common-content-validation.md` whenever test artifacts or test code are generated
- Defines the **Failure-Mode-First Principle** and **Pre-Write Validation Checklist** that all downstream stages apply
- Consumed by `construction-test-design.md` for per-unit test case derivation
- Consumed by `construction-code-generation.md` when test code is produced
- Enforced by `construction-build-and-test.md` as quality gate criteria
- Parameters (coverage thresholds, flaky SLA, TDD policy) come from `inception-test-strategy.md`
- Waivers for rule exceptions follow `common-waiver.md`

## When to Load

- Before writing any test artifact to disk (test-cases.md, test-doubles.md, test code files)
- During Test Design stage execution
- During Code Generation when test code is being produced
- During Build and Test quality gate evaluation

---

## Core Principle: Failure-Mode-First

**For every test, answer: "What production bug would ship if this test did not exist?"**

- If the answer is "none" or "I don't know", the test is noise. Delete.
- If the answer is "a bug that another test already catches", the test is duplicate. Delete.
- If the answer is a concrete bug, document it in the test case spec (see `construction-test-design.md` Step 4 "Failure Mode If Missing" field).

This principle drives all other rules below. A test that cannot justify its existence by the bug it prevents has no business in the suite.

---

## Test Independence

- **No ordering dependencies.** A test must pass in isolation, in reverse order, and in parallel.
- **No shared mutable state between tests.** Each test constructs its world from scratch.
- **No implicit global setup** beyond framework bootstrap. Shared setup must be explicit and per-test-scoped.

## Determinism

Rules are written for **new unit and integration tests**. E2E and brownfield tests have explicit, documented exceptions.

### Rules (new unit and integration tests)

- **No `sleep`-based waits.** Use explicit synchronization: polling with timeout, event subscription, latch, framework wait primitives.
- **No real wall clock.** Inject a clock abstraction. Tests never depend on "now".
- **No real randomness.** Seed generators explicitly. Prefer property-based frameworks with deterministic shrinking.
- **No real network.**
- **No real filesystem** beyond temp dirs scoped to the test.

A test that passes 99 times and fails once is not a passing test. It is a failing test with a coverage gap in its own determinism.

### Documented exceptions

**E2E tests** may use real clock, real network, real filesystem, and real randomness when the behavior under test specifically involves them (session expiry, cookie TTL, scheduled jobs, real DNS resolution). Each exception must be:
- Scoped to the E2E layer only; never leak the pattern into unit/integration layers
- Documented in the test file comment header with rationale
- Compensated by deterministic assertions (e.g., use wall clock to wait, but assert on a deterministic observable outcome, not on the clock value)

**Brownfield legacy tests** (see Legacy Test Boundary below) may retain existing non-deterministic patterns during a transitional period. They must be tracked in `test-debt.md` and cannot be added to — any new test must comply with the rules above.

### Absolute prohibitions (no exceptions, no waivers)

- **Retry-until-pass loops** in tests or CI config that mask flakiness
- **Silent skips** based on environment (e.g., `if (isCI) { return }`)
- **Commented-out asserts** left in committed code

## Legacy Test Boundary (Brownfield)

Brownfield projects typically inherit test suites that violate the rules above. Zero-day compliance is unrealistic and a forced rewrite campaign usually destroys more value than it creates.

**Rule set for brownfield**:

1. **New tests** (added or significantly modified) MUST comply with all rules in this file.
2. **Legacy tests** retain the right to exist. They are inventoried in `aidlc-docs/construction/build-and-test/test-debt.md`:
   ```markdown
   | Test                                | Violation(s)                | Planned action         | Target date |
   |-------------------------------------|-----------------------------|------------------------|-------------|
   | OrderServiceTest.processesPayment   | real wall clock, sleep(500) | Refactor with Clock port| 2026-Q4     |
   ```
3. **Legacy tests do not block the quality gate** on structural smell — but they DO block the gate if flaky (flakiness is fixed, not waived; see Flaky Tests below).
4. **No regression**: a legacy test that is modified becomes a new test and must comply with current rules.
5. **Opportunistic cleanup**: when a test file is touched for any reason, remediate its legacy violations in the same commit if feasible.

This boundary is enforced in Build and Test Phase B quality gate:
- New tests failing rules -> fail gate
- Legacy tests failing rules but listed in `test-debt.md` -> pass gate
- Tests failing rules and NOT in `test-debt.md` -> fail gate (add to debt inventory or fix)

## Naming and Intent

- Test name describes **behavior under conditions**, not method name.
  - CORRECT: `refund_fails_when_order_already_refunded`
  - WRONG: `testRefund`, `test_refund_1`, `refundTest`
- Test body follows **Arrange-Act-Assert** (or Given-When-Then). One act per test.
- One logical assertion per test. Multiple physical asserts are acceptable only if they verify one behavior.
- **Parameterized tests** must have deterministic and readable names per case. `test[0]`, `test[1]` is insufficient; use a format like `test[input=NEGATIVE]`, `test[input=ZERO]`, `test[input=MAX]`.

## Test Double Principles

The choice of test double is not a ranked preference. It is a trade-off between **what you verify** and **cost of maintenance**.

### Principle 1: Prefer state verification over interaction verification

- **State verification**: arrange, act, then assert on observable state (return values, queries, emitted events). Favors fakes, stubs, and real collaborators.
- **Interaction verification**: arrange, act, then assert on which methods were called with which arguments. Favors mocks and spies.

State verification produces less brittle tests because it does not couple to internal call sequences. Use interaction verification only when the call itself is the observable outcome (e.g., "an email was sent", "a metric was emitted").

### Principle 2: Choose the double that minimizes brittleness for the target observation

| Double type | What it provides                          | Good for                                         | Poor for                                |
|-------------|-------------------------------------------|--------------------------------------------------|-----------------------------------------|
| Real        | Actual production implementation          | Fast, deterministic real collaborators           | Slow, network-bound, non-deterministic  |
| Fake        | Working shortcut impl (e.g., in-memory DB)| Complex contracts where stubbing is tedious      | Trivial collaborators                   |
| Stub        | Pre-programmed responses, no verification | Returning canned data to drive the SUT           | Verifying side-effect-only calls        |
| Mock        | Stub + interaction verification           | Side-effect-only calls (email, metrics, events)  | State-based collaborators               |
| Spy         | Wraps a real object, records calls        | Partial real behavior + interaction observation  | When a fake is viable                   |

### Principle 3: Only replace at architectural seams

- Mock/fake/stub **at ownership boundaries only**. Never replace types you own and can exercise directly.
- Never replace value objects, DTOs, or pure functions. Use the real thing.

### Principle 4: Every non-real double must have a contract anchor

Every fake, stub, mock, or spy replacing a collaborator **you do not control** (external API, shared service, vendor SDK) must have a contract anchor: another test somewhere in the suite that pins the doubled behavior to reality (a contract test, a real-integration test, or a documented vendor-sandbox test).

**Unpinned doubles are lies.** They produce green tests while production drifts from assumption.

Doubles replacing owned collaborators do not need an external anchor — the real implementation's own tests anchor them.

### Principle 5: Never hand-roll what the framework provides

If the framework has ergonomic mocks/stubs, use them. Hand-rolled test doubles that reimplement framework features add maintenance burden without benefit.

### Principle 6: Avoid over-specified interaction verification

When using mocks, verify the smallest set of interactions required for the behavior. Avoid:

- Strict ordering (`inOrder`) unless the order is the contract itself
- Exact call counts (`times(1)`) unless the count is semantic (e.g., idempotency)
- Argument matchers that lock down implementation details

Over-specified mocks break on legitimate refactoring and give false confidence.

## Forbidden Test Smells

| Smell | Definition | Remediation |
|-------|------------|-------------|
| Assertion Roulette | Many asserts, unclear which failed | Split into named tests |
| Mystery Guest | Test depends on external file/DB/env not visible in the test | Move dependency into test |
| Eager Test | Verifies multiple behaviors at once | Split per behavior |
| Conditional Logic in Tests | `if`/`switch` inside a test | Two tests, not one |
| Production Logic Duplication | Test recomputes what production does | Assert concrete expected value |
| Happy-Path Only | No failure-case tests for non-trivial code | Add failure-mode tests |
| Comment-Driven Asserts | `// TODO: assert something here` | Write the assertion or delete the test |
| Snapshot Overreliance | Snapshots without review process | Review discipline or delete snapshot |
| Sleep-Based Sync | `sleep(N)` to wait for async | Explicit wait primitive |
| Testing the Framework | Assertions that verify library behavior | Delete |
| Irrelevant Information | Setup data unrelated to the test | Use minimal fixture |
| Reflection-Based Access | Using reflection to read/write private state | Refactor production to expose observable state, or remove the test |
| Over-Specified Mocks | Strict ordering/counts/matchers not required by contract | Relax to semantic verification |
| Private-Method Unit Testing | Testing methods the caller cannot see | Test through the public surface, or make the method public |

Any of these in generated test artifacts requires regeneration, not a style fix.

## Flaky Tests

- A test that fails intermittently is **worse than no test**. It trains teams to ignore failures.
- **Detection**: any test that fails on retry within a 30-day window is flaky.
- **Action**: quarantine immediately; fix within the SLA defined in Test Strategy; delete if unfixable.
- **Never**: retry-until-pass in CI without a tracking ticket that names the root cause.
- **Flakiness is fixed, not waived.** Waivers per `common-waiver.md` do NOT cover flaky tests.

## Coverage Discipline

- **Line coverage is a floor, not a ceiling.** 80% line coverage with no branch coverage is weak evidence.
- Prefer **mutation score** over line coverage when tooling permits. It measures whether tests would actually catch bugs.
- Coverage drops require explicit justification in the PR description.
- **Never** game coverage by writing assertion-free tests.
- Coverage claims live in `coverage-claim.md` per unit (see `construction-test-design.md`).

## Test Code Quality

Test code is production code. It receives the same discipline:

- Same review standards
- Same refactoring cadence
- Naming standards equal to or stricter than production
- DAMP over DRY in tests: readability beats minimal duplication
- Builders and factories for object construction are encouraged
- Helper functions that hide assertions are forbidden

## Speed Budget

Default budgets (override in Test Strategy):

- Unit tests: <100ms per test, <60s total for the unit
- Integration tests: <5s per test
- Contract tests: <2s per test
- E2E: explicit budget in Test Strategy

Tests exceeding budget require either justification or reclassification to a slower layer.

---

## Pre-Write Validation Checklist

Apply to every test artifact and every generated test code file before writing to disk:

### Intent and traceability
- [ ] Every test traces to an AC ID, BR ID, INV ID, or NFR ID
- [ ] Every test answers the Failure-Mode-First question with a concrete production bug

### Structure
- [ ] AAA / GWT structure visible
- [ ] Name describes behavior under conditions
- [ ] Parameterized cases have deterministic, readable names
- [ ] One act per test; one logical assertion per test

### Determinism
- [ ] No `sleep`, no real time, no real randomness, no real network, no real filesystem (except explicit contract/E2E layer with documented rationale)
- [ ] No retry-until-pass loops
- [ ] No environment-conditional skips

### Coverage
- [ ] Failure-mode cases exist, not only happy path
- [ ] Boundary values covered for numeric/ordered inputs
- [ ] Error paths have triggering tests

### Test doubles
- [ ] Every non-real double replacing a collaborator you do not control has a contract anchor (CT-/IT- or documented waiver)
- [ ] No mocks of value objects, DTOs, or pure functions
- [ ] No mocks of owned types exercised directly in other tests
- [ ] Mock interaction verification is not over-specified (no unnecessary strict ordering, counts, or matchers)

### Isolation
- [ ] No test depends on another test's side effects
- [ ] No shared mutable state between tests
- [ ] No reflection-based access to private state

### Budget and smells
- [ ] Speed budget respected (or justified and reclassified)
- [ ] No forbidden smell from the Forbidden Test Smells table

**Failing any checklist item is not a style issue - it is a correctness risk. Reject the artifact and regenerate.** For items that genuinely cannot be satisfied, file a waiver per `common-waiver.md` rather than silently proceeding.
