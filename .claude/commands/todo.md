---
allowed-tools: Task, Read, Write, Bash
description: Generate prioritized tasks from design with branch awareness
argument-hint: [generate|status|update]
---

# /todo - Smart Task Generation

Create actionable todo list from design documents with branch workspace integration.

## Usage

```bash
/todo          # Generate comprehensive task list from current branch design
/todo status   # Check todo list status and statistics
/todo update   # Update todo list based on implementation progress
```

## Main Execution Flow

When you run `/todo`, it orchestrates specialized agents:

```python
# Main orchestration logic
if args == "" or args == "generate":
    # Step 1: Analyze design document
    Task(
        subagent_type="general-purpose",
        description="Analyze design",
        prompt="Load design from branch workspace, assess complexity"
    )
    
    # Step 2: Generate comprehensive todos
    Task(
        subagent_type="sdac-todo-generator",
        description="Create task list",
        prompt="Generate prioritized tasks with dependencies and effort estimates"
    )
    
    # Step 3: Analyze PR strategy
    Task(
        subagent_type="sdac-pr-splitter",
        description="Determine PR strategy",
        prompt="Analyze if PR splitting needed based on task count and complexity"
    )
    
elif args == "status":
    # Check todo status
    Task(
        subagent_type="general-purpose",
        description="Show todo status",
        prompt="Display task statistics and completion progress"
    )
    
elif args == "update":
    # Update based on progress
    Task(
        subagent_type="sdac-todo-reconciler",
        description="Update todo list",
        prompt="Sync todo status with actual implementation progress"
    )
```

## Enhanced Process with Branch Workspace

### Phase 1: Design Analysis with Branch Context
Task(
  subagent_type="general-purpose",
  description="Analyze design in branch workspace",
  prompt="""
Analyze design document from current branch workspace:

1. **Load Branch Design**
   ```bash
   # Get current branch
   current_branch=$(git branch --show-current)
   
   # Check if design exists
   design_file=".claude/pr/${current_branch}/design-docs.md"
   
   if [[ ! -f "$design_file" ]]; then
     echo "Error: No design found for branch $current_branch"
     echo "Run '/design start' first"
     exit 1
   fi
   
   # Read design document
   cat "$design_file"
   ```

2. **Check Parent Branch Context**
   ```bash
   # Get parent branch info from status.json
   parent_branch=$(jq -r '.parent_branch // empty' ".claude/pr/${current_branch}/status.json")
   
   # If sub-branch, check parent todos for context
   if [[ -n "$parent_branch" && -f ".claude/pr/${parent_branch}/todo.md" ]]; then
     echo "Parent branch todos found, considering for context"
   fi
   ```

3. **Assess Complexity**
   - Count major components
   - Identify integration points
   - Estimate total effort
   - Determine optimal parallelism

4. **Extract Task Categories**
   - Backend services
   - Frontend components
   - Database changes
   - API endpoints
   - Tests required
   - Documentation needs
"""
)

### Phase 2: Task Generation with Workspace Save
Task(
  subagent_type="sdac-todo-generator",
  description="Generate tasks and save to workspace",
  prompt="""
Generate comprehensive task list from design:

1. **Create Prioritized Tasks**
   - Break design into atomic, actionable tasks
   - Assign priority levels (high/medium/low)
   - Estimate effort (S/M/L/XL)
   - Identify dependencies
   - Mark parallel-safe tasks

2. **Task Format**
   ```markdown
   # TODO List for [Branch Name]
   
   Generated: [timestamp]
   Total Tasks: [count]
   Estimated Effort: [total story points]
   Suggested Parallel Workers: [1-8]
   
   ## High Priority
   - [ ] [TASK-001] Implement user authentication API
     - Effort: M
     - Dependencies: None
     - Parallel-safe: Yes
     - Files: src/auth/\*
   
   - [ ] [TASK-002] Create database schema for users
     - Effort: S
     - Dependencies: None
     - Parallel-safe: Yes
     - Files: migrations/\*, models/\*
   
   ## Medium Priority
   ...
   
   ## Low Priority
   ...
   ```

3. **Save to Branch Workspace**
   ```bash
   current_branch=$(git branch --show-current)
   todo_file=".claude/pr/${current_branch}/todo.md"
   
   # Save todo list
   cat > "$todo_file"
   
   # Update status
   jq '.status = "todo-generated" | 
      .todo_generated = "'$(date -Iseconds)'" |
      .stats.total_tasks = '$total_tasks' |
      .stats.suggested_workers = '$suggested_workers \
     ".claude/pr/${current_branch}/status.json" > tmp.json && \
     mv tmp.json ".claude/pr/${current_branch}/status.json"
   ```

4. **Cross-Reference with Parent**
   - If sub-branch, ensure no duplicate tasks
   - Mark inherited vs new tasks
   - Maintain task ID consistency
"""
)

### Phase 3: PR Strategy Analysis
Task(
  subagent_type="sdac-pr-splitter",
  description="Analyze PR splitting needs",
  prompt="""
Determine optimal PR strategy based on tasks:

1. **Analyze Total Scope**
   ```bash
   current_branch=$(git branch --show-current)
   todo_file=".claude/pr/${current_branch}/todo.md"
   
   # Count tasks and estimate LOC
   total_tasks=$(grep -c "^\- \[ \]" "$todo_file")
   estimated_loc=$(($total_tasks * 50))  # Average 50 LOC per task
   ```

2. **PR Splitting Decision**
   - If < 300 LOC: Single PR
   - If 300-800 LOC: Consider 2 PRs
   - If > 800 LOC: Recommend 3+ PRs

3. **Splitting Strategy**
   ```markdown
   ## PR Splitting Recommendation
   
   Total Estimated LOC: [count]
   Recommended PRs: [1-5]
   
   ### PR 1: Core Infrastructure
   - Tasks: TASK-001, TASK-002, TASK-005
   - Focus: Database and models
   - Estimated LOC: 250
   
   ### PR 2: API Implementation  
   - Tasks: TASK-003, TASK-004, TASK-006
   - Focus: REST endpoints
   - Estimated LOC: 300
   - Dependencies: PR 1
   
   ### PR 3: Frontend Integration
   - Tasks: TASK-007, TASK-008
   - Focus: UI components
   - Estimated LOC: 200
   - Dependencies: PR 2
   ```

4. **Update Workspace**
   ```bash
   # Add PR strategy to status.json
   jq '.pr_strategy = {
     "recommended_prs": '$recommended_prs',
     "estimated_total_loc": '$estimated_loc',
     "splitting_rationale": "'$rationale'"
   }' ".claude/pr/${current_branch}/status.json" > tmp.json && \
   mv tmp.json ".claude/pr/${current_branch}/status.json"
   ```

5. **Sub-branch Creation Hints**
   - If splitting needed, suggest branch names
   - Example: feature-auth/auth-api, feature-auth/auth-ui
   - Maintain parent-child relationships
"""
)

## Branch Workspace Integration

### Automatic Features

1. **Branch-Specific Todos**
   - Each branch has its own todo.md
   - No confusion between features
   - Clear task ownership

2. **Parent-Child Awareness**
   ```bash
   # Check if working on sub-branch
   if [[ "$current_branch" == *"/"* ]]; then
     parent=$(echo "$current_branch" | cut -d'/' -f1)
     # Can reference parent todos
   fi
   ```

3. **Task ID Management**
   - Unique IDs per branch
   - Format: [BRANCH]-[NUMBER]
   - Prevents conflicts

### Status Tracking

```json
{
  "status": "todo-generated",
  "todo_generated": "2024-01-27T12:00:00Z",
  "stats": {
    "total_tasks": 15,
    "high_priority": 5,
    "medium_priority": 7,
    "low_priority": 3,
    "suggested_workers": 3,
    "estimated_loc": 750
  },
  "pr_strategy": {
    "recommended_prs": 2,
    "splitting_needed": true
  }
}
```

## GitHub Integration

### PR Planning Commands
```bash
# Check if PR already exists
gh pr list --head "$current_branch"

# Get PR template for consistency
gh api repos/{owner}/{repo}/contents/.github/pull_request_template.md

# Check branch protection rules
gh api repos/{owner}/{repo}/branches/main/protection
```

### Issue Linking
```bash
# Find related issues
gh issue list --label "feature-request"

# Link to parent issue if exists
gh issue view 123 --json number,title,body
```

## Output Examples

### Single Branch Todo
```markdown
# TODO List for feature-payment

Generated: 2024-01-27T12:00:00Z
Total Tasks: 12
Estimated Effort: 20 points
Suggested Parallel Workers: 3

## High Priority
- [ ] [PAY-001] Create payment service interface
- [ ] [PAY-002] Implement Stripe integration
- [ ] [PAY-003] Add payment database schema
```

### Sub-branch Todo with Parent Context
```markdown
# TODO List for feature-payment/stripe-integration

Generated: 2024-01-27T13:00:00Z
Parent Branch: feature-payment
Parent Tasks Inherited: 3
New Tasks: 5

## From Parent Branch
- [x] [PAY-001] Create payment service interface ✓

## This Branch
- [ ] [STRIPE-001] Implement Stripe webhook handler
- [ ] [STRIPE-002] Add Stripe configuration
```

## Success Metrics

- **Task Clarity**: Each task is atomic and actionable
- **Accurate Estimation**: Effort estimates within 20% of actual
- **Optimal Parallelism**: Suggested workers maximize efficiency
- **Smart PR Splitting**: PRs stay under 400 LOC for easy review

Remember: Good task breakdown is the foundation of efficient parallel implementation.