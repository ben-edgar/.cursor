---
name: Code Review
description: Perform a comprehensive code review comparing current branch to main, focusing on maintainability, DRY principles, test coverage, and code quality
parameters:
  - name: pr_description
    type: string
    required: false
    description: Optional PR description to validate against code changes
  - name: focus_areas
    type: string
    required: false
    description: Specific areas to focus on (e.g., "notifications, database, UI")
  - name: output_file
    type: string
    required: false
    description: Output file path (defaults to code_review_results.md)
---

# Code Review Command

## Overview
Perform a comprehensive code review of all changes in the current branch compared to main, with a focus on:
- Maintainability and code quality
- DRY (Don't Repeat Yourself) principles
- Test coverage for critical business logic
- Alignment with commit messages and PR descriptions
- Performance implications
- Security considerations

## Process

### 1. Get Branch Diff
```bash
# Get the diff between current branch and main, check total files with stats and the full diff
git diff main...HEAD --stat
git diff main...HEAD
```

### 2. Analyze Changes
For each changed file, examine:
- **Code Quality**: Readability, naming conventions, complexity
- **Architecture**: Proper separation of concerns, clean architecture principles
- **DRY Violations**: Duplicated code that should be extracted
- **Test Coverage**: Missing unit tests for business logic
- **Error Handling**: Proper exception handling and user feedback
- **Documentation**: Comments for complex logic

### 3. Validate Against Commit Messages
Check if the code changes align with what the commit messages describe.

### 4. Validate Against PR Description
If provided, ensure the code implements what the PR description promises.

### 5. Generate Review Report
Create a structured markdown report with:
- Summary of changes
- Critical issues (must fix)
- Suggestions for improvement
- Test coverage gaps
- Performance concerns
- Security considerations

## Review Criteria

### Critical Issues (Must Fix)
- **Security vulnerabilities**: Hardcoded secrets, unsafe data handling
- **Breaking changes**: API changes without proper migration
- **Performance regressions**: Unnecessary rebuilds, memory leaks
- **Test failures**: Missing tests for critical business logic
- **Architecture violations**: Tight coupling, violation of SOLID principles

### Code Quality Issues
- **Complexity**: Functions > 20 lines, deep nesting
- **Naming**: Unclear variable/function names
- **Duplication**: Repeated code blocks
- **Error handling**: Missing try-catch, poor error messages
- **Documentation**: Missing comments for complex logic

### Test Coverage
- **Unit tests**: Missing for services, repositories, business logic
- **Widget tests**: Missing for complex UI components
- **Integration tests**: Missing for critical user flows
- **Mock usage**: Proper mocking of external dependencies

## Output Format

The review will generate a markdown file with the following structure:

```markdown
# Code Review Results

## Summary
- **Branch**: [current branch]
- **Base**: main
- **Files Changed**: [count]
- **Lines Added**: [count]
- **Lines Removed**: [count]

## Critical Issues (Must Fix)
### [Issue Title]
- **File**: `path/to/file:line`
- **Severity**: Critical
- **Description**: [detailed description]
- **Recommendation**: [specific fix suggestion]

## Code Quality Issues
### [Issue Title]
- **File**: `path/to/file:line`
- **Severity**: Medium
- **Description**: [detailed description]
- **Recommendation**: [specific fix suggestion]

## Test Coverage Gaps
### [Missing Test]
- **File**: `path/to/file`
- **Description**: [what needs testing]
- **Recommendation**: [test implementation suggestion]

## Performance Concerns
### [Performance Issue]
- **File**: `path/to/file:line`
- **Description**: [performance impact]
- **Recommendation**: [optimization suggestion]

## Security Considerations
### [Security Issue]
- **File**: `path/to/file:line`
- **Description**: [security concern]
- **Recommendation**: [security fix]

## Positive Findings
- [List of good practices and well-implemented features]

## Recommendations Summary
1. [Priority 1 recommendation]
2. [Priority 2 recommendation]
3. [Priority 3 recommendation]
```

## Implementation Notes

1. **Git Integration**: Use git commands to get accurate diffs
2. **File Analysis**: Read and analyze each changed file
3. **Context Awareness**: Consider the broader codebase context
4. **Test Analysis**: Check for corresponding test files
5. **Performance**: Look for potential performance issues
6. **Security**: Identify security vulnerabilities
7. **Documentation**: Ensure proper documentation

## Quality Gates

Before marking the review complete, ensure:
- [ ] All critical issues are identified
- [ ] Test coverage gaps are documented
- [ ] Performance implications are assessed
- [ ] Security considerations are reviewed
- [ ] Changes match commit messages and PR description
- [ ] Recommendations are actionable and specific

