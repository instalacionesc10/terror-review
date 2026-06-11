---
description: "Triple-lens code review combining Architecture + Backend + Security perspectives. Use when auditing a module, feature, or set of files for quality, scalability, and vulnerabilities. Accepts optional path argument."
---

# Terror Review - Triple Lens Code Audit

**Announce at start:** "Running Terror Review (Architecture + Backend + Security) on target: $ARGUMENTS"

## Target Resolution

- If `$ARGUMENTS` is provided, use it as the target path/module
- If empty, infer from recent git changes (`git diff --name-only HEAD~3`) or ask the user

## Phase 1: Architecture Lens (senior-architect)

Analyze the target for:
- **SOLID violations**: Single responsibility, open/closed, dependency inversion
- **Component boundaries**: Are responsibilities properly separated? Coupling vs cohesion
- **Dependency flow**: Do dependencies flow inward? Circular dependencies?
- **Scalability patterns**: Will this break at 10x load? N+1 queries? Unbounded loops?
- **Code organization**: File size, function length, nesting depth
- **Pattern consistency**: Does it follow the project's established patterns?

## Phase 2: Backend Lens (senior-backend)

Analyze the target for:
- **API design**: RESTful conventions, payload structure, status codes, error responses
- **Database queries**: N+1 problems, missing indexes, unbounded SELECTs, SQL injection
- **Error handling**: Silent failures, swallowed exceptions, missing try/catch on async
- **Performance**: Unnecessary re-renders, blocking calls, missing caching, over-fetching
- **Data flow**: Props drilling, context bloat, state management issues
- **Validation**: Input validation at boundaries, type safety, null checks

## Phase 3: Security Lens (senior-security)

Analyze the target for:
- **OWASP Top 10**: Injection, broken auth, sensitive data exposure, XXE, broken access control, misconfig, XSS, insecure deserialization, vulnerable components, insufficient logging
- **Input validation**: User input sanitized? Parameterized queries? HTML escaping?
- **Authentication/Authorization**: Token handling, session management, permission checks
- **Data exposure**: Sensitive data in logs/responses? API keys in code? PII leaks?
- **CORS/Headers**: Missing security headers? Permissive CORS?
- **Dependency vulnerabilities**: Known CVEs in dependencies?

## Output Format

Present findings as a structured report:

### Summary
One paragraph overview of the module's health.

### Findings

| # | Severity | Lens | File:Line | Issue | Recommended Fix |
|---|----------|------|-----------|-------|-----------------|
| 1 | CRITICAL | Security | path:123 | ... | ... |
| 2 | HIGH | Architecture | path:45 | ... | ... |
| ... | ... | ... | ... | ... | ... |

Severity levels: CRITICAL > HIGH > MEDIUM > LOW > INFO

### Scores

| Dimension | Score (1-10) | Notes |
|-----------|-------------|-------|
| Architecture | X/10 | ... |
| Backend Quality | X/10 | ... |
| Security | X/10 | ... |
| **Overall** | **X/10** | ... |

### Priority Actions (Top 5)

Ordered list of the 5 most impactful fixes, with estimated effort (S/M/L).

### Positive Patterns

List 2-3 things the code does well (reinforcement, not just criticism).