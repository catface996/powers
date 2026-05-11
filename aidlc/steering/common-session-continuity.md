# Session Continuity Templates

## Welcome Back Prompt Template
When a user returns to continue work on an existing AI-DLC project, present this prompt:

```markdown
**Welcome back! I can see you have an existing AI-DLC project in progress.**

Based on your aidlc-state.md, here's your current status:
- **Project**: [project-name]
- **Current Phase**: [INCEPTION/CONSTRUCTION/OPERATIONS]
- **Current Stage**: [Stage Name]
- **Last Completed**: [Last completed step]
- **Next Step**: [Next step to work on]

**What would you like to work on today?**

A) Continue where you left off ([Next step description])
B) Review a previous stage ([Show available stages])

[Answer]: 
```

## MANDATORY: Session Continuity Instructions
1. **Always read aidlc-state.md first** when detecting existing project
2. **Parse current status** from the workflow file to populate the prompt
3. **MANDATORY: Load Previous Stage Artifacts** - Before resuming any stage, automatically read all relevant artifacts from previous stages:
   - **Reverse Engineering**: Read architecture.md, code-structure.md, api-documentation.md, code-quality-assessment.md (test asset inventory)
   - **Requirements Analysis**: Read requirements.md, requirement-verification-questions.md
   - **User Stories**: Read stories.md (with AC-nnn IDs in GWT format), personas.md, story-generation-plan.md
   - **Application Design**: Read application-design artifacts (components.md, component-methods.md, services.md, testability-review.md)
   - **Test Strategy**: Read test-strategy.md, traceability-matrix.md, test-types-matrix.md, test-environments.md, testability-constraints.md
   - **Design (Units)**: Read unit-of-work.md, unit-of-work-dependency.md, unit-of-work-story-map.md
   - **Per-Unit Design**: Read functional-design.md (with BR-/INV- IDs), nfr-requirements.md (with NFR- IDs), nfr-design.md, infrastructure-design.md
   - **Per-Unit Test Design**: Read test-cases.md, test-doubles.md, test-data.md, coverage-claim.md
   - **Code Stages**: Read all code files, plans, AND all previous artifacts (including test artifacts)
4. **Smart Context Loading by Stage**:
   - **Early Stages (Workspace Detection, Reverse Engineering)**: Load workspace analysis
   - **Requirements/Stories**: Load reverse engineering + requirements artifacts
   - **Test Strategy**: Load requirements + stories + application design + reverse engineering test assets (if brownfield)
   - **Design Stages**: Load requirements + stories + architecture + design artifacts + testability-constraints.md (if Test Strategy executed)
   - **Test Design**: Load test-strategy + testability-constraints + functional-design + nfr-requirements + nfr-design + infrastructure-design + story-to-AC mapping for this unit (Test Design runs after all design stages and needs every upstream output)
   - **Code Stages**: Load ALL artifacts + test artifacts + existing code files
5. **Adapt options** based on architectural choice and current phase
6. **Show specific next steps** rather than generic descriptions
7. **Log the continuity prompt** in audit.md with timestamp
8. **Context Summary**: After loading artifacts, provide brief summary of what was loaded for user awareness
9. **Asking questions**: ALWAYS ask clarification or user feedback questions by placing them in .md files. DO NOT place the multiple-choice questions in-line in the chat session.

## Error Handling
If artifacts are missing or corrupted during session resumption, see [error-handling.md](error-handling.md) for guidance on recovery procedures. 