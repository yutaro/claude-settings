---
allowed-tools: Task
description: Comprehensive testing and coverage analysis
argument-hint: [run|write|coverage|fix]
---

# /test - Comprehensive Testing Suite

Automated test generation, execution, and coverage analysis.

## Usage

```bash
/test         # Run full testing workflow
/test write   # Generate missing tests
/test run     # Execute test suite
/test coverage # Analyze coverage gaps
/test fix     # Auto-fix failing tests
```

## Process

**Step 1: Test Generation**
Task(
  subagent_type="sdac-test-writer",
  description="Create comprehensive test suite",
  prompt="""
Generate comprehensive test coverage:

1. Analyze implemented code for test requirements
2. Create unit tests for individual functions/methods
3. Write integration tests for component interactions
4. Add edge case and error scenario tests
5. Ensure >80% coverage for new code
6. Follow project testing conventions and frameworks
"""
)

**Step 2: Test Execution**
Task(
  subagent_type="general-purpose",
  description="Execute test suite",
  prompt="""
Run comprehensive test suite:

1. Execute all unit tests
2. Run integration tests
3. Check test coverage metrics
4. Identify failing tests
5. Generate test execution report
"""
)

**Step 3: Coverage Analysis**
Task(
  subagent_type="sdac-test-writer",
  description="Analyze test coverage",
  prompt="""
Perform detailed coverage analysis:

1. Identify uncovered code paths
2. Analyze coverage quality vs quantity
3. Suggest additional test cases for gaps
4. Recommend testing improvements
5. Ensure critical paths are covered
"""
)

## Quality Standards

- **Unit Test Coverage**: 80%+ for new code
- **Integration Testing**: All API endpoints and component interactions
- **Edge Cases**: Error handling and boundary conditions
- **Performance**: Load testing for critical paths

## Output

- Comprehensive test suite
- Coverage reports and analysis
- Failing test identification and fixes
- Quality metrics and recommendations
- Production-ready test coverage