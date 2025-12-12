# AI-DLC Welcome Message

**Purpose**: This file contains brief welcome messages. Display ONLY when user explicitly asks about AI-DLC.

**IMPORTANT**: Do NOT display this automatically. The interaction protocol handles the initial flow.

---

## ENGLISH VERSION

Use this ONLY if user asks "What is AI-DLC?" or "How does this work?":

```
**AI-DLC** (AI-Driven Development Life Cycle) is an adaptive software development workflow.

**Three Phases:**

► **INCEPTION** - Understanding what to build and why
  _Requirements, user stories, architecture planning_

► **CONSTRUCTION** - Designing and implementing the solution
  _Detailed design, code generation, testing_

► **OPERATIONS** - Deployment and monitoring (future)
  _Placeholder for future expansion_

**Key Features:**
- Adapts to your project's complexity
- Skips unnecessary steps for simple changes
- Provides full coverage for complex projects
- Documents all decisions in audit trail

---
What would you like to build?
```

---

## CHINESE VERSION

Use this ONLY if user selected Chinese AND asks "AI-DLC 是什么？" or "这是如何工作的？":

```
**AI-DLC**（AI 驱动开发生命周期）是一个自适应的软件开发工作流。

**三个阶段：**

► **初始阶段** - 理解要构建什么以及为什么
  _需求、用户故事、架构规划_

► **构建阶段** - 设计和实现解决方案
  _详细设计、代码生成、测试_

► **运维阶段** - 部署和监控（未来）
  _未来扩展的占位符_

**主要特点：**
- 根据项目复杂度自适应调整
- 简单更改跳过不必要的步骤
- 复杂项目提供完整覆盖
- 在审计追踪中记录所有决策

---
您想要构建什么？
```

---

# DO NOT USE

The following detailed explanations should NOT be shown automatically. They are reference material only.

## Phase Details (Reference Only)

### INCEPTION PHASE
- Workspace Detection (ALWAYS)
- Reverse Engineering (CONDITIONAL - Brownfield only)
- Requirements Analysis (ALWAYS - Adaptive depth)
- User Stories (CONDITIONAL)
- Workflow Planning (ALWAYS)
- Application Design (CONDITIONAL)
- Units Generation (CONDITIONAL)

### CONSTRUCTION PHASE
- Functional Design (CONDITIONAL, per-unit)
- NFR Requirements (CONDITIONAL, per-unit)
- NFR Design (CONDITIONAL, per-unit)
- Infrastructure Design (CONDITIONAL, per-unit)
- Code Generation (ALWAYS, per-unit)
- Build and Test (ALWAYS)

### OPERATIONS PHASE
- Operations (PLACEHOLDER)

**Remember**: Reveal this information progressively, stage by stage, NOT all at once.
