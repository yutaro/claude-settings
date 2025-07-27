---
allowed-tools: Task, TodoWrite, Read, Write, Bash, Grep
description: PR-driven development orchestrator - automatic branch, implementation, and PR management
argument-hint: [start|pr|status|merge]
---

# /sdac - PR-Driven Development Orchestrator

Intelligently manages your entire PR-based development workflow: branch creation, implementation, PR splitting, and review preparation.

## Usage

```bash
/sdac              # Start new feature or continue existing work
/sdac pr           # Create PR with auto-generated description
/sdac status       # Check workflow and PR status
/sdac merge        # Post-merge cleanup and knowledge sync
```

## Main Execution Flow

When you run `/sdac`, it orchestrates multiple specialized agents:

```python
# Main orchestration logic
if args == "start" or args == "":
    # Step 1: Setup branch and workspace
    Task(
        subagent_type="general-purpose",
        description="Setup PR workflow",
        prompt="Check current branch, create feature branch if needed, initialize PR workspace"
    )
    
    # Step 2: Design with PR awareness
    Task(
        subagent_type="sdac-design-questioner",
        description="Interactive design phase",
        prompt="Guide user through design with PR size considerations"
    )
    
    # Step 3: Generate optimized todos
    Task(
        subagent_type="sdac-todo-generator", 
        description="Create PR-friendly task list",
        prompt="Generate tasks grouped by PR boundaries"
    )
    
    # Step 4: Launch parallel implementation
    Task(
        subagent_type="sdac-task-distributor",
        description="Coordinate parallel execution",
        prompt="Launch 3-5 implementers based on task complexity"
    )

elif args == "pr":
    # Create and manage PR
    Task(
        subagent_type="sdac-pr-creator",
        description="Create comprehensive PR",
        prompt="Generate PR with description, review guide, and proper labels"
    )

elif args == "status":
    # Check progress across all agents
    Task(
        subagent_type="sdac-status-coordinator",
        description="Aggregate status",
        prompt="Show branch, PR, implementation, and review status"
    )

elif args == "merge":
    # Post-merge knowledge extraction
    Task(
        subagent_type="sdac-knowledge-synthesizer",
        description="Extract PR learnings",
        prompt="Analyze merged PR for patterns and update knowledge base"
    )
    
    # Cleanup and archive
    Task(
        subagent_type="general-purpose",
        description="Post-merge cleanup",
        prompt="Archive branch data, delete merged branch, update main"
    )
```

## PR-Driven Workflow

### Automatic Flow
1. **Branch Creation** → Auto-creates feature branch
2. **Design & Planning** → Interactive design with PR size awareness
3. **Implementation** → PR-optimized parallel execution
4. **PR Preparation** → Auto-generates PR description and review guide
5. **Post-Merge** → Knowledge extraction and cleanup

## Detailed Agent Workflows

### Phase 0: Branch Strategy
When starting a new feature, the orchestrator launches:
```python
Task(
  subagent_type="general-purpose",
  description="Setup PR-driven development",
  prompt="""
Initialize PR-driven workflow:

1. **Check Current Branch**
   ```bash
   current_branch=$(git branch --show-current)
   
   # If on main/master, create feature branch
   if [[ "$current_branch" == "main" || "$current_branch" == "master" ]]; then
     echo "📌 Let's create a feature branch first."
     echo "What feature are you building? (e.g., user-auth, payment-integration)"
     read feature_name
     
     # Create branch with naming convention
     branch_name="feature/${feature_name}"
     git checkout -b "$branch_name"
     
     # Link to issue if provided
     echo "Related issue number? (optional, press enter to skip)"
     read issue_number
     if [[ -n "$issue_number" ]]; then
       echo "issue: #$issue_number" > ".claude/pr/${branch_name}/metadata.json"
     fi
   fi
   ```

2. **Initialize PR Workspace**
   ```bash
   workspace=".claude/pr/${current_branch}"
   mkdir -p "$workspace"
   
   # Create PR tracking file
   echo '{
     "pr_strategy": "single",
     "target_branch": "main",
     "draft": true,
     "reviewers": []
   }' > "$workspace/pr-config.json"
   ```

3. **Check Existing PR**
   ```bash
   # Check if PR already exists
   existing_pr=$(gh pr list --head "$current_branch" --json number --jq '.[0].number')
   
   if [[ -n "$existing_pr" ]]; then
     echo "📋 Found existing PR #$existing_pr"
     gh pr view "$existing_pr"
   fi
   ```
"""
)
```

### Phase 1: PR-Aware Design
The design phase uses specialized agent:
```python
Task(
  subagent_type="sdac-design-questioner",
  description="Create design with PR strategy",
  prompt="""
Design with PR best practices in mind:

1. **Context Gathering**
   - Standard design questions
   - Additional PR considerations:
     - "Is this a single PR or will it need splitting?"
     - "What's the review complexity?"
     - "Any risky changes that need careful review?"

2. **PR Size Estimation**
   During design, continuously estimate:
   - Total LOC expected
   - Number of files affected
   - Review complexity score
   
   If > 400 LOC estimated:
   - Suggest PR splitting strategy
   - Design natural breaking points
   - Plan incremental delivery

3. **Review Considerations**
   - Identify areas needing careful review
   - Note security implications
   - Flag breaking changes
   - Document testing requirements

4. **Save PR Metadata**
   ```json
   {
     "estimated_loc": 350,
     "review_complexity": "medium",
     "breaking_changes": false,
     "security_review": false,
     "suggested_reviewers": ["backend-team"],
     "pr_strategy": "single"
   }
   ```
"""
)
```

### Phase 2: PR-Optimized Todo Generation
Todo generation with PR boundaries:
```python
Task(
  subagent_type="sdac-todo-generator",
  description="Generate PR-friendly tasks",
  prompt="""
Create tasks optimized for PR workflow:

1. **Task Grouping for PRs**
   - Group related tasks that should ship together
   - Mark PR boundaries clearly
   - Ensure each PR is independently deployable

2. **PR Splitting Strategy**
   If design suggests multiple PRs:
   ```markdown
   ## PR Strategy: 2 PRs Recommended
   
   ### PR 1: Backend API (Prerequisites)
   Tasks: TASK-001 to TASK-005
   - Database schema
   - API endpoints
   - Core business logic
   Estimated: 300 LOC
   Branch: feature/auth → feature/auth-api
   
   ### PR 2: Frontend Integration
   Tasks: TASK-006 to TASK-010
   - UI components
   - API integration
   - User flows
   Estimated: 250 LOC
   Branch: feature/auth → feature/auth-ui
   Depends on: PR 1
   ```

3. **Review Preparation Tasks**
   Add tasks for PR readiness:
   - [ ] Write comprehensive tests
   - [ ] Update documentation
   - [ ] Add PR description
   - [ ] Create review guide
   - [ ] Run linting and checks

4. **Branch Strategy Tasks**
   If splitting needed:
   - [ ] Create sub-branches for each PR
   - [ ] Set up PR dependencies
   - [ ] Plan merge order
"""
)
```

### Phase 3: Parallel Implementation
Launch multiple agents in parallel:
```python
# Main distributor launches sub-agents
Task(
  subagent_type="sdac-task-distributor",
  description="Orchestrate parallel agents",
  prompt="Launch 3-5 agents based on todo complexity and dependencies"
)

# Each implementer works independently
for i in range(num_agents):
    Task(
  subagent_type="sdac-implementer",
  description="Implement with PR best practices",
  prompt="""
Implement with PR review in mind:

1. **Commit Strategy**
   - Logical, atomic commits
   - Clear commit messages with context
   - Reference issue numbers
   
   ```bash
   # Good commit messages for PR
   git commit -m "feat(auth): Add JWT token generation

   - Implement RS256 signing
   - Add token expiration logic
   - Include refresh token support
   
   Refs: #123"
   ```

2. **Review-Friendly Code**
   - Add comments for complex logic
   - Include "Review Note:" comments for reviewers
   - Keep changes focused and coherent
   - Avoid mixing refactoring with features

3. **Incremental Progress**
   - Push changes regularly
   - Keep PR in draft while implementing
   - Update PR description as you go

4. **Pre-Review Checklist**
   Before marking PR ready:
   - [ ] All tests passing
   - [ ] Linting clean
   - [ ] Documentation updated
   - [ ] PR description complete
   - [ ] Self-review done
"""
    )
```

### Phase 4: PR Creation & Management
Automated PR creation:
```python
Task(
  subagent_type="sdac-pr-creator",
  description="Create and manage PR",
  prompt="""
Automate PR creation and management:

1. **Auto-generate PR Description**
   ```bash
   # Create PR with comprehensive description
   gh pr create --draft --title "feat: $feature_name" --body "$(cat <<EOF
   ## Summary
   $summary_from_design
   
   ## Changes
   $bullet_points_from_todos
   
   ## Testing
   - [ ] Unit tests added/updated
   - [ ] Integration tests passing
   - [ ] Manual testing completed
   
   ## Review Guide
   1. Start with: $key_files
   2. Key changes: $important_changes
   3. Risk areas: $risk_areas
   
   ## Checklist
   - [ ] Tests passing
   - [ ] Documentation updated
   - [ ] No breaking changes (or documented)
   - [ ] Security considerations addressed
   
   Related: #$issue_number
   EOF
   )"
   ```

2. **PR Status Management**
   ```bash
   # Update PR status as implementation progresses
   current_pr=$(gh pr list --head "$(git branch --show-current)" --json number --jq '.[0].number')
   
   # Mark ready when complete
   gh pr ready "$current_pr"
   
   # Add reviewers
   gh pr edit "$current_pr" --add-reviewer "@backend-team"
   
   # Add labels
   gh pr edit "$current_pr" --add-label "feature,needs-review"
   ```

3. **Review Preparation**
   Generate review guide:
   - Key areas to focus on
   - Potential concerns
   - Testing instructions
   - Deploy considerations
"""
)
```

### Phase 5: Post-Merge Knowledge Capture
Extract learnings after merge:
```python
Task(
  subagent_type="sdac-knowledge-synthesizer",
  description="Extract learnings from PR",
  prompt="""
After PR merge, capture knowledge:

1. **Extract PR Learnings**
   ```bash
   # Get PR review comments
   gh pr view "$pr_number" --comments
   
   # Extract patterns from review feedback
   # Save successful patterns
   # Note improvement areas
   ```

2. **Update Knowledge Base**
   - Add new patterns discovered
   - Update coding standards based on review
   - Document architectural decisions
   - Save reusable components

3. **Cleanup Workflow**
   ```bash
   # Archive branch workspace
   tar -czf ".claude/archive/PR-${pr_number}-${branch_name}.tar.gz" "$workspace"
   
   # Delete merged branch
   git branch -d "$branch_name"
   gh pr close "$pr_number"
   
   # Update main and start fresh
   git checkout main
   git pull origin main
   ```

4. **Generate PR Summary**
   ```markdown
   ## PR #$pr_number Summary
   
   - **Feature**: $feature_name
   - **LOC**: $actual_loc (estimated: $estimated_loc)
   - **Review Time**: $review_duration
   - **Iterations**: $review_cycles
   
   ### Learnings
   - $key_learning_1
   - $key_learning_2
   
   ### Patterns Added
   - $pattern_1
   - $pattern_2
   ```
"""
)
```

## Multiple Agent Coordination

When `/sdac` runs, it coordinates multiple specialized agents:

```python
# Example: Starting a new feature
/sdac start

# Behind the scenes:
agents_running = [
    "sdac-design-questioner",     # Getting requirements
    "sdac-todo-generator",         # Creating task list
    "sdac-pr-splitter",           # Analyzing PR strategy
    "sdac-task-distributor",      # Launching implementers
    "sdac-implementer-1",         # Working on task #1
    "sdac-implementer-2",         # Working on task #3
    "sdac-implementer-3",         # Working on task #5
    "sdac-design-reconciler",     # Checking alignment
    "sdac-todo-reconciler",       # Verifying completion
]

# Real-time monitoring
/sdac status
# Shows all agent progress in unified dashboard
```

## Intelligent Agent Selection

The orchestrator automatically selects agents based on context:

```python
def select_agents(context):
    if context.feature_size == "large":
        # Use PR splitter and multiple implementers
        return [
            Task(subagent_type="sdac-pr-splitter", ...),
            Task(subagent_type="sdac-task-distributor", 
                 prompt="Launch 5-8 parallel implementers"),
        ]
    elif context.has_tests_failing:
        # Add test specialist
        return [
            Task(subagent_type="sdac-test-writer", ...),
            Task(subagent_type="sdac-implementer", ...),
        ]
    elif context.needs_documentation:
        # Include doc updater
        return [
            Task(subagent_type="sdac-doc-updater", ...),
            Task(subagent_type="sdac-implementer", ...),
        ]
```

## PR Workflow Commands

### Starting New Feature
```bash
/sdac
> "I'm on main branch. Let's create a feature!"
> "Feature name?" user-authentication
> "Creating feature/user-authentication branch..."
> "Now, what are you building?"
```

### Creating PR
```bash
/sdac pr
> "Preparing PR for feature/user-authentication"
> "✓ 15/15 tasks complete"
> "✓ All tests passing"
> "Creating PR..."
> "PR #456 created: https://github.com/..."
```

### PR Status
```bash
/sdac status
> Branch: feature/user-authentication
> PR: #456 (Draft)
> Progress: 12/15 tasks (80%)
> Reviews: 0/2 required
> Checks: 5/6 passing
```

### Post-Merge
```bash
/sdac merge
> "PR #456 was merged!"
> "Extracting learnings..."
> "✓ 3 patterns added"
> "✓ 2 rules updated"
> "✓ Docs updated"
> "Cleaning up..."
> "Ready for next feature!"
```

## PR Best Practices Integration

### Automatic PR Sizing
- Warns when PR gets too large
- Suggests splitting strategy
- Creates sub-branches automatically

### Review Optimization
- Groups related changes
- Adds helpful review comments
- Generates review guide
- Tracks review feedback

### Continuous Integration
- Runs checks before PR creation
- Updates PR status automatically
- Handles CI feedback

## Success Metrics

- **PR Size**: Average <400 LOC
- **Review Cycles**: Average <2 iterations
- **Time to Merge**: <2 days average
- **Knowledge Capture**: 100% PR learnings saved

Remember: Every PR is an opportunity to improve the codebase and share knowledge with the team!