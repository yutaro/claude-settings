---
allowed-tools: Task, TodoWrite, Read, Write, Bash
description: Parallel implementation with branch workspace coordination
argument-hint: [start|status|reconcile]
---

# /implement - Intelligent Parallel Implementation

Execute implementation with branch-aware workspace management and dynamic agent orchestration.

## Usage

```bash
/implement start     # Start 3-agent parallel implementation
/implement status    # Check all agents' progress in current branch
/implement reconcile # Force reconciliation check
```

## Main Execution Flow

When you run `/implement`, it orchestrates multiple specialized agents:

```python
# Main orchestration logic
if args == "start":
    # Pre-flight checks
    Task(
        subagent_type="general-purpose",
        description="Verify workspace ready",
        prompt="Check design and todos exist in branch workspace"
    )
    
    # Launch parallel implementation
    Task(
        subagent_type="sdac-task-distributor",
        description="Launch parallel agents",
        prompt="""
        Launch 3 parallel agents:
        1. sdac-implementer - Build features
        2. sdac-design-reconciler - Ensure alignment
        3. sdac-todo-reconciler - Verify completion
        
        Monitor and coordinate their work.
        """
    )
    
elif args == "status":
    # Check all agent progress
    Task(
        subagent_type="sdac-status-coordinator",
        description="Aggregate agent status",
        prompt="Show progress from all active agents in current branch"
    )
    
elif args == "reconcile":
    # Force reconciliation
    Task(
        subagent_type="sdac-todo-reconciler",
        description="Deep verification",
        prompt="Thoroughly verify all claimed completions"
    )
```

## Branch Workspace Integration

### Pre-Implementation Checks
```bash
# Verify branch workspace setup
current_branch=$(git branch --show-current)
workspace_dir=".claude/pr/${current_branch}"

# Check required files exist
if [[ ! -f "$workspace_dir/design-docs.md" ]]; then
  echo "Error: No design found. Run '/design start' first"
  exit 1
fi

if [[ ! -f "$workspace_dir/todo.md" ]]; then
  echo "Error: No todo list found. Run '/todo' first"
  exit 1
fi

# Initialize implementation tracking
echo '{"implementation_started": "'$(date -Iseconds)'", "active_agents": 3}' > "$workspace_dir/implementation.json"
```

## 3-Agent Parallel Process

### Agent 1: Implementation with Branch Awareness
Task(
  subagent_type="sdac-implementer",
  description="Execute tasks from branch todo list",
  prompt="""
Implement tasks with branch workspace awareness:

1. **Load Branch Context**
   ```bash
   current_branch=$(git branch --show-current)
   workspace_dir=".claude/pr/${current_branch}"
   
   # Read design and todos
   design_docs="$workspace_dir/design-docs.md"
   todo_list="$workspace_dir/todo.md"
   ```

2. **Coordination File Management**
   ```bash
   # Create branch-specific coordination file
   coordination_file="$workspace_dir/doing.md"
   
   # Register work before starting
   echo "## Agent: implementer-1 ($(date -Iseconds))" >> "$coordination_file"
   echo "Working on: [file paths]" >> "$coordination_file"
   echo "Task: [todo description]" >> "$coordination_file"
   ```

3. **Task Selection**
   - Read todos from branch workspace
   - Select highest priority pending task
   - Check coordination file for conflicts
   - Register selected task

4. **Implementation Tracking**
   ```bash
   # Update todo status in branch workspace
   sed -i 's/\[ \] \[TASK-001\]/\[~\] \[TASK-001\]/' "$todo_list"
   
   # Log progress
   echo "Task TASK-001: In Progress (50%)" >> "$workspace_dir/progress.log"
   ```

5. **Branch-Specific Patterns**
   - Check parent branch for established patterns
   - Maintain consistency within feature branch
   - Document any new patterns discovered

Continue implementing until all tasks complete or blocked.
"""
)

### Agent 2: Design Reconciler with Branch Context
Task(
  subagent_type="sdac-design-reconciler",
  description="Ensure implementation matches branch design",
  prompt="""
Monitor implementation alignment with branch-specific design:

1. **Load Branch Design**
   ```bash
   current_branch=$(git branch --show-current)
   design_file=".claude/pr/${current_branch}/design-docs.md"
   
   # Also check parent design if sub-branch
   if [[ "$current_branch" == *"/"* ]]; then
     parent_branch=$(echo "$current_branch" | cut -d'/' -f1)
     parent_design=".claude/pr/${parent_branch}/design-docs.md"
   fi
   ```

2. **Track Design Compliance**
   - Review each implementation against design specs
   - Check architectural decisions are followed
   - Verify API contracts match design
   - Ensure data models align

3. **Document Deviations**
   ```bash
   # Create reconciliation log
   recon_log="$workspace_dir/reconciliation.log"
   
   echo "[$(date -Iseconds)] Deviation found:" >> "$recon_log"
   echo "- Design specified: Async processing" >> "$recon_log"
   echo "- Implementation: Sync with timeout" >> "$recon_log"
   echo "- Decision: Update design (better approach)" >> "$recon_log"
   ```

4. **Update Branch Design**
   - When implementation improves on design
   - Document rationale for changes
   - Maintain design evolution history
   - Flag breaking changes

5. **Cross-Branch Consistency**
   - Ensure consistency with parent branch patterns
   - Flag any architectural divergences
   - Maintain feature cohesion

Balance design integrity with practical improvements.
"""
)

### Agent 3: Todo Reconciler with Branch Tracking
Task(
  subagent_type="sdac-todo-reconciler",
  description="Verify todos in branch workspace",
  prompt="""
Verify todo completion within branch context:

1. **Load Branch Todos**
   ```bash
   current_branch=$(git branch --show-current)
   todo_file=".claude/pr/${current_branch}/todo.md"
   progress_log=".claude/pr/${current_branch}/progress.log"
   ```

2. **Verification Process**
   - Check each "completed" task in todo.md
   - Verify actual implementation exists
   - Test functionality works
   - Validate against acceptance criteria

3. **Update Todo Status Accurately**
   ```bash
   # Mark genuinely complete
   sed -i 's/\[~\] \[TASK-001\]/\[x\] \[TASK-001\]/' "$todo_file"
   
   # Revert false completions
   sed -i 's/\[x\] \[TASK-002\]/\[ \] \[TASK-002\]/' "$todo_file"
   
   # Add completion notes
   echo "TASK-001: Verified complete - all tests pass" >> "$progress_log"
   ```

4. **Branch-Specific Validation**
   - Check if task meets branch-specific requirements
   - Verify integration with parent branch code
   - Ensure no regression of parent features

5. **Generate Completion Report**
   ```markdown
   ## Branch Implementation Status
   
   Branch: feature-payment
   Started: 2024-01-27T10:00:00Z
   
   ### Completion Summary
   - Total Tasks: 15
   - Completed: 12 (80%)
   - In Progress: 2
   - Blocked: 1
   
   ### Verification Results
   - Verified Complete: 11
   - False Completions Fixed: 1
   - New Tasks Added: 2
   ```

Be thorough - AI agents often claim completion prematurely.
"""
)

## Branch-Aware Coordination

### Workspace File Structure
```
.claude/pr/feature-payment/
├── design-docs.md          # Feature design
├── todo.md                 # Task list
├── status.json            # Overall status
├── doing.md               # Active work coordination
├── progress.log           # Detailed progress
├── reconciliation.log     # Design deviations
└── implementation.json    # Implementation metadata
```

### Status Tracking
```json
{
  "branch": "feature-payment",
  "status": "implementing",
  "implementation_started": "2024-01-27T14:00:00Z",
  "stats": {
    "total_tasks": 15,
    "completed": 12,
    "in_progress": 2,
    "blocked": 1,
    "verified_complete": 11
  },
  "agents": {
    "implementer": "active",
    "design_reconciler": "active",
    "todo_reconciler": "active"
  }
}
```

### Parent-Child Branch Coordination
```bash
# For sub-branches, coordinate with parent
if [[ "$current_branch" == *"/"* ]]; then
  parent_branch=$(echo "$current_branch" | cut -d'/' -f1)
  
  # Check parent implementation status
  parent_status=".claude/pr/${parent_branch}/status.json"
  
  # Ensure parent tasks completed before dependent tasks
  parent_complete=$(jq -r '.stats.completed' "$parent_status")
fi
```

## GitHub Integration

### Progress Reporting
```bash
# Update PR description with progress
gh pr edit --body "$(cat <<EOF
## Implementation Progress

Branch: $(git branch --show-current)
Progress: 12/15 tasks (80%)

### Completed
- [x] User authentication API
- [x] Database schema
- [x] JWT token generation

### In Progress
- [ ] OAuth integration (50%)
- [ ] Email verification (30%)

See .claude/pr/$(git branch --show-current)/progress.log for details
EOF
)"
```

### Commit Management
```bash
# Commits are branch-aware
git add .
git commit -m "feat($(git branch --show-current)): Implement tasks 1-5

- Completed authentication API
- Added user model and migrations
- Implemented JWT token generation

Progress: 5/15 tasks complete"
```

## Success Metrics

- **Branch Isolation**: Each branch has independent workspace
- **Progress Visibility**: Real-time status in branch files
- **Conflict Prevention**: Branch-specific coordination files
- **Parent Awareness**: Sub-branches respect parent context
- **GitHub Integration**: Progress reflected in PRs

## Usage Examples

### Feature Branch Implementation
```bash
git checkout -b feature-notifications
/design start
/todo
/implement start
# All work isolated to .claude/pr/feature-notifications/
```

### Sub-feature Implementation
```bash
git checkout -b feature-notifications/email-provider
/design start  # Inherits parent context
/todo          # Shows parent tasks + new tasks
/implement start
# Work in .claude/pr/feature-notifications/email-provider/
```

Remember: Every branch gets its own isolated workspace, enabling true parallel development across features.