---
allowed-tools: Task
description: Generate prioritized tasks from design
argument-hint: none
---

# /todo - Smart Task Generation

Create actionable todo list from design with PR strategy analysis.

## Usage

```bash
/todo  # Generate comprehensive task list
```

## Process

**Step 1: Design Analysis**
Task(
  subagent_type="general-purpose",
  description="Analyze design document",
  prompt="""
Analyze current design document:

1. Read design document from current branch
2. Assess complexity and scope
3. Identify major components and dependencies
4. Estimate implementation effort
"""
)

**Step 2: Task Generation**
Task(
  subagent_type="sdac-todo-generator",
  description="Generate implementation tasks",
  prompt="""
Create prioritized task list:

1. Break design into actionable tasks
2. Prioritize by dependencies and importance
3. Estimate effort per task
4. Identify parallel execution opportunities
5. Create clear, specific task descriptions
"""
)

**Step 3: PR Strategy**
Task(
  subagent_type="sdac-pr-splitter",
  description="Analyze PR splitting strategy",
  prompt="""
Determine optimal PR strategy:

1. Analyze total scope and complexity
2. Identify logical breaking points
3. Recommend PR splitting if >500 lines
4. Suggest parallel development paths
5. Optimize for review efficiency
"""
)

## Output

- Prioritized task list
- PR splitting recommendations
- Parallel execution plan
- Worker scaling suggestions
- Ready for `/implement`