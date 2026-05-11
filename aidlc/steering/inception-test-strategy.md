# Test Strategy (System-Level)

**Purpose**: Establish a single, system-wide testing strategy before any unit-level work begins.

**Why this stage exists**: Testing strategy is an architectural decision, not an implementation detail. Deferring it to per-unit Construction produces fragmented test approaches, inconsistent mocking, duplicated integration test infrastructure, and broken traceability from requirements to tests. This stage fixes the strategy once, so every downstream unit inherits it.

**Position in workflow**: Inception phase. Executes after Application Design, before Units Generation. If Units Generation is skipped, executes before the first Construction stage.

---

## Prerequisites

- Requirements Analysis must be complete
- User Stories recommended (if executed, AC IDs are required inputs)
- Application Design recommended (component seams inform testability constraints)

## When to Execute (CONDITIONAL)

**MANDATORY Execute IF any of**:
- System decomposes into multiple units (contract/integration boundaries exist)
- Any NFR has quantitative targets (performance, availability, security)
- Regulated domain (finance, healthcare, public sector, safety-critical)
- Brownfield project with existing test suite that must coexist
- Public or customer-facing API

**LIKELY Execute IF**:
- Multiple personas with different acceptance criteria
- State management or long-lived workflows
- External integrations (third-party APIs, message queues)

**SKIP ONLY IF**:
- Single-file change with zero behavior change
- Documentation-only update
- Internal tooling with no correctness requirements

**Default to execute when in doubt.** Skipping this stage is a claim that the strategy is obvious - rarely true in practice.

---

## Execution Steps

### Step 1: Load Context
- `aidlc-docs/inception/requirements/requirements.md`
- `aidlc-docs/inception/user-stories/stories.md` (if executed)
- `aidlc-docs/inception/application-design/components.md` (if executed)
- `aidlc-docs/inception/application-design/testability-review.md` (if executed)
- For brownfield:
  - `aidlc-docs/inception/reverse-engineering/code-quality-assessment.md` (existing coverage, test tooling, flakiness)
  - `aidlc-docs/inception/reverse-engineering/technology-stack.md` (test framework constraints)

### Step 2: Build Initial Traceability Skeleton (Layer-Free)

Enumerate every requirement, story, and AC into a single matrix. **Leave test layer columns blank** — layer assignment happens in Step 5 after the user has answered pyramid/layer questions in Step 3.

Output: `aidlc-docs/inception/test-strategy/traceability-matrix.md` (initial version):

```markdown
| Req ID | Story ID | AC ID  | AC Summary (GWT)     | Primary Test Layer | Secondary Layer | Owning Unit | Status   |
|--------|----------|--------|----------------------|--------------------|-----------------|-------------|----------|
| R-01   | S-003    | AC-007 | coupon discount...   | TBD                | TBD             | TBD         | Pending  |
```

Completeness check at this step (only):
- No AC is missing from the matrix
- Every AC has a stable AC-nnn ID
- Every AC is in GWT format

If any AC fails these checks, return to User Stories Step 4a (AC Quality Gate) rather than continue. Layer assignment is premature on defective ACs.

### Step 3: Generate Context-Appropriate Questions

Create `aidlc-docs/inception/test-strategy/test-strategy-questions.md` following `common-question-format-guide.md`.

**Question categories to evaluate** (consider ALL; ask whenever unclear):

- **Test Pyramid Shape** - target ratio of unit : integration : contract : E2E
- **Coverage Targets** - line, branch, mutation; per layer; gate thresholds
- **Test Data Strategy** - synthetic, anonymized production snapshot, fixtures, factories, sensitive data handling
- **Test Environment Strategy** - in-memory, containerized dependencies, shared staging, ephemeral per-PR
- **Contract Test Approach** - consumer-driven (Pact-style), provider-driven, schema-only, none
- **External Dependency Policy** - real, containerized, mocked, sandboxed (per dependency type)
- **Non-Functional Test Coverage** - which NFRs get automated performance / security / chaos / availability tests
- **Regression Policy** - full suite on every commit, selective, nightly
- **Flaky Test Policy** - detection threshold, quarantine process, fix-or-delete SLA
- **TDD vs Test-After** - project default; exceptions rule
- **Accessibility / i18n / Compatibility** - if user-facing
- **Security Testing Depth** - SAST, DAST, dependency scan, pen test, none
- **Test Ownership** - who owns unit/integration/contract/E2E/non-functional tests

### Step 4: Collect and Analyze Answers

Wait for all [Answer]: tags. Apply ambiguity detection per `common-overconfidence-prevention.md`. Follow-up file: `test-strategy-clarification-questions.md`.

**Critical ambiguity triggers** (always follow up):
- "appropriate coverage", "standard practice", "typical", "reasonable"
- Target without a number
- "depends on" without stated decision criteria
- "best practice" without which specific practice

Do not proceed with any unresolved ambiguity.

### Step 5: Generate Test Strategy Artifacts

Create under `aidlc-docs/inception/test-strategy/`:

#### 5.1 `test-strategy.md`

```markdown
# Test Strategy

## Test Pyramid
- Unit: [X]% of total tests, target coverage line [Y]% / branch [Z]%
- Integration: [X]% ...
- Contract: ...
- E2E: ...
- Non-functional: ...

Rationale: [why this shape fits this system - not an industry default]

## Quality Gates (enforced in Build & Test)
- Unit line coverage >= [X]%, branch >= [Y]%
- Mutation score >= [Z]% (if mutation testing enabled)
- All critical-path ACs covered by >=1 automated test
- Zero known-flaky tests on main
- Test suite runtime <= [W] minutes on CI
- [Additional gates as decided]

**Anchor ranges for typical projects** (use as starting point; override with project-specific rationale):

| Metric                          | Low bar (risk flag)  | Typical          | High bar (regulated/critical) |
|---------------------------------|----------------------|------------------|-------------------------------|
| Unit line coverage              | < 60%                | 70-85%           | > 85%                         |
| Unit branch coverage            | < 50%                | 60-80%           | > 80%                         |
| Mutation score (when enabled)   | < 40%                | 50-70%           | > 70%                         |
| Full suite runtime (CI)         | > 30 min             | 10-20 min        | < 10 min (or parallelized)    |
| E2E suite runtime               | > 60 min             | 15-30 min        | < 15 min                      |
| Flaky tests on main             | > 1                  | 0                | 0 (hard gate)                 |
| AC automated coverage (critical)| < 90%                | 95-100%          | 100%                          |

**How to use**:
- If user does not answer specific thresholds, propose typical values as defaults.
- If user answers below "low bar", flag the risk and require explicit justification (log in `audit.md`).
- "High bar" is the default for regulated domains (finance, healthcare, safety-critical).

## Test Environment Topology
[Diagram + description: what runs where, lifecycle, ownership]

## Test Data Strategy
- Source: [synthetic / anonymized / fixture]
- Generation: [factory library, seed scripts]
- Sensitive data: [policy]
- Cleanup: [per-test isolation strategy]

## External Dependencies
| Dependency   | Test Approach          | Rationale                              |
|--------------|------------------------|----------------------------------------|
| Payment API  | Sandbox + contract     | Vendor provides sandbox                |
| Internal auth| Containerized          | Owned; fast startup                    |

## Cross-Unit Testing
- Contract test framework: [choice]
- Integration test ownership: [which unit owns which scenario]
- Shared test harness location: [path]

## Regression and CI Policy
- Trigger: [on every PR / nightly / release]
- Parallelization: [strategy]
- Time budget: [target]
- Failure policy: [block merge / warn / advisory]

## Flaky Test Policy
- Detection: [mechanism]
- Quarantine: [threshold and process]
- Fix SLA: [e.g., 3 business days]
- Delete rule: [when to stop fighting]

## TDD Policy
- Default: [TDD / test-after]
- Exceptions: [explicit list]
- Enforcement: [how verified]

## Non-Functional Test Coverage
| NFR Category    | Automated? | Tool       | Frequency     |
|-----------------|------------|------------|---------------|
| Performance     | Yes        | k6         | nightly       |
| Security (SAST) | Yes        | [tool]     | every PR      |
| Availability    | Manual     | -          | per release   |
```

#### 5.2 `test-types-matrix.md`

Catalog of every test type used in the project: what it covers, tool choice, location, who runs it, when.

#### 5.3 `traceability-matrix.md` (Finalized)

Take the layer-free skeleton from Step 2 and fill in:
- **Primary Test Layer** (Unit / Integration / Contract / E2E / Manual) - based on user's Step 3 answers about pyramid and layer responsibilities
- **Secondary Layer** (if any) - for ACs that warrant defense in depth
- **Owning Unit** - if Units Generation has not yet executed, fill as "TBD - assign after Units Generation"; revisit when units exist
- **Status** - "Assigned" once layer and unit are set

Completeness check at this step:
- No AC has layers still "TBD"
- No AC has "Manual" as the only layer unless waiver WAV-nnn is created (per `common-waiver.md`)
- Every AC that maps to an NFR target has a test layer capable of measuring that NFR

#### 5.4 `test-environments.md`

Concrete environment definitions: name, purpose, composition, lifecycle, access, data source.

#### 5.5 `testability-constraints.md`

Constraints that downstream design stages must honor. These are inputs to Functional Design, NFR Design, Infrastructure Design, Test Design (conformance check), and Code Generation:

```markdown
# Testability Constraints

Constraint TCON-01: All external calls go through injectable ports.
  Rationale: Contract tests require swappable implementations.

Constraint TCON-02: No static singletons in domain layer.
  Rationale: Test isolation requires per-test state.

Constraint TCON-03: Time is injected via a Clock port.
  Rationale: Determinism in time-sensitive tests.

Constraint TCON-04: All ID generation goes through an injectable ID provider.
  Rationale: Deterministic assertions on generated IDs.

[... more constraints as needed]
```

**ID scheme**: Testability constraints use the `TCON-nnn` prefix (zero-padded 2-3 digits). This prefix is distinct from:
- `TC-nnn` (Test Case, scoped per-unit: `TC-{unit}-nnn`)
- `CT-nnn` (Contract Test)
- `IT-nnn` (Integration Test)

Never reuse IDs. Deviations require a waiver (see `common-waiver.md`).

Code Generation MUST refuse to produce code that violates these constraints without explicit waiver.

### Step 6: Testability Feedback Loop (MANDATORY)

If test strategy reveals the current Application Design cannot support the chosen strategy (e.g., strategy requires contract tests but components have no stable interfaces), **return to Application Design**. Document the reason in `audit.md`.

This is a feature, not a bug: catching untestable design in Inception is cheap; catching it in Construction is not.

### Step 7: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:
- Mark Test Strategy complete
- Record that `testability-constraints.md` is now a mandatory input for:
  - Application Design (if re-executed)
  - Functional Design (per-unit)
  - NFR Design (per-unit)
  - Code Generation (per-unit)

### Step 8: Present Completion Message
- Present completion message in this structure:
     1. **Completion Announcement** (mandatory): Always start with this:

```markdown
# 🧪 Test Strategy Complete
```

     2. **AI Summary** (optional): Provide structured bullet-point summary of test strategy
        - Format: "Test strategy has established [description]:"
        - List test pyramid shape and coverage targets (bullet points)
        - List key policies (flaky, TDD, regression, environment)
        - Mention traceability matrix completeness and testability constraints published
        - DO NOT include workflow instructions ("please review", "let me know", "proceed to next phase", "before we proceed")
        - Keep factual and content-focused
     3. **Formatted Workflow Message** (mandatory): Always end with this exact format:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**  
> Please examine the test strategy at: `aidlc-docs/inception/test-strategy/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the test strategy based on your review  
> ✅ **Approve & Continue** - Approve strategy and proceed to **[Units Generation / next stage]**

---
```

### Step 9: Wait for Explicit Approval and Log
- Do not proceed until the user explicitly approves the test strategy
- Approval must be clear and unambiguous
- If user requests changes, update the strategy and repeat the approval process
- Log approval prompt and user response in `audit.md` with ISO 8601 timestamp
- Mark Test Strategy stage complete in `aidlc-state.md`

---

## Critical Rules

- **One strategy, one system.** Do not allow per-unit re-negotiation of pyramid, coverage, or mocking policy.
- **Every AC routes to a test layer.** No exceptions without explicit justification in the traceability matrix.
- **Measurable targets or no target.** "Reasonable performance" is not a requirement.
- **Testability is a design constraint, not an aspiration.** If the design cannot host the strategy, the design is wrong.
- **Mocks require contract anchors.** Strategy defines where anchors live; per-unit Test Design consumes the strategy.
- **Regenerate, do not patch.** If strategy artifacts fail the traceability/measurability checks, fix at source (Requirements / Stories / NFR), do not paper over in strategy.

---

## Anti-Patterns This Stage Prevents

- Per-unit mock strategies that contradict each other
- "Coverage" being a number without a definition of what it measures
- Integration tests that duplicate unit tests at higher cost
- E2E-only test suites that take hours to run
- Performance requirements with no test plan attached
- Contract tests invented ad-hoc when the first integration breaks
- Flaky tests tolerated as "normal"
- NFRs that ship as slogans

---

## Completion Criteria

- Traceability matrix covers every AC
- Every NFR with a quantitative target has a corresponding test type in `test-types-matrix.md`
- Testability constraints published and acknowledged as inputs to downstream stages
- Quality gates numeric and measurable
- User explicit approval recorded
