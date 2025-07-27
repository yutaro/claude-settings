---
allowed-tools: Task, TodoWrite, Read, Write, Bash
description: Advanced design creation with branch workspace management
argument-hint: [start|qa|refine|status]
---

# /design - Intelligent Design Creation System

Transform any context into comprehensive design documents with automatic branch workspace setup.

## Usage

```bash
/design start   # Start from any context (auto-creates workspace)
/design qa      # Continue Q&A refinement until design is complete
/design refine  # Further improve existing design
/design status  # Check design completeness and workspace
```

## Main Execution Flow

When you run `/design`, it orchestrates specialized agents:

```python
# Main orchestration logic
if args == "start":
    # Step 1: Setup workspace and analyze context
    Task(
        subagent_type="sdac-design-questioner",
        description="Begin design creation",
        prompt="Setup branch workspace, analyze context, start Q&A process"
    )
    
elif args == "qa":
    # Step 2: Continue Q&A refinement
    Task(
        subagent_type="sdac-design-questioner",
        description="Continue design refinement",
        prompt="Load current design, ask deeper questions, update workspace"
    )
    
elif args == "refine":
    # Step 3: Polish and finalize
    Task(
        subagent_type="general-purpose",
        description="Finalize design document",
        prompt="Structure design properly, save to workspace, prepare for todos"
    )
    
elif args == "status":
    # Check design status
    Task(
        subagent_type="general-purpose",
        description="Check design status",
        prompt="Show workspace status, design completeness, and next steps"
    )
```

## Enhanced Execution Framework

### Phase 0: Workspace Setup (Automatic)
```bash
# Automatically executed before design creation
current_branch=$(git branch --show-current)
parent_branch=$(git show-branch -a | grep '\*' | grep -v "$current_branch" | head -n1 | sed 's/.*\[\(.*\)\].*/\1/')

# Create branch workspace
mkdir -p ".claude/pr/${current_branch}"

# For sub-branches, maintain hierarchy
if [[ "$current_branch" == *"/"* ]]; then
  parent_part=$(echo "$current_branch" | cut -d'/' -f1)
  mkdir -p ".claude/pr/${parent_part}/${current_branch}"
fi

# Initialize workspace files
touch ".claude/pr/${current_branch}/design-docs.md"
touch ".claude/pr/${current_branch}/todo.md"
echo '{"status": "design", "created": "'$(date -Iseconds)'"}' > ".claude/pr/${current_branch}/status.json"
```

### Phase 1: Intelligent Context Analysis
Task(
  subagent_type="sdac-design-questioner",
  description="Analyze context and setup workspace",
  prompt="""
First, setup the branch workspace:

1. **Get Git Information**
   ```bash
   # Get current branch
   current_branch=$(git branch --show-current)
   
   # Get parent branch (if exists)
   parent_branch=$(git show-branch -a | grep '\*' | grep -v "$current_branch" | head -n1 | sed 's/.*\[\(.*\)\].*/\1/')
   
   # Create workspace directory
   mkdir -p ".claude/pr/${current_branch}"
   ```

2. **Analyze Provided Context**
   - Meeting notes: Extract decisions, concerns, requirements
   - Slack threads: Identify consensus, debates, decisions
   - Specs: Parse formal requirements and constraints
   - Emails: Extract commitments and clarifications

3. **Strategic Question Generation**
   - Identify critical unknowns blocking implementation
   - Surface hidden complexity early
   - Clarify ambiguous terminology
   - Validate assumptions explicitly

4. **Save to Branch Workspace**
   - Write initial design to `.claude/pr/${current_branch}/design-docs.md`
   - Track status in `.claude/pr/${current_branch}/status.json`
   - Note parent branch relationship if applicable

Continue asking questions until design is implementation-ready.
"""
)

### Phase 2: Deep Dive Refinement
Task(
  subagent_type="sdac-design-questioner",
  description="Persistent refinement with workspace updates",
  prompt="""
Continue refining the design with workspace awareness:

1. **Load Current Design**
   ```bash
   current_branch=$(git branch --show-current)
   design_file=".claude/pr/${current_branch}/design-docs.md"
   ```

2. **Domain-Specific Deep Dives**
   - Architecture: Service boundaries, data flow, APIs
   - Performance: Latency requirements, throughput, scale
   - Security: Auth, encryption, compliance needs
   - Integration: External systems, protocols, formats

3. **Update Design Document**
   - Save iterations to branch workspace
   - Track design evolution in status.json
   - Maintain version history

4. **Branch Relationship Awareness**
   - If sub-branch, check parent design for context
   - Ensure alignment with parent branch goals
   - Note any divergences or specializations

Keep refining until ambiguity is minimized.
"""
)

### Phase 3: Design Document Finalization
Task(
  subagent_type="general-purpose",
  description="Finalize design in branch workspace",
  prompt="""
Finalize the design document with proper organization:

1. **Structure Design Document**
   ```markdown
   # [Feature Name] Design Document
   
   ## Branch Information
   - Current Branch: [branch-name]
   - Parent Branch: [parent-branch]
   - Created: [timestamp]
   
   ## Overview
   [Problem statement and solution overview]
   
   ## Requirements
   ### Functional Requirements
   - [Specific requirements]
   
   ### Non-Functional Requirements
   - Performance: [metrics]
   - Security: [requirements]
   - Scale: [expectations]
   
   ## Technical Design
   [Architecture, data models, APIs]
   
   ## Implementation Plan
   - Estimated tasks: [count]
   - Suggested parallelism: [1-8 workers]
   - PR splitting strategy: [if needed]
   ```

2. **Save to Branch Workspace**
   ```bash
   current_branch=$(git branch --show-current)
   
   # Save design
   cat > ".claude/pr/${current_branch}/design-docs.md"
   
   # Update status
   jq '.status = "design-complete" | .design_completed = "'$(date -Iseconds)'"' \
     ".claude/pr/${current_branch}/status.json" > tmp.json && mv tmp.json ".claude/pr/${current_branch}/status.json"
   ```

3. **Prepare for Todo Generation**
   - Mark implementation boundaries
   - Identify parallel work opportunities
   - Note dependencies
   - Estimate complexity

Design is now ready for todo generation.
"""
)

## Branch Workspace Management

### Automatic Features
1. **Workspace Creation**
   - Creates `.claude/pr/[branch]/` on design start
   - Maintains parent-child relationships
   - Initializes required files

2. **Status Tracking**
   ```json
   {
     "status": "design|todo|implementing|complete",
     "created": "2024-01-27T10:00:00Z",
     "design_completed": "2024-01-27T11:00:00Z",
     "parent_branch": "main",
     "stats": {
       "total_questions": 15,
       "clarifications": 12,
       "tbd_items": 3
     }
   }
   ```

3. **Branch Hierarchy**
   ```
   .claude/pr/
   ├── main/
   │   └── feature-auth/
   │       ├── design-docs.md
   │       ├── todo.md
   │       └── status.json
   ├── feature-auth/
   │   ├── design-docs.md
   │   ├── todo.md
   │   ├── status.json
   │   └── auth-oauth/
   │       ├── design-docs.md
   │       ├── todo.md
   │       └── status.json
   ```

## GitHub Integration

### Branch Information Commands
```bash
# Get current branch
git branch --show-current

# Get parent branch
git show-branch -a | grep '\*' | grep -v "$(git branch --show-current)" | head -n1 | sed 's/.*\[\(.*\)\].*/\1/'

# Get branch hierarchy
git branch -a --contains HEAD

# Get remote tracking branch
git rev-parse --abbrev-ref --symbolic-full-name @{u}
```

### PR Context Integration
```bash
# If PR exists, get additional context
gh pr view --json title,body,labels,milestone

# Get related issues
gh pr view --json linkedIssues

# Get review comments for context
gh pr view --json reviews
```

## Success Metrics

- **Workspace Organization**: All designs in proper branch folders
- **Branch Awareness**: Parent-child relationships maintained
- **Context Preservation**: Design decisions tracked per branch
- **GitHub Integration**: Automatic PR/issue context inclusion

## Usage Examples

### New Feature Branch
```bash
git checkout -b feature-payment
/design start
# Automatically creates .claude/pr/feature-payment/
# Asks questions about payment feature
# Saves design to branch workspace
```

### Sub-feature Branch
```bash
git checkout -b feature-payment/stripe-integration
/design start
# Creates nested workspace
# Inherits context from parent branch
# Maintains relationship in status.json
```

Remember: Every branch gets its own workspace, maintaining clear separation of concerns and enabling parallel development.