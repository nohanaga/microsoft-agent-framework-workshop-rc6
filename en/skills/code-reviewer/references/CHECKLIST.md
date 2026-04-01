# Code Review Checklist

## Python

### Basics
- [ ] Compliant with PEP 8 style guide
- [ ] Type hints used appropriately
- [ ] Docstrings included for functions/classes
- [ ] Using f-strings (not `%` or `.format()`)

### Security
- [ ] No use of `eval()` / `exec()`
- [ ] Parameter binding used for SQL queries
- [ ] Sensitive information retrieved from environment variables
- [ ] No unsafe deserialization with `pickle`

### Performance
- [ ] List comprehensions used appropriately
- [ ] Generators used for large data processing
- [ ] `asyncio` utilized for I/O-bound operations
- [ ] No unnecessary global variables

## JavaScript / TypeScript

### Basics
- [ ] Using `const` / `let` (not `var`)
- [ ] Utilizing optional chaining (`?.`)
- [ ] Using `async/await` (not `.then()` chains)
- [ ] Avoiding the `any` type in TypeScript

### Security
- [ ] Using `textContent` instead of `innerHTML`
- [ ] User input is sanitized
- [ ] CORS settings are properly configured
- [ ] Dependency package versions are up to date

### Performance
- [ ] Preventing unnecessary re-renders (in React)
- [ ] Bundle size is considered
- [ ] No memory leaks (e.g., event listeners properly removed)
- [ ] Appropriate use of debounce / throttle

## Common

### Testing
- [ ] Unit tests exist
- [ ] Edge case tests exist
- [ ] Mocks are used appropriately
- [ ] Tests can run independently

### Documentation
- [ ] README is up to date
- [ ] Migration guide provided for breaking changes
- [ ] API documentation is accurate
