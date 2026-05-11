# Build and Test (Quality Gate)

**Purpose**: Build all units, execute the full test suite, and enforce the quality gates defined in Test Strategy. This stage is a **go/no-go decision point**, not a descriptive summary. Its output determines whether the system is eligible to proceed to Operations.

**Structure**: Two distinct phases with different natures:
- **Phase A: Specification Generation** — Produce human/CI-readable instruction documents (build, test execution, environment setup). Descriptive.
- **Phase B: Quality Gate Execution** — Evaluate measured results against gate thresholds. Produces a go/no-go decision.

Do not mix these phases. Phase A documents what CAN be done; Phase B decides whether what WAS done is acceptable.

## Prerequisites
- Code Generation must be complete for all units
- All code artifacts must be generated and per-unit tests passing locally
- Test Strategy executed (if applicable) — provides the quality gate thresholds
- Per-unit Test Design artifacts available (if applicable) — provide coverage claims and test double anchors

---

## Step 1: Load Gate Criteria

Load the criteria that define pass/fail for this stage:

- `aidlc-docs/inception/test-strategy/test-strategy.md` — quality gate thresholds (coverage, mutation, flakiness, speed budget)
- `aidlc-docs/inception/test-strategy/traceability-matrix.md` — every AC must map to an executed, passing test
- `aidlc-docs/construction/{unit-name}/test-design/coverage-claim.md` for every unit — declared coverage with gaps
- `aidlc-docs/waivers/INDEX.md` — active waivers that modify gate interpretation
- `common-test-quality.md` — structural test quality rules
- `common-waiver.md` — how to handle proposed waivers for gate failures

If Test Strategy was skipped, use defaults from `common-test-quality.md` (Speed Budget, Coverage Discipline) as minimum gates.

Enumerate every gate that will be checked in Phase B and publish the list in `build-and-test-summary.md`.

---

## Step 2: Analyze Test Layers Present

For each layer below, identify whether it exists in this project and what pass/fail criteria apply:
- **Unit tests**: Already generated per unit during code generation. Must pass; must meet coverage gate.
- **Integration tests**: Test interactions between units/services. Must pass.
- **Contract tests**: API contract validation between services. Must pass if units participate in contracts.
- **Performance tests**: Load, stress, scalability. Must meet NFR thresholds if NFRs had quantitative targets.
- **End-to-end tests**: Complete user workflows. Must pass.
- **Security tests**: SAST, DAST, dependency scan, per Test Strategy.

Layers not present in the project are documented as "N/A" with reason, never silently skipped.

---

# PHASE A: Specification Generation

**Purpose**: Produce reusable instruction documents that describe HOW to build and test the system. These are consumed by CI systems, onboarding developers, and operators. They are descriptive, not gate-enforcing.

## Step A1: Generate Build Instructions

Create `aidlc-docs/construction/build-and-test/build-instructions.md`:

```markdown
# Build Instructions

## Prerequisites
- **Build Tool**: [Tool name and version]
- **Dependencies**: [List all required dependencies]
- **Environment Variables**: [List required env vars]
- **System Requirements**: [OS, memory, disk space]

## Build Steps

### 1. Install Dependencies
\`\`\`bash
[Command to install dependencies]
# Example: npm install, mvn dependency:resolve, pip install -r requirements.txt
\`\`\`

### 2. Configure Environment
\`\`\`bash
[Commands to set up environment]
# Example: export variables, configure credentials
\`\`\`

### 3. Build All Units
\`\`\`bash
[Command to build all units]
# Example: mvn clean install, npm run build, brazil-build
\`\`\`

### 4. Verify Build Success
- **Expected Output**: [Describe successful build output]
- **Build Artifacts**: [List generated artifacts and locations]
- **Common Warnings**: [Note any acceptable warnings]

## Troubleshooting

### Build Fails with Dependency Errors
- **Cause**: [Common causes]
- **Solution**: [Step-by-step fix]

### Build Fails with Compilation Errors
- **Cause**: [Common causes]
- **Solution**: [Step-by-step fix]
```

## Step A2: Generate Unit Test Execution Instructions

Create `aidlc-docs/construction/build-and-test/unit-test-instructions.md`:

```markdown
# Unit Test Execution

## Run Unit Tests

### 1. Execute All Unit Tests
\`\`\`bash
[Command to run all unit tests]
# Example: mvn test, npm test, pytest tests/unit
\`\`\`

### 2. Review Test Results
- **Expected**: [X] tests pass, 0 failures
- **Test Coverage**: [Expected coverage percentage - cite gate from test-strategy.md]
- **Test Report Location**: [Path to test reports]

### 3. Fix Failing Tests
If tests fail:
1. Review test output in [location]
2. Identify failing test cases
3. Fix code issues
4. Rerun tests until all pass
```

## Step A3: Generate Integration Test Instructions

Create `aidlc-docs/construction/build-and-test/integration-test-instructions.md`:

```markdown
# Integration Test Instructions

## Purpose
Test interactions between units/services to ensure they work together correctly.

## Test Scenarios

### Scenario 1: [Unit A] -> [Unit B] Integration
- **Description**: [What is being tested]
- **Setup**: [Required test environment setup]
- **Test Steps**: [Step-by-step test execution]
- **Expected Results**: [What should happen]
- **Cleanup**: [How to clean up after test]

### Scenario 2: [Unit B] -> [Unit C] Integration
[Similar structure]

## Setup Integration Test Environment

### 1. Start Required Services
\`\`\`bash
[Commands to start services]
# Example: docker-compose up, start test database
\`\`\`

### 2. Configure Service Endpoints
\`\`\`bash
[Commands to configure endpoints]
# Example: export API_URL=http://localhost:8080
\`\`\`

## Run Integration Tests

### 1. Execute Integration Test Suite
\`\`\`bash
[Command to run integration tests]
# Example: mvn integration-test, npm run test:integration
\`\`\`

### 2. Verify Service Interactions
- **Test Scenarios**: [List key integration test scenarios]
- **Expected Results**: [Describe expected outcomes]
- **Logs Location**: [Where to check logs]

### 3. Cleanup
\`\`\`bash
[Commands to clean up test environment]
# Example: docker-compose down, stop test services
\`\`\`
```

## Step A4: Generate Performance Test Instructions (If Applicable)

Create `aidlc-docs/construction/build-and-test/performance-test-instructions.md`:

```markdown
# Performance Test Instructions

## Purpose
Validate system performance under load to ensure it meets NFR thresholds.

## Performance Requirements (from NFR-nnn)
- **Response Time**: < [X]ms for [Y]% of requests (NFR-nnn)
- **Throughput**: [X] requests/second (NFR-nnn)
- **Concurrent Users**: Support [X] concurrent users (NFR-nnn)
- **Error Rate**: < [X]%

## Setup Performance Test Environment

### 1. Prepare Test Environment
\`\`\`bash
[Commands to set up performance testing]
# Example: scale services, configure load balancers
\`\`\`

### 2. Configure Test Parameters
- **Test Duration**: [X] minutes
- **Ramp-up Time**: [X] seconds
- **Virtual Users**: [X] users

## Run Performance Tests

### 1. Execute Load Tests
\`\`\`bash
[Command to run load tests]
# Example: jmeter -n -t test.jmx, k6 run script.js
\`\`\`

### 2. Execute Stress Tests
\`\`\`bash
[Command to run stress tests]
# Example: gradually increase load until failure
\`\`\`

### 3. Analyze Performance Results
- **Response Time**: [Actual vs NFR target]
- **Throughput**: [Actual vs NFR target]
- **Error Rate**: [Actual vs NFR target]
- **Bottlenecks**: [Identified bottlenecks]
- **Results Location**: [Path to performance reports]
```

## Step A5: Generate Additional Test Instructions (As Needed)

Based on Test Strategy's test-types-matrix, generate additional instruction files:

### Contract Tests (For Microservices / Cross-Service APIs)
Create `aidlc-docs/construction/build-and-test/contract-test-instructions.md`:
- API contract validation between services
- Consumer-driven contract testing
- Schema validation

### Security Tests
Create `aidlc-docs/construction/build-and-test/security-test-instructions.md`:
- Vulnerability scanning (SAST / DAST)
- Dependency security checks
- Authentication/authorization testing
- Input validation testing

### End-to-End Tests
Create `aidlc-docs/construction/build-and-test/e2e-test-instructions.md`:
- Complete user workflow testing
- Cross-service scenarios
- UI testing (if applicable)

---

# PHASE B: Quality Gate Execution

**Purpose**: Evaluate measured results against gate thresholds. Produce a go/no-go decision. This is not documentation — it is a verdict.

## Step B1: Execute or Load Test Results

For each layer identified in Step 2, obtain measured results:
- Either execute the tests now (if this stage runs end-to-end)
- Or load results from the most recent CI run (referenced by run ID and timestamp)

Record:
- Pass/fail count per layer
- Coverage (line, branch, and mutation if enabled) per layer
- Runtime per suite
- Flaky test detections from this run
- Performance test metrics (p50, p95, p99, throughput, error rate) vs NFR targets
- Security scan findings by severity

## Step B2: Quality Gate Verification (MANDATORY)

Evaluate every gate identified in Step 1 against Step B1 measurements.

Create `aidlc-docs/construction/build-and-test/quality-gate-report.md`:

```markdown
# Quality Gate Report

**Test Run ID**: [CI run identifier or local execution timestamp]
**Evaluation Date**: [ISO timestamp]

## Gate Evaluation

| Gate                              | Threshold       | Actual         | Status   | Waiver    |
|-----------------------------------|-----------------|----------------|----------|-----------|
| Unit line coverage                | >= 80%          | 84.2%          | PASS     | -         |
| Unit branch coverage              | >= 70%          | 65.1%          | FAIL     | WAV-007   |
| Mutation score                    | >= 60%          | N/A            | SKIPPED  | -         |
| Flaky tests on main               | 0               | 2              | FAIL     | -         |
| Full suite runtime                | <= 15 min       | 11 min         | PASS     | -         |
| AC coverage (traceability)        | 100% critical   | 98%            | FAIL     | -         |
| NFR-002 p95 latency               | < 200ms @ 1kRPS | 178ms          | PASS     | -         |
| SAST scan                         | no high/crit    | 1 high         | FAIL     | -         |

## Failed Gates Without Waivers
[List every FAIL gate without an active waiver. These block progression.]

For each:
- **Gate**: [name]
- **Actual vs threshold**: [numbers]
- **Root cause**: [one-line diagnosis]
- **Responsible stage to return to**: [Code Generation / Test Design / Functional Design / Test Strategy]

## Active Waivers Applied
[List every FAIL gate that is covered by an active waiver]

For each:
- **Waiver ID**: WAV-nnn
- **Gate**: [name]
- **Review date**: [date]
- **Owner**: [name]

## Flaky Test Inventory
[List every flaky test detected during this run with failure rate]

Per `common-test-quality.md`, flakiness is fixed, not waived. A flaky test gate failure without an already-quarantined status is ALWAYS a hard fail.

## Coverage Drift
[Comparison to previous baseline if brownfield; note any unexplained drops]

## Overall Decision
**Status**: GO / NO-GO
**Rationale**: [one-sentence]

- **GO**: all gates PASS, or all FAIL gates covered by active, non-expired waivers
- **NO-GO**: any gate FAIL without a covering active waiver
```

**Critical rules**:
1. Any FAIL gate without a covering waiver blocks progression to Operations.
2. Waivers follow `common-waiver.md`. AI proposes; user approves. AI never applies waivers on its own authority.
3. Expired waivers do not count as covering.
4. Flaky test failures require fixing, not waiving (per `common-test-quality.md`).

## Step B3: Propose Waivers for Gate Failures (IF NEEDED)

For each failed gate without an existing active waiver, AI may propose a waiver per `common-waiver.md`:

1. Draft `aidlc-docs/waivers/WAV-{next-id}.md.draft`
2. Present the draft to the user with rationale
3. Wait for explicit approval or rejection
4. On approval: activate; on rejection: return to the responsible stage for fix

Do NOT proceed past the gate without either a clean pass or an approved waiver.

---

# PHASE C: Reporting and Handoff

## Step C1: Generate Test Summary

Create `aidlc-docs/construction/build-and-test/build-and-test-summary.md`:

```markdown
# Build and Test Summary

## Build Status
- **Build Tool**: [Tool name]
- **Build Status**: [Success/Failed]
- **Build Artifacts**: [List artifacts]
- **Build Time**: [Duration]

## Test Execution Summary

### Unit Tests
- **Total Tests**: [X]
- **Passed**: [X] / Failed: [X]
- **Coverage (line/branch/mutation)**: [L%/B%/M%]
- **Status**: [Pass/Fail]

### Integration Tests
- **Test Scenarios**: [X]
- **Passed**: [X] / Failed: [X]
- **Status**: [Pass/Fail]

### Contract Tests
- **Contracts verified**: [X]/[Y] ([% pass])
- **Status**: [Pass/Fail/N/A]

### Performance Tests (NFR Verification)
- **NFR-nnn (latency)**: [Actual] (Target: [Expected]) - [Pass/Fail]
- **NFR-nnn (throughput)**: [Actual] (Target: [Expected]) - [Pass/Fail]
- **Error Rate**: [Actual] (Target: [Expected]) - [Pass/Fail]

### Security Tests
- **SAST**: [findings by severity]
- **DAST**: [findings by severity]
- **Dependency scan**: [findings by severity]
- **Status**: [Pass/Fail/N/A]

### E2E Tests
- **Journeys tested**: [X]/[Y]
- **Status**: [Pass/Fail/N/A]

## Overall Status
- **Build**: [Success/Failed]
- **All Tests**: [Pass/Fail]
- **Quality Gates**: [All Pass / N Failed — see quality-gate-report.md]
- **Active Waivers Applied**: [list of WAV-nnn with gate names]
- **Ready for Operations**: [Yes/No — driven by Quality Gate Report Overall Decision]

## Traceability Completeness
- **ACs with passing test evidence**: [X / Y]
- **Unmapped ACs (no test evidence)**: [list of AC IDs]
- **NFRs with measured verification**: [X / Y]
- **Testability constraints honored**: [X / Y] (from testability-constraints.md TCON-nnn list)

## Flakiness Report
- **New flaky tests this run**: [count and list]
- **Existing quarantined tests**: [count and list]
- **Quarantine SLA status**: [on track / breached per test-strategy.md SLA]

## Next Steps
[If all gates pass or are waived]: Ready to proceed to Operations phase for deployment planning
[If any gate fails without waiver]: Block progression. Return to [responsible stage per quality-gate-report.md] and fix.
```

## Step C2: Update State Tracking

Update `aidlc-docs/aidlc-state.md`:
- Mark Build and Test stage as complete IF quality gate decision is GO
- If NO-GO, mark as "gated - fix required" and record which stage must be revisited
- Update current status

## Step C3: Present Results to User

```
"Build and Test Complete — Quality Gate [GO / NO-GO]

Build Status: [Success/Failed]

Test Results:
- Unit Tests: [X]/[Y] passed, coverage line [L]% / branch [B]%
- Integration Tests: [X]/[Y] scenarios passed
- Contract Tests: [Status]
- Performance Tests: [summary vs NFR targets]
- Security Tests: [summary by severity]
- E2E Tests: [Status]

Quality Gates ([P] pass / [F] fail / [W] waived):
[List each gate with PASS/FAIL/WAIVED-BY-WAV-nnn]

Traceability:
- ACs covered: [X]/[Y]
- Unmapped ACs: [list or 'none']
- NFRs verified: [X]/[Y]

Flakiness:
- New flaky tests this run: [count]
- SLA status: [on track / breached]

Waivers applied: [list of WAV-nnn or 'none']

Generated Files:
1. build-instructions.md
2. unit-test-instructions.md
3. integration-test-instructions.md
4. performance-test-instructions.md (if applicable)
5. contract-test-instructions.md (if applicable)
6. security-test-instructions.md (if applicable)
7. e2e-test-instructions.md (if applicable)
8. quality-gate-report.md
9. build-and-test-summary.md

Review the gate report at: aidlc-docs/construction/build-and-test/quality-gate-report.md

[If GO]: Ready to proceed to Operations stage for deployment planning?
[If NO-GO]: Quality gate FAILED. Return to [responsible stage] to fix, or propose waiver with justification per common-waiver.md."
```

## Step C4: Log Interaction

**MANDATORY**: Log the phase completion in `aidlc-docs/audit.md`:

```markdown
## Build and Test Stage
**Timestamp**: [ISO timestamp]
**Build Status**: [Success/Failed]
**Test Status**: [Pass/Fail per layer]
**Quality Gate Decision**: [GO/NO-GO]
**Waivers Applied**: [list of WAV-nnn]
**Files Generated**:
- build-instructions.md
- unit-test-instructions.md
- integration-test-instructions.md
- performance-test-instructions.md
- quality-gate-report.md
- build-and-test-summary.md

---
```

---

## Critical Rules

- **Phase A and Phase B are distinct**. Do not conflate documentation generation with gate enforcement.
- **Gate failures block progression by default**. Waivers are explicit, approved, and time-bound per `common-waiver.md`.
- **Flakiness is fixed, not waived**.
- **Every NFR with a measurable target must have a measured result in Phase B**. Missing measurement is a gate failure.
- **Traceability completeness is a gate**. Unmapped ACs or missing NFR verification fails the stage.
- **Waivers have expiry**. Expired waivers do not count as covering.
