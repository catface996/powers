---
name: "aidlc"
displayName: "AI-DLC (AI-Driven Development Life Cycle)"
description: "Intelligent software development workflow that adapts to your needs with three phases: Inception (requirements & design), Construction (implementation & testing), and Operations (deployment). Maintains quality standards while keeping you in control."
keywords: ["aidlc", "ai-dlc", "software development", "workflow", "sdlc", "requirements", "design", "implementation", "testing", "adaptive workflow"]
author: "AWS"
---

# AI-DLC (AI-Driven Development Life Cycle)

AI-DLC is an intelligent software development workflow that adapts to your needs, maintains quality standards, and keeps you in control of the process.

---

## MANDATORY FIRST STEP: Language Selection

**CRITICAL**: You MUST ask user to select language BEFORE any other interaction. This is NON-NEGOTIABLE.

When user activates AI-DLC, you MUST first display this prompt:

```
AI-DLC Power activated.

Please select your preferred language / 请选择您的首选语言:

► **A** - English
  _All conversations and generated documents will be in English_

► **B** - 中文
  _所有对话和生成的文档都将使用中文_

---
Reply with "A" or "B" / 请回复 "A" 或 "B"
```

**WAIT for user response before proceeding.**

**Do NOT load core-workflow.md until language is selected.**
**Do NOT display welcome message until language is selected.**
**Do NOT proceed with ANY workflow steps until language is confirmed.**

Once language is selected:
1. Record the selection in `aidlc-docs/aidlc-state.md`
2. Use the selected language for ALL subsequent outputs
3. **THEN** load `steering/core-workflow.md` and proceed with the workflow

---

## Overview

AI-DLC provides a structured approach to software development with three adaptive phases:

- **Inception** - Requirements gathering and design (WHAT to build and WHY)
- **Construction** - Implementation and testing (HOW to build it)
- **Operations** - Deployment and monitoring (future expansion)

## Activation Trigger

When user starts any request with:
```
Using AI-DLC, [describe your software development need]
```

## Steering Files

All steering files are in the `steering/` directory:

- `core-workflow.md` - Main workflow (load AFTER language selection is complete)
- `common-*.md` - Shared rules (process overview, content validation, question format, etc.)
- `inception-*.md` - Inception phase rules
- `construction-*.md` - Construction phase rules
- `operations-*.md` - Operations phase rules

## Additional Resources

- **Blog**: [AI-Driven Development Life Cycle](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- **Method Definition Paper**: [AI-DLC Methodology](https://prod.d13rzhkk8cj2z0.amplifyapp.com/)
- **GitHub Repository**: [aidlc-workflows](https://github.com/aws-samples/aidlc-workflows)
