---
allowed-tools: Task
description: Code quality analysis and standards enforcement
argument-hint: [check|rules|fix|init]
---

# /quality - Code Quality Assurance

Multi-dimensional code quality analysis with automated fixes.

## Usage

```bash
/quality        # Full quality assessment
/quality check  # Quick quality check
/quality rules  # Verify coding standards
/quality fix    # Auto-fix detected issues
/quality init   # Initialize project standards
```

## Process

**Step 1: Quality Analysis**
Task(
  subagent_type="sdac-quality-checker",
  description="Comprehensive quality assessment",
  prompt="""
Perform multi-dimensional quality analysis:

1. **Maintainability (25%)**
   - Code clarity and readability
   - Proper abstraction levels
   - Documentation completeness

2. **Security (25%)**
   - Input validation
   - Authentication/authorization
   - Vulnerability patterns

3. **Performance (20%)**
   - Algorithm efficiency
   - Resource usage
   - Database optimization

4. **Reliability (20%)**
   - Error handling
   - Logging quality
   - Recovery mechanisms

5. **Testability (10%)**
   - Test coverage
   - Mock-ability
   - Function isolation

Generate overall quality score and specific recommendations.
"""
)

**Step 2: Standards Enforcement**
Task(
  subagent_type="general-purpose",
  description="Check coding standards compliance",
  prompt="""
Verify adherence to coding standards:

1. Check project-specific rules from .claude/rules/
2. Verify code style and formatting
3. Ensure naming conventions
4. Check for best practice violations
5. Validate documentation requirements
"""
)

**Step 3: Automated Fixes**
Task(
  subagent_type="general-purpose",
  description="Apply automated quality fixes",
  prompt="""
Apply automated quality improvements:

1. Fix code formatting and style issues
2. Add missing documentation
3. Optimize imports and dependencies
4. Apply security best practices
5. Improve error handling patterns
"""
)

## Quality Standards

- **Overall Score**: 8.0/10 minimum for production
- **Security**: No critical vulnerabilities
- **Performance**: No significant regressions
- **Maintainability**: Clear, documented, well-structured code

## Output

- Quality score breakdown by dimension
- Specific issues with fix recommendations
- Automated fixes applied
- Standards compliance report
- Production readiness assessment