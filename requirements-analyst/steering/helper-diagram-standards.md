---
inclusion: agent
---

# Diagram and Documentation Standards

This document defines the mandatory standards for UML diagrams and documentation format in requirements analysis.

---

## Expression Priority (FUNDAMENTAL RULE)

**ALWAYS follow this priority when expressing requirements:**

```
1st Priority: Diagram (Visual representation)
    └── 2nd Priority: UML Diagram (Standard notation)
        └── 3rd Priority: Mermaid Syntax (Generation method)
```

### Priority Matrix

| Expression Method | Priority | Usage |
|-------------------|----------|-------|
| **UML Diagram (Mermaid)** | 🥇 Highest | Default choice - ALWAYS use first |
| **Other Diagrams (Mermaid)** | 🥈 Second | When UML type not applicable |
| **Table + Diagram** | 🥉 Third | Supplementary details only |
| **Text/Table only** | ❌ Avoid | Only when diagram is impossible |

### UML Diagram Selection Guide

| Requirement Type | UML Diagram | Mermaid Type |
|------------------|-------------|--------------|
| System interactions | Use Case Diagram | `graph TB` with actors |
| **Process flow** | **Activity Diagram** | **`stateDiagram-v2`** |
| Time-based interactions | Sequence Diagram | `sequenceDiagram` |
| **Domain model** | **Class Diagram** | **`classDiagram`** |
| **Data model** | **ER Diagram** | **`erDiagram`** |
| State transitions | State Diagram | `stateDiagram-v2` |
| Component structure | Component Diagram | `graph TB` with subgraphs |

> ⚠️ **Class Diagram vs ER Diagram**: Do NOT mix their syntax! See sections 4 and 5 for correct usage.

### Non-UML Diagram Guide

| Visualization Type | Purpose | Mermaid Type |
|--------------------|---------|--------------|
| User Story Map | Release planning matrix | `graph TB` with subgraphs |
| Dependency Graph | Requirement relationships | `graph LR/TD` |
| Traceability | Mapping connections | `graph LR` |
| Mind Map | Brainstorming | `mindmap` |
| Timeline | Milestones | `timeline` |

> **IMPORTANT**: For **user activity flows** and **business processes**, ALWAYS use `stateDiagram-v2` (UML Activity Diagram), NOT `graph` (flowchart).

---

## ⛔ Mermaid Syntax Constraints (MANDATORY)

**CRITICAL**: Mermaid has strict syntax rules. Violating these will cause parse errors.

### Special Characters in Node Text

| Character | Problem | Solution |
|-----------|---------|----------|
| `()` | Parsed as node shape | Use quotes: `["text (note)"]` |
| `[]` | Parsed as node shape | Use quotes: `["text [note]"]` |
| `{}` | Parsed as node shape | Use quotes: `["text {note}"]` |
| `<>` | Parsed as HTML/link | Use quotes or escape: `["text <note>"]` |
| `/` | May cause issues | Use quotes: `["A/B"]` |

### Node Definition Rules

**DO**:
```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
graph TD
    A["External Library (G6/Cytoscape)"]
    B["Config File [JSON]"]
    C["Status {Active}"]

    style A fill:none,stroke:#32FF96,stroke-width:2px,rx:6
    style B fill:none,stroke:#FFFF66,stroke-width:2px,rx:6
    style C fill:none,stroke:#FF6666,stroke-width:2px,rx:6
```

**DO NOT**:
```
graph TD
    A[External Library (G6/Cytoscape)]   ❌ Parse error
    B[Config File [JSON]]                 ❌ Parse error
    C[Status {Active}]                    ❌ Parse error
```

### Text with Line Breaks

**DO**:
```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
graph TD
    A["Line 1<br/>Line 2"]

    style A fill:none,stroke:#32FF96,stroke-width:2px,rx:6
```

**DO NOT**:
```
graph TD
    A[Line 1<br/>(Note)]   ❌ Parentheses cause parse error
```

### Verification Checklist

Before generating ANY Mermaid diagram, verify:
- [ ] All node text with special characters `()[]{}/<>` wrapped in quotes `""`
- [ ] No unescaped parentheses in node labels
- [ ] No unescaped brackets in node labels
- [ ] Line breaks `<br/>` only used inside quoted strings

---

## 1. UML Use Case Diagram Standards

### MANDATORY Rules

- **Actors**: Must use stick figure icon (not rectangles)
- **Use Cases**: Must use ellipse shape
- **System Boundary**: Must use dashed rectangle
- **Relationships**: Must use correct stereotypes
  - `<<include>>`: Mandatory dependency (always executed)
  - `<<extend>>`: Optional extension (conditionally executed)
  - `<<generalize>>`: Inheritance relationship

### ❌ PROHIBITED

- Using simple flowcharts to represent use case diagrams
- Omitting system boundary
- Using incorrect relationship markers

### Mermaid Syntax for Use Case Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
graph TB
    subgraph System["System Boundary"]
        direction TB
        UC1((Use Case 1))
        UC2((Use Case 2))
        UC3((Use Case 3))

        UC1 -->|<<include>>| UC2
        UC1 -.->|<<extend>>| UC3
    end

    Actor1[/"👤 Actor 1"\]
    Actor2[/"👤 Actor 2"\]

    Actor1 --> UC1
    Actor2 --> UC2

    %% Cyclic theme colors, no fill, stroke only
    style UC1 fill:none,stroke:#32FF96,stroke-width:2px
    style UC2 fill:none,stroke:#FFFF66,stroke-width:2px
    style UC3 fill:none,stroke:#FF6666,stroke-width:2px
    style Actor1 fill:none,stroke:#FB00FF,stroke-width:2px
    style Actor2 fill:none,stroke:#902FF0,stroke-width:2px
```

---

## 2. Business Process Standards (Activity Diagram)

### MANDATORY Rules

- **Core user activity flows MUST use UML Activity Diagram**
- **Tables alone are NOT sufficient** - must have accompanying diagram
- **Parallel processing MUST be explicitly marked** using fork/join or `par` syntax
- **Decision points MUST use diamond shape**
- **Start/End MUST use standard notation** (filled circle / bull's eye)

### Activity Diagram Syntax

```mermaid
stateDiagram-v2
    [*] --> Activity1
    Activity1 --> Decision1

    state Decision1 <<choice>>
    Decision1 --> Activity2: [condition A]
    Decision1 --> Activity3: [condition B]

    state ParallelProcessing {
        direction LR
        [*] --> Task1
        [*] --> Task2
        Task1 --> [*]
        Task2 --> [*]
    }

    Activity2 --> ParallelProcessing
    Activity3 --> ParallelProcessing
    ParallelProcessing --> Activity4
    Activity4 --> [*]
```

### Alternative: Flowchart with Swim Lanes

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
flowchart TB
    subgraph User["👤 User"]
        A1[Start Request]
        A4[Receive Result]
    end

    subgraph System["System"]
        A2[Process Request]
        A3[Generate Response]
    end

    A1 --> A2
    A2 --> A3
    A3 --> A4

    %% Cyclic theme colors, no fill, stroke only, rx:6
    style A1 fill:none,stroke:#32FF96,stroke-width:2px,rx:6
    style A2 fill:none,stroke:#FFFF66,stroke-width:2px,rx:6
    style A3 fill:none,stroke:#FF6666,stroke-width:2px,rx:6
    style A4 fill:none,stroke:#FB00FF,stroke-width:2px,rx:6
```

---

## 3. Use Case Main Flow Standards (Sequence Diagram)

### MANDATORY Rules

- **Use Case main flows MUST use Sequence Diagram**
- **Actor-System tables alone are NOT sufficient**
- **All key participants MUST be included**: User, UI, System, Agent, Database, External Services
- **Parallel execution MUST use `par` syntax**
- **Alternative flows use `alt` syntax**
- **Optional flows use `opt` syntax**

### ❌ PROHIBITED

Simple table format like:

| Step | Actor | System |
|------|-------|--------|
| 1 | Action | |
| 2 | | Response |

### ✅ REQUIRED

```mermaid
sequenceDiagram
    autonumber

    actor User as 👤 User
    participant UI as 🖥️ Interface
    participant System as ⚙️ System
    participant Agent as 🤖 Agent
    participant DB as 🗄️ Database

    User->>UI: 1. Initiate Request
    activate UI
    UI->>System: 2. Forward Request
    activate System

    par Parallel Processing
        System->>Agent: 3a. Analyze Request
        Agent-->>System: 3a. Analysis Result
    and
        System->>DB: 3b. Query Data
        DB-->>System: 3b. Return Data
    end

    alt Success
        System-->>UI: 4. Success Response
        UI-->>User: 5. Display Result
    else Failure
        System-->>UI: 4. Error Response
        UI-->>User: 5. Display Error
    end

    deactivate System
    deactivate UI
```

### Sequence Diagram Syntax Reference

| Syntax | Purpose | Example |
|--------|---------|---------|
| `par ... and ... end` | Parallel execution | Concurrent operations |
| `alt ... else ... end` | Alternative flows | Success/failure paths |
| `opt ... end` | Optional flow | Conditional execution |
| `loop ... end` | Repeated execution | Iteration |
| `break ... end` | Exit flow | Exception handling |
| `activate/deactivate` | Lifeline activation | Active processing |

---

## 4. Class Diagram Standards (Domain Model)

### When to Use

- **Domain modeling**: Core business entities and relationships
- **Data structure design**: Object attributes and methods
- **Inheritance hierarchies**: Class specialization

### MANDATORY Rules

- Use `classDiagram` syntax for object relationships
- Define attributes with visibility (`+` public, `-` private, `#` protected)
- Use correct relationship notation

### Class Diagram Syntax

```mermaid
classDiagram
    class ResourceNode {
        +String id
        +String name
        +ResourceType type
        +getStatus() Status
    }

    class ResourceType {
        +String typeName
        +String description
    }

    class Agent {
        +String agentId
        +String version
        +Status status
        +start() void
        +stop() void
    }

    ResourceNode "1" -- "1" ResourceType : has
    ResourceNode "1" -- "0..*" Agent : monitors
    Agent <|-- MonitorAgent : extends
    Agent <|-- CollectorAgent : extends
```

### Relationship Syntax Reference

| Relationship | Syntax | Description |
|--------------|--------|-------------|
| Association | `A -- B` | Basic relationship |
| Association (labeled) | `A "1" -- "0..*" B : has` | With cardinality and label |
| Inheritance | `Parent <\|-- Child` | Generalization |
| Composition | `A *-- B` | Strong ownership (lifecycle bound) |
| Aggregation | `A o-- B` | Weak ownership (independent lifecycle) |
| Dependency | `A ..> B` | Uses relationship |
| Realization | `A ..\|> B` | Interface implementation |

### ⚠️ COMMON MISTAKE

```
❌ WRONG (ER Diagram syntax in Class Diagram):
classDiagram
    ResourceNode ||--|| ResourceType

✅ CORRECT (Class Diagram syntax):
classDiagram
    ResourceNode "1" -- "1" ResourceType : has
```

---

## 5. ER Diagram Standards (Data Model)

### When to Use

- **Database design**: Entity relationships for persistence
- **Data modeling**: Tables and foreign key relationships
- **System integration**: Data exchange structures

### MANDATORY Rules

- Use `erDiagram` syntax for entity relationships
- Define attributes with data types
- Use correct cardinality notation

### ER Diagram Syntax

```mermaid
erDiagram
    RESOURCE_NODE ||--|| RESOURCE_TYPE : has
    RESOURCE_NODE ||--o{ AGENT : monitors
    AGENT ||--o{ METRIC : collects

    RESOURCE_NODE {
        string id PK
        string name
        string type_id FK
        datetime created_at
    }

    RESOURCE_TYPE {
        string id PK
        string type_name
        string description
    }

    AGENT {
        string id PK
        string resource_id FK
        string version
        string status
    }

    METRIC {
        string id PK
        string agent_id FK
        string metric_name
        float value
        datetime timestamp
    }
```

### Cardinality Notation

| Syntax | Meaning |
|--------|---------|
| `\|\|--\|\|` | One to One |
| `\|\|--o{` | One to Many |
| `o{--o{` | Many to Many |
| `\|\|--o\|` | One to Zero or One |
| `}o--o{` | Zero or Many to Zero or Many |

### Comparison: Class Diagram vs ER Diagram

| Aspect | Class Diagram (`classDiagram`) | ER Diagram (`erDiagram`) |
|--------|-------------------------------|--------------------------|
| **Purpose** | Domain/Object modeling | Database/Data modeling |
| **Relationship** | `"1" -- "0..*"` | `\|\|--o{` |
| **Inheritance** | `<\|--` (supported) | Not supported |
| **Methods** | Supported | Not supported |
| **Primary Key** | Not explicit | `PK` notation |
| **Foreign Key** | Not explicit | `FK` notation |

### ⚠️ DO NOT MIX SYNTAX

```
❌ WRONG (mixing syntax):
classDiagram
    A ||--o{ B

❌ WRONG (mixing syntax):
erDiagram
    A <|-- B

✅ CORRECT:
Use classDiagram for OOP relationships
Use erDiagram for database relationships
```

---

## 6. Document Format Standards

### MANDATORY Rules

#### Text Formatting
- **Each analysis item MUST be on a separate line**
- **Key terms MUST be bold**
- **Consistent indentation** throughout document
- **Clear visual hierarchy** with proper heading levels

#### Example - CORRECT Format

```markdown
## Analysis Summary

**User Roles**:
- Operations personnel
- DevOps engineers
- Development engineers

**Core Activities**:
- Resource topology management
- Agent configuration
- Monitoring and inspection
- Problem diagnosis
- Fault handling

**Key Findings**:
- **Finding 1**: Description of first finding
- **Finding 2**: Description of second finding
```

#### Example - INCORRECT Format

```markdown
## Analysis Summary
User Roles: Operations personnel, DevOps engineers, Development engineers
Core Activities: Resource topology management, Agent configuration, Monitoring...
```

---

## 7. Diagram Visual Standards (MANDATORY)

### ⛔ Color and Style Rules (MUST FOLLOW)

**CRITICAL**: All diagrams MUST strictly follow these visual rules.

#### 7.1 Canvas Background

| Property | Value | Description |
|----------|-------|-------------|
| **Background Color** | `#000066` | Dark blue canvas background |

#### 7.2 Stroke Width (Line Thickness)

| Level | Width | Usage |
|-------|-------|-------|
| **Primary** | `3px` | Main elements, key nodes, important connections |
| **Secondary** | `2px` | Supporting elements, standard connections |
| **Tertiary** | `1px` | Minor elements, annotations, subtle connections |

#### 7.3 Fill Style

| Rule | Description |
|------|-------------|
| **NO Background Fill** | Shapes MUST NOT have filled backgrounds |
| **Stroke Only** | Use stroke color only, keep interior transparent |
| **Example** | `fill:none` or `fill:transparent` |

#### 7.4 Rectangle Border Radius

| Property | Value | Description |
|----------|-------|-------------|
| **Border Radius (rx)** | `6` | Rectangle corner radius |
| **❌ PROHIBITED** | `12` | Do NOT use radius of 12 |

#### 7.5 Theme Colors (Cyclic Usage)

**Primary Palette** - Use these colors IN ORDER, cycling through for same-level nodes:

| Order | Color Code | Color Name | Usage |
|-------|------------|------------|-------|
| 1st | `#32FF96` | Neon Green | First element at each level |
| 2nd | `#FFFF66` | Yellow | Second element at each level |
| 3rd | `#FF6666` | Coral Red | Third element at each level |
| 4th | `#FB00FF` | Magenta | Fourth element at each level |
| 5th | `#902FF0` | Purple | Fifth element at each level |

**Cyclic Usage Rule**:
- When there are multiple nodes at the SAME hierarchy level, cycle through colors 1→2→3→4→5→1→2→...
- Example: 6 sibling nodes would use colors: `#32FF96`, `#FFFF66`, `#FF6666`, `#FB00FF`, `#902FF0`, `#32FF96`

### Style Template

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
graph TD
    A[Element 1]
    B[Element 2]
    C[Element 3]
    D[Element 4]
    E[Element 5]
    F[Element 6]

    %% Cyclic color assignment for same-level nodes
    style A fill:none,stroke:#32FF96,stroke-width:3px,rx:6
    style B fill:none,stroke:#FFFF66,stroke-width:3px,rx:6
    style C fill:none,stroke:#FF6666,stroke-width:3px,rx:6
    style D fill:none,stroke:#FB00FF,stroke-width:3px,rx:6
    style E fill:none,stroke:#902FF0,stroke-width:3px,rx:6
    style F fill:none,stroke:#32FF96,stroke-width:3px,rx:6
```

### Hierarchical Example

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'background': '#000066' }}}%%
graph TB
    %% Level 1 - Primary (3px)
    Root[Root Node]

    %% Level 2 - Same level siblings cycle colors
    A[Child A]
    B[Child B]
    C[Child C]

    %% Level 3 - Secondary (2px)
    A1[Sub A1]
    A2[Sub A2]
    B1[Sub B1]

    Root --> A
    Root --> B
    Root --> C
    A --> A1
    A --> A2
    B --> B1

    %% Level 1 styling
    style Root fill:none,stroke:#32FF96,stroke-width:3px,rx:6

    %% Level 2 - cycle through colors
    style A fill:none,stroke:#32FF96,stroke-width:2px,rx:6
    style B fill:none,stroke:#FFFF66,stroke-width:2px,rx:6
    style C fill:none,stroke:#FF6666,stroke-width:2px,rx:6

    %% Level 3 - cycle continues per parent
    style A1 fill:none,stroke:#32FF96,stroke-width:1px,rx:6
    style A2 fill:none,stroke:#FFFF66,stroke-width:1px,rx:6
    style B1 fill:none,stroke:#32FF96,stroke-width:1px,rx:6
```

### Verification Checklist

Before generating ANY diagram, verify:
- [ ] Canvas background set to `#000066`
- [ ] All shapes have `fill:none` (no background fill)
- [ ] Stroke width is `3px`, `2px`, or `1px` based on importance
- [ ] Rectangle border radius is `6` (NOT `12`)
- [ ] Same-level nodes cycle through theme colors in order
- [ ] Theme colors used: `#32FF96` → `#FFFF66` → `#FF6666` → `#FB00FF` → `#902FF0` → repeat

### Other Quality Rules

1. **All UML diagrams MUST follow standard syntax**
2. **Use Mermaid syntax for all diagrams**
3. **Complex processes MUST be decomposed** into multiple diagrams
4. **Each diagram MUST have a clear title**

---

## 8. Diagram Decomposition Guidelines

### When to Decompose

| Condition | Action |
|-----------|--------|
| More than 10 nodes | Split into sub-diagrams |
| Multiple swimlanes (>3) | Create separate diagrams per domain |
| Complex parallel flows | Separate detailed sequence diagram |
| Multiple abstraction levels | Use overview + detail diagrams |

### Decomposition Pattern

```
Overview Diagram (High-level)
    │
    ├── Detail Diagram 1 (Subprocess A)
    ├── Detail Diagram 2 (Subprocess B)
    └── Detail Diagram 3 (Subprocess C)
```

---

## Quick Reference Card

| Element | Standard | Mermaid Syntax |
|---------|----------|----------------|
| Actor | Stick figure | `[/"👤 Name"\]` |
| Use Case | Ellipse | `((Use Case))` |
| Activity | Rectangle | `[Activity]` |
| Decision | Diamond | `{Decision}` or `<<choice>>` |
| Parallel | Fork/Join | `par ... and ... end` |
| System Boundary | Dashed box | `subgraph` |
| Include | Dashed arrow with label | `-->|<<include>>|` |
| Extend | Dashed arrow with label | `-.->|<<extend>>|` |
