---
allowed-tools: Task
description: Continue the previous interrupted operation
argument-hint: [context]
---

# Continue - Resume Interrupted Work

## Overview
Resumes the last interrupted operation or continues working on the current task.

## Usage
```bash
/continue              # Resume last operation
/continue "context"    # Resume with additional context
```

## What It Does

Task(
  subagent_type="general-purpose",
  description="Resume interrupted work",
  prompt="""
Continue the previously interrupted operation:

1. **Identify Context**:
   - Check recent conversation history
   - Find the last active task or operation
   - Understand what was being done
   - Identify where it was interrupted

2. **Resume Operation**:
   - Continue from the exact point of interruption
   - Maintain the same approach and style
   - Use the same tools and methods
   - Keep consistent with previous work

3. **Handle State**:
   - Check for any partial changes
   - Verify file states if applicable
   - Resume any multi-step processes
   - Maintain todo list continuity

4. **Additional Context**:
   - If context provided: "${1}"
   - Incorporate any new requirements
   - Adjust approach if needed

5. **Complete the Task**:
   - Finish what was started
   - Ensure quality standards
   - Update any tracking files
   - Report completion status

Remember to maintain consistency with the interrupted work.
"""
)

## Examples

### Simple Resume
```bash
/continue
# Resumes exactly where you left off
```

### Resume with Context
```bash
/continue "but skip the test writing for now"
# Continues previous work with modification
```

### After Interruption
```bash
# User interrupts a long implementation...
/continue
# SDAC picks up right where it stopped
```

## Common Scenarios

1. **Long Operations**
   - Implementation was interrupted
   - Continue with remaining tasks

2. **Multi-Step Processes**
   - Design refinement interrupted
   - Continue asking questions

3. **Complex Workflows**
   - PR creation interrupted
   - Continue with remaining steps

## Tips

- SDAC remembers the full context
- No need to re-explain everything
- Works with all SDAC operations
- Maintains consistency automatically