# Question Format Guide

## CRITICAL RULE: One Question at a Time

**NEVER ask multiple questions in a single response.** Each interaction must focus on ONE question only.

---

## Standard Question Format

### English Format:
```
**Question: [Topic]**

**Context**: [Brief explanation - why this matters for the project]

**Options:**

► **A** - [First option]
  _Impact: [What choosing this means]_

► **B** - [Second option]
  _Impact: [What choosing this means]_

► **C** - [Third option]
  _Impact: [What choosing this means]_

► **Other** - Provide your own answer

---
Your choice:
```

### Chinese Format:
```
**问题: [主题]**

**背景**: [简要说明 - 为什么这对项目很重要]

**选项:**

► **A** - [第一个选项]
  _影响: [选择这个意味着什么]_

► **B** - [第二个选项]
  _影响: [选择这个意味着什么]_

► **C** - [第三个选项]
  _影响: [选择这个意味着什么]_

► **其他** - 提供您自己的答案

---
您的选择:
```

---

## Question Guidelines

### Option Count
- Minimum: 2 options + "Other"
- Maximum: 4 options + "Other"
- Only include meaningful, realistic options
- **"Other" is ALWAYS the last option**

### Option Quality
- Make options mutually exclusive
- Be specific and actionable
- Include impact descriptions
- Cover common scenarios

### Good Example:

```
**Question: Authentication Method**

**Context**: This determines how users will log into your application.

**Options:**

► **A** - Email + Password
  _Impact: Simple to implement, requires password reset flow_

► **B** - OAuth2 (Google/GitHub)
  _Impact: Better UX, depends on third-party services_

► **C** - Both email and OAuth2
  _Impact: Maximum flexibility, more implementation work_

► **Other** - Provide your own answer

---
Your choice:
```

### Bad Example (Avoid):

```
What authentication do you want? (A/B/C/D/E)

A) Yes
B) No
C) Maybe
D) All of the above
E) None of the above
```

**Problems**: No context, meaningless options, no impact descriptions, multiple questions implied.

---

## User Response Handling

### Valid Responses
- Single letter: "A", "B", "C"
- Letter with explanation: "A - I prefer simple authentication"
- "Other" with custom answer: "Other - I want biometric authentication"

### After Receiving Response
1. Acknowledge the choice briefly
2. If "Other", confirm understanding of custom answer
3. Proceed to next question OR next stage
4. **NEVER ask follow-up questions in the same response**

---

## Stage Transition After Questions

When all questions for a stage are answered:

```
**[Stage Name] Complete**

[Brief summary of decisions made]

**Key decisions:**
- [Decision 1]
- [Decision 2]

---
Ready to proceed to **[Next Stage]**?

► **A** - Yes, continue
► **B** - Request changes

Your choice:
```

---

## Clarification Questions

If user's answer is ambiguous, ask ONE clarification:

```
**Clarification needed**

**Your response**: "[User's original answer]"

**I need to confirm**: [Specific point of confusion]

**Options:**

► **A** - [Interpretation 1]
  _This means: [Explanation]_

► **B** - [Interpretation 2]
  _This means: [Explanation]_

---
Which interpretation is correct?
```

---

## Prohibited Behaviors

| ❌ DON'T | ✅ DO |
|----------|-------|
| Ask multiple questions at once | ONE question per response |
| Use yes/no without context | Provide meaningful options |
| Skip impact descriptions | Explain what each choice means |
| Assume answers | Wait for explicit response |
| Proceed without acknowledgment | Confirm understanding first |
| Create question files | Ask directly in conversation |

---

## Summary

**Remember:**
- ✅ ONE question at a time
- ✅ Always provide context
- ✅ Always include impact descriptions
- ✅ Always include "Other" as last option
- ✅ Always wait for response
- ✅ Use ► symbol for visual clarity
- ✅ Use italic for impact descriptions
- ❌ Never dump multiple questions
- ❌ Never proceed without answer
- ❌ Never assume user intent
