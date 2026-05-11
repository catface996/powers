# AI-DLC Terminology Glossary

## Core Terminology

### Phase vs Stage

**Phase**: One of the three high-level lifecycle phases in AI-DLC
- 🔵 **INCEPTION PHASE** - Planning & Architecture (WHAT and WHY)
- 🟢 **CONSTRUCTION PHASE** - Design, Implementation & Test (HOW)
- 🟡 **OPERATIONS PHASE** - Deployment & Monitoring (future expansion)

**Stage**: An individual workflow activity within a phase
- Examples: Context Assessment stage, Requirements Assessment stage, Code Planning stage
- Each stage has specific prerequisites, steps, and outputs
- Stages can be ALWAYS-EXECUTE or CONDITIONAL

**Usage Examples**:
- ✅ "The CONSTRUCTION phase contains 7 stages"
- ✅ "The Code Planning stage is always executed"
- ✅ "We're in the INCEPTION phase, executing the Requirements Assessment stage"
- ❌ "The Requirements Assessment phase" (should be "stage")
- ❌ "The CONSTRUCTION stage" (should be "phase")

## Three-Phase Lifecycle

### INCEPTION PHASE
**Purpose**: Planning and architectural decisions  
**Focus**: Determine WHAT to build and WHY  
**Location**: `inception/` directory

**Stages**:
- Workspace Detection (ALWAYS)
- Reverse Engineering (CONDITIONAL - Brownfield only)
- Requirements Analysis (ALWAYS - Adaptive depth)
- User Stories (CONDITIONAL)
- Workflow Planning (ALWAYS)
- Application Design (CONDITIONAL)
- Design - Units Planning/Generation (CONDITIONAL)

**Outputs**: Requirements, user stories, architectural decisions, unit definitions

### CONSTRUCTION PHASE
**Purpose**: Detailed design and implementation  
**Focus**: Determine HOW to build it  
**Location**: `construction/` directory

**Stages**:
- Functional Design (CONDITIONAL, per-unit)
- NFR Requirements (CONDITIONAL, per-unit)
- NFR Design (CONDITIONAL, per-unit)
- Infrastructure Design (CONDITIONAL, per-unit)
- Code Planning (ALWAYS)
- Code Generation (ALWAYS)
- Build and Test (ALWAYS)

**Outputs**: Design artifacts, NFR implementations, code, tests

### OPERATIONS PHASE
**Purpose**: Deployment and operational readiness  
**Focus**: How to DEPLOY and RUN it  
**Location**: `operations/` directory

**Stages**:
- Operations (PLACEHOLDER)

**Outputs**: Build instructions, deployment guides, monitoring setup, verification procedures

---

## Workflow Stages

### Always-Execute Stages
- **Workspace Detection**: Initial analysis of workspace state and project type
- **Requirements Analysis**: Gathering requirements (depth varies based on complexity)
- **Workflow Planning**: Creating execution plan for which phases to run
- **Code Planning**: Creating detailed implementation plans for code generation
- **Code Generation**: Generating actual code based on plans and prior artifacts
- **Build and Test**: Building all units and executing comprehensive testing

### Conditional Stages
- **Reverse Engineering**: Analyzing existing codebase (brownfield projects only)
- **User Stories**: Creating user stories and personas (includes Story Planning and Story Generation)
- **Application Design**: Designing application components, methods, business rules, and services
- **Design**: Designing system components (includes Units Planning, Units Generation, per-unit design)
- **Functional Design**: Technology-agnostic business logic design (per-unit)
- **NFR Requirements**: Determining NFRs and selecting tech stack (per-unit)
- **NFR Design**: Incorporating NFR patterns and logical components (per-unit)
- **Infrastructure Design**: Mapping to actual infrastructure services (per-unit)

## Application Design Terms

- **Component**: A functional unit with specific responsibilities
- **Method**: A function or operation within a component with defined business rules
- **Business Rule**: Logic that governs method behavior and validation
- **Service**: Orchestration layer that coordinates business logic across components
- **Component Dependency**: Relationship and communication pattern between components

## Architecture Terms (Infrastructure)

### Unit of Work
A logical grouping of user stories for development purposes. The term used during planning and decomposition.

**Usage**: "We need to decompose the system into units of work"

### Service
An independently deployable component in a microservices architecture. Each service is a separate unit of work.

**Usage**: "The Payment Service handles all payment processing"

### Module
A logical grouping of functionality within a single service or monolith. Modules are not independently deployable.

**Usage**: "The authentication module within the User Service"

### Component
A reusable building block within a service or module. Components are classes, functions, or packages that provide specific functionality.

**Usage**: "The EmailValidator component validates email addresses"

## Terminology Guidelines

### When to Use Each Term

**Unit of Work**:
- During Units Planning and Units Generation phases
- When discussing system decomposition
- In planning documents and discussions
- Example: "How should we decompose this into units of work?"

**Service**:
- When referring to independently deployable components
- In microservices architecture contexts
- In deployment and infrastructure discussions
- Example: "The Order Service will be deployed to ECS"

**Module**:
- When referring to logical groupings within a service
- In monolith architecture contexts
- When discussing internal organization
- Example: "The reporting module generates all reports"

**Component**:
- When referring to specific classes, functions, or packages
- In design and implementation discussions
- When discussing reusable building blocks
- Example: "The DatabaseConnection component manages connections"

## Stage Terminology

### Planning vs Generation
- **Planning**: Creating a plan with questions and checkboxes for execution
- **Generation**: Executing the plan to create artifacts

Examples:
- Story Planning → Story Generation
- Units Planning → Units Generation
- Unit Design Planning → Unit Design Generation
- NFR Planning → NFR Generation
- Code Planning → Code Generation

### Depth Levels
- **Minimal**: Quick, focused execution for simple changes
- **Standard**: Normal depth with standard artifacts for typical projects
- **Comprehensive**: Full depth with all artifacts for complex/high-risk projects

## Artifact Types

### Plans
Documents with checkboxes and questions that guide execution.
- Located in `aidlc-docs/plans/`
- Examples: `story-generation-plan.md`, `unit-of-work-plan.md`

### Artifacts
Generated outputs from executing plans.
- Located in various `aidlc-docs/` subdirectories
- Examples: `requirements.md`, `stories.md`, `design.md`

### State Files
Files tracking workflow progress and status.
- `aidlc-state.md`: Overall workflow state
- `audit.md`: Complete audit trail of all interactions

## Testing Terminology

### Test Pyramid
The target distribution of tests across layers, from many fast tests at the bottom (unit) to few slow tests at the top (E2E). Shape is decided in Test Strategy, not per-unit.

### Test Layers
- **Unit Test**: Exercises a single component in isolation. Fast (<100ms). No real network, filesystem, database.
- **Integration Test**: Exercises multiple components together, possibly with real infrastructure (containerized or in-memory).
- **Contract Test**: Verifies the contract between two services. Can be consumer-driven or provider-driven.
- **E2E Test (End-to-End)**: Exercises a full user journey through the deployed system.
- **Non-Functional Tests**: Performance, security, availability, chaos — verify NFRs.

### Test Doubles
Umbrella term for test replacements of real collaborators.
- **Fake**: A working implementation with shortcuts unsuitable for production (e.g., in-memory database).
- **Stub**: Returns pre-programmed responses. No behavior.
- **Mock**: Like a stub, but also verifies the interactions (calls made to it).
- **Spy**: Records interactions for later assertion, often wraps a real object.
- **Dummy**: A placeholder passed but never used.

Choice of double is a trade-off, not a ranking. See `common-test-quality.md` Test Double Principles: prefer state over interaction verification; pick the double that minimizes brittleness for the observation you need.

### Contract Anchor
Any test that pins a mocked collaborator to reality (typically a contract test or real-integration test). **Every mock must have a contract anchor**, or the mock is an unverified assumption.

### Coverage Metrics
- **Line Coverage**: % of source lines executed by tests. Floor, not ceiling.
- **Branch Coverage**: % of decision branches executed. Stronger than line.
- **Mutation Score**: % of injected code mutations detected by tests. Strongest; expensive.

### Flaky Test
A test that fails intermittently with no production change. Treated as worse than no test; see `common-test-quality.md` Flaky Tests policy.

### Traceability Matrix
System-level table mapping Requirement → Story → Acceptance Criterion → Test Layer → Owning Unit. Lives in Test Strategy.

### Testability Constraint
An architectural constraint that downstream design must honor to make the strategy implementable (e.g., "all external calls through injectable ports"). Published in Test Strategy; enforced in Code Generation.

### Stable IDs
Immutable identifiers assigned at creation, never reused:
- **S-nnn**: User Story
- **AC-nnn**: Acceptance Criterion
- **BR-nnn**: Business Rule
- **INV-nnn**: Domain Invariant
- **NFR-nnn**: Non-Functional Requirement
- **TCON-nnn**: Testability Constraint (system-level, in test-strategy)
- **TC-{unit}-nnn**: Test Case (per-unit)
- **CT-nnn**: Contract Test
- **IT-nnn**: Integration Test
- **WAV-nnn**: Waiver (see `common-waiver.md`)

These IDs form the spine of traceability from requirements through tests.

**Important**: `TC-` and `TCON-` are distinct namespaces. `TC-` is always per-unit (e.g., `TC-order-012`). `TCON-` is system-level (e.g., `TCON-03`). Do not abbreviate Testability Constraint as `TC-`.

### TDD vs Test-After
- **TDD (Test-Driven Development)**: Write failing test, then production code to make it pass.
- **Test-After**: Write production code, then tests that cover it atomically (same commit).

AI-DLC supports both. Default is decided in Test Strategy. "Tests never" is not an option.

### Given-When-Then (GWT)
Acceptance criterion format:
```
Given [precondition]
When  [action]
Then  [observable outcome]
```
Mandated in `inception-user-stories.md` Step 4a.

## Common Abbreviations

- **AI-DLC**: AI-Driven Development Life Cycle
- **NFR**: Non-Functional Requirements
- **UOW**: Unit of Work
- **API**: Application Programming Interface
- **CDK**: Cloud Development Kit (AWS)
- **AC**: Acceptance Criterion
- **BR**: Business Rule
- **INV**: Domain Invariant
- **GWT**: Given-When-Then
- **TDD**: Test-Driven Development
- **TCON**: Testability Constraint
- **TC**: Test Case (per-unit)
- **CT**: Contract Test
- **IT**: Integration Test
- **WAV**: Waiver
- **SAST**: Static Application Security Testing
- **DAST**: Dynamic Application Security Testing
