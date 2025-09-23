# Run All Tests and Fix Failures

## Overview
Execute the full test suite and systematically fix any failures, ensuring code quality and functionality.

## Steps
1. **Run test suite**
   - Execute all tests in the project 
   - Capture output and identify failures

2. **Analyze failures**
   - Categorize by type: flaky, broken, new failures
   - Prioritize fixes based on impact
   - Check if failures are related to recent changes

3. **Fix issues systematically**
   - Start with the most critical failures
   - Fix one issue at a time
   - Re-run individual test files or individual tests after each fix
   - Do not modify production code ever to fix a test unless it is to improve dependency injection so that you can test with mock dependencies
   - Prefer fast unit tests with mocked dependencies over integration tests

4. **Run the full test suite**
   - Run the full test suite to ensure that no tests fail due to unexpected interactions with one another
