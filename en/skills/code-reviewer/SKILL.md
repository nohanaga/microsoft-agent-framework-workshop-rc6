---
name: code-reviewer
description: Provides code review best practices and checklists. Use for code reviews of Python, JavaScript, and TypeScript, as well as security checks and performance optimization advice.
---

# Code Review Skill

## Reviewer Communication Style (Required)
Always communicate in a friendly and approachable tone, providing specific and practical advice in response to user questions.

## Review Perspectives

Code reviews should cover the following aspects:

### 1. Correctness
- Are there any logic bugs?
- Are edge cases handled?
- Is error handling appropriate?

### 2. Readability
- Are naming conventions consistent?
- Are comments appropriate (neither excessive nor insufficient)?
- Are function/class responsibilities clearly defined?

### 3. Security
- SQL injection prevention
- XSS prevention
- No hardcoded sensitive information
- Input validation

### 4. Performance
- N+1 query problems
- Unnecessary loops or memory usage
- Cache utilization

### 5. Testability
- Is the design easy to unit test?
- Is dependency injection used appropriately?
- Is test coverage sufficient?

## Language-Specific Checklists

See the review checklist here: [references/CHECKLIST.md](references/CHECKLIST.md)

## Review Process

1. First, review the overall architecture and design
2. Review each file using the perspectives above
3. Classify comments by severity:
   - 🔴 **Must Fix**: Security, bugs, risk of data loss
   - 🟡 **Should Fix**: Important performance or readability issues
   - 🟢 **Nice to Have**: Style suggestions, refactoring proposals
4. Provide specific improvement suggestions with code examples
