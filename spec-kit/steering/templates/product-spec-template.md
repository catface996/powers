# Product Specification Template

Use this template when generating product specifications from project discovery.

<!--
  This template is used by the Discover workflow to document existing projects.
  Fill in sections based on code analysis and detected patterns.
  Mark uncertain items with [INFERRED] or [NEEDS CLARIFICATION].
-->

---

# Product Specification: [PROJECT_NAME]

**Generated**: [TIMESTAMP]
**Version**: [VERSION]
**Status**: [Draft/Review/Approved]
**Last Updated**: [DATE]

## Executive Summary

[2-3 paragraph overview of what the product does, who it serves, and its key value proposition. This should be understandable by non-technical stakeholders.]

---

## Product Overview

### Purpose

[Why this product exists - the problem it solves and the value it provides]

### Target Audience

| Audience | Description | Primary Needs |
|----------|-------------|---------------|
| [User Type 1] | [Description] | [Key needs] |
| [User Type 2] | [Description] | [Key needs] |

### Key Value Propositions

1. **[Value 1]**: [Description of benefit]
2. **[Value 2]**: [Description of benefit]
3. **[Value 3]**: [Description of benefit]

---

## Feature Inventory

### Core Features

| ID | Feature | Description | Priority | Status |
|----|---------|-------------|----------|--------|
| F001 | [Feature Name] | [Brief description] | P1 | Active |
| F002 | [Feature Name] | [Brief description] | P1 | Active |

### Supporting Features

| ID | Feature | Description | Priority | Status |
|----|---------|-------------|----------|--------|
| F010 | [Feature Name] | [Brief description] | P2 | Active |

### Planned Features

| ID | Feature | Description | Priority | Target |
|----|---------|-------------|----------|--------|
| F020 | [Feature Name] | [Brief description] | P2 | [Version/Date] |

---

## User Journeys

### Journey 1: [Journey Name]

**Actor**: [User type]
**Goal**: [What user wants to accomplish]

```
1. User [action]
2. System [response]
3. User [action]
4. System [response]
5. Result: [outcome]
```

### Journey 2: [Journey Name]

**Actor**: [User type]
**Goal**: [What user wants to accomplish]

```
1. User [action]
2. System [response]
3. ...
```

---

## Architecture Overview

### System Context

```
┌─────────────────────────────────────────────────────────────┐
│                      [SYSTEM NAME]                          │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐                 │
│  │ [Comp1] │───▶│ [Comp2] │───▶│ [Comp3] │                 │
│  └─────────┘    └─────────┘    └─────────┘                 │
└─────────────────────────────────────────────────────────────┘
        │                │                │
        ▼                ▼                ▼
   [External 1]    [External 2]    [External 3]
```

### Component Breakdown

| Component | Responsibility | Technology |
|-----------|----------------|------------|
| [Component 1] | [What it does] | [Tech used] |
| [Component 2] | [What it does] | [Tech used] |

### Data Flow

1. **Input**: [How data enters the system]
2. **Processing**: [How data is transformed]
3. **Storage**: [How data is persisted]
4. **Output**: [How data is presented/returned]

---

## Technical Summary

### Technology Stack

| Layer | Technology | Version | Purpose |
|-------|------------|---------|---------|
| Language | [e.g., TypeScript] | [e.g., 5.0] | Primary development language |
| Framework | [e.g., Next.js] | [e.g., 14.0] | Application framework |
| Database | [e.g., PostgreSQL] | [e.g., 15] | Data persistence |
| Cache | [e.g., Redis] | [e.g., 7.0] | Performance caching |
| Search | [e.g., Elasticsearch] | [e.g., 8.0] | Full-text search |

### External Dependencies

| Service | Purpose | Criticality |
|---------|---------|-------------|
| [Service 1] | [What it provides] | [High/Medium/Low] |
| [Service 2] | [What it provides] | [High/Medium/Low] |

### Infrastructure Requirements

**Minimum Requirements**:
- CPU: [requirement]
- Memory: [requirement]
- Storage: [requirement]
- Network: [requirement]

**Recommended Production Setup**:
- [Description of production infrastructure]

---

## API Reference

### REST Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | /api/[resource] | List resources | Yes |
| GET | /api/[resource]/:id | Get single resource | Yes |
| POST | /api/[resource] | Create resource | Yes |
| PUT | /api/[resource]/:id | Update resource | Yes |
| DELETE | /api/[resource]/:id | Delete resource | Yes |

### Data Models

#### [Model Name]

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| [field] | [type] | [Yes/No] | [Description] |

#### [Model Name 2]

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Unique identifier |
| [field] | [type] | [Yes/No] | [Description] |

---

## Security

### Authentication

- **Method**: [e.g., JWT, OAuth 2.0, Session-based]
- **Provider**: [e.g., Auth0, Custom, Firebase]
- **Session Duration**: [e.g., 24 hours]

### Authorization

| Role | Permissions |
|------|-------------|
| Admin | Full access |
| User | [Specific permissions] |
| Guest | [Limited permissions] |

### Data Protection

- **Encryption at Rest**: [Yes/No - details]
- **Encryption in Transit**: [Yes/No - details]
- **PII Handling**: [How personal data is handled]

---

## Quality & Testing

### Test Coverage

| Type | Coverage | Location |
|------|----------|----------|
| Unit Tests | [X%] | [path] |
| Integration Tests | [X%] | [path] |
| E2E Tests | [X%] | [path] |

### Quality Gates

- [ ] All tests pass
- [ ] Code coverage >= [X]%
- [ ] No critical security vulnerabilities
- [ ] Performance benchmarks met
- [ ] Documentation updated

---

## Deployment & Operations

### Build Process

```bash
# Build commands
[command 1]
[command 2]
```

### Deployment

**Environment**: [e.g., AWS, GCP, Azure, On-premise]
**Method**: [e.g., Docker, Kubernetes, Serverless]
**Pipeline**: [e.g., GitHub Actions, Jenkins, CircleCI]

### Monitoring

| Aspect | Tool | Dashboard |
|--------|------|-----------|
| Application | [e.g., DataDog] | [URL] |
| Infrastructure | [e.g., CloudWatch] | [URL] |
| Logs | [e.g., ELK Stack] | [URL] |

### Incident Response

- **On-call**: [Team/Contact]
- **Escalation**: [Process]
- **SLA**: [Target uptime, response times]

---

## Known Issues & Technical Debt

### Active Issues

| ID | Description | Severity | Workaround |
|----|-------------|----------|------------|
| [ID] | [Description] | [High/Medium/Low] | [Workaround if any] |

### Technical Debt

| Item | Description | Impact | Effort to Fix |
|------|-------------|--------|---------------|
| [Item] | [Description] | [Impact description] | [S/M/L/XL] |

---

## Roadmap

### Short-term (Next 3 months)

- [ ] [Initiative 1]
- [ ] [Initiative 2]

### Medium-term (3-6 months)

- [ ] [Initiative 3]
- [ ] [Initiative 4]

### Long-term (6-12 months)

- [ ] [Initiative 5]
- [ ] [Initiative 6]

---

## Appendix

### Glossary

| Term | Definition |
|------|------------|
| [Term 1] | [Definition] |
| [Term 2] | [Definition] |

### References

- [Reference 1]: [URL or document]
- [Reference 2]: [URL or document]

### Change Log

| Date | Version | Changes | Author |
|------|---------|---------|--------|
| [Date] | [Version] | [Description] | [Author] |
