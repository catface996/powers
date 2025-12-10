# Phase 4: Requirements Clarification

## Overview
Transform vague or ambiguous requirements into clear, unambiguous specifications through systematic questioning and validation.

## Objectives
- Eliminate ambiguity in requirements statements
- Clarify assumptions and constraints
- Define clear boundaries and scope
- Establish measurable acceptance criteria

## Clarification Process

### Step 1: Identify Ambiguities
Look for these common ambiguity patterns:
- Vague terms: "user-friendly", "fast", "secure"
- Missing details: "users can login" (which users? how?)
- Unclear scope: "manage products" (create/edit/delete/view?)
- Undefined conditions: "when needed", "if required"

### Step 2: Apply Clarification Rules (MANDATORY)

#### STRICT ENFORCEMENT: One Question at a Time
- **MUST ask only ONE question per response**
- **FORBIDDEN to ask multiple questions in single response**
- **MUST wait for user's answer before proceeding**

#### MANDATORY Priority Order (Top-Down)
**MUST follow this exact sequence:**
1. **Project Context** - What system/product are we working on?
2. **User/Stakeholder** - Who will use this? Who are the stakeholders?
3. **Business Goal** - What business problem are we solving?
4. **Scope Boundary** - What's included/excluded in this requirement?
5. **Functional Details** - How should it work?
6. **Non-functional Requirements** - Performance, security, usability constraints
7. **Edge Cases** - What happens when things go wrong?

#### REQUIRED Question Format
```
[Single focused question]

Why I'm asking: [Brief explanation of why this matters for requirements]
```

### Step 3: Document Clarified Requirements
After each clarification, update the requirement statement to be:
- **Specific**: Clear and detailed
- **Measurable**: Has quantifiable criteria
- **Unambiguous**: Only one interpretation possible
- **Testable**: Can be verified

## Clarification Techniques

### 5W1H Method
- **Who**: Which users/roles are involved?
- **What**: What exactly needs to happen?
- **When**: Under what conditions/timing?
- **Where**: In which part of the system?
- **Why**: What's the business reason?
- **How**: What's the expected behavior?

### Boundary Analysis
- What's included in this requirement?
- What's explicitly excluded?
- What are the edge cases?
- What happens when things go wrong?

### Constraint Identification
- Performance requirements (speed, volume)
- Security requirements (authentication, authorization)
- Usability requirements (accessibility, user experience)
- Technical constraints (platforms, integrations)

## Templates

### Clarification Question Template
```
I need to clarify [specific aspect] of this requirement.

[Single focused question]?

Why I'm asking: [Explanation of why this matters for the requirement]
```

### Clarified Requirement Template
```
**Original**: [Vague requirement statement]

**Clarified**: [Clear, specific requirement]

**Acceptance Criteria**:
- Given [context]
- When [action]
- Then [expected result]
```

## Quality Checklist

Before moving to validation, ensure each requirement is:
- [ ] Has only one possible interpretation
- [ ] Includes all necessary details
- [ ] Defines clear boundaries
- [ ] Has measurable acceptance criteria
- [ ] Addresses edge cases and error conditions

## Common Clarification Scenarios

### Vague User Story
**Original**: "As a user, I want to search for products"
**Clarification needed**: Which users? What search criteria? How should results be displayed?

### Missing Business Rules
**Original**: "System should validate user input"
**Clarification needed**: What validation rules? What happens on validation failure?

### Unclear Integration
**Original**: "System should integrate with payment gateway"
**Clarification needed**: Which gateway? What payment methods? Error handling?

## Output
- Clarified requirement statements
- Updated acceptance criteria
- Documented assumptions and constraints
- Identified dependencies and risks
