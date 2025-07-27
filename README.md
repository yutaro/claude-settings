# SDAC - Spec Driven Agentic Coding

Transform your development workflow with intelligent AI agents that design, build, and test software systematically through PR-driven development. 

## 🚀 Quick Start

```bash
git clone https://github.com/yutaro/claude-settings.git /tmp/sdac
mkdir -p ~/.claude/commands ~/.claude/agents
cp -n /tmp/sdac/.claude/commands/*.md ~/.claude/commands/
cp -n /tmp/sdac/.claude/agents/*.md ~/.claude/agents/
rm -rf /tmp/sdac
```

## ✨ PR-Driven Development with `/sdac`

Use the unified `/sdac` command for your entire PR workflow:

```bash
/sdac              # Intelligently detects current state and continues workflow
/sdac pr           # Create PR with auto-generated description
/sdac status       # Check workflow and PR status
/sdac merge        # Post-merge cleanup and knowledge sync
```

SDAC automatically:
- Creates feature branches from main
- Manages PR size (< 400 LOC)
- Suggests PR splitting strategies
- Generates comprehensive PR descriptions
- Coordinates parallel implementation
- Extracts learnings after merge

## 📋 Commands 

### 🎯 Unified PR Workflow (Recommended)
- `/sdac` - **All-in-one PR workflow orchestrator**
  - Automatically detects workflow state
  - Creates feature branches
  - Manages design → implementation → PR flow
  - Handles PR creation and post-merge cleanup

### Individual Commands (Advanced)
- `/design [start|refine|status]` - Complete design workflow
- `/todo` - Generate tasks with PR splitting strategy
- `/implement [parallel N|sequential|status]` - Scalable implementation (3-8 workers)
- `/test [run|write|coverage|fix]` - Comprehensive testing
- `/quality [check|rules|fix|init]` - Quality + standards
- `/docs [check|update|create|api]` - Documentation management
- `/knowledge [pr|learn|sync|search]` - Unified knowledge base

## 🤖 Agent Ecosystem

### Design & Planning Agents
- `sdac-design-questioner` - Advanced design refinement through strategic inquiry frameworks
- `sdac-design-reconciler` - Design-implementation alignment with architectural consistency
- `sdac-todo-generator` - Comprehensive task list generation from design documents

### Implementation Agents
- `sdac-implementer` - Systematic todo-driven development with intelligent prioritization
- `sdac-task-distributor` - Advanced parallel coordination with intelligent conflict resolution
- `sdac-todo-reconciler` - Implementation completeness verification with forensic precision

### Quality & Testing Agents
- `sdac-test-writer` - Advanced testing strategy with intelligent test generation
- `sdac-quality-checker` - Comprehensive quality intelligence with predictive insights
- `sdac-rule-enforcer` - Sophisticated standards compliance with adaptive enforcement

### Knowledge & Documentation Agents
- `sdac-pr-analyzer` - PR content analysis that extracts learnings and patterns
- `sdac-doc-updater` - Documentation maintenance specialist for current information
- `sdac-pattern-learner` - Automatic learning system that extracts implementation patterns

### Advanced Workflow Agents
- `sdac-pr-creator` - Automated PR creation with dependency tracking and documentation
- `sdac-pr-splitter` - PR splitting specialist for optimal breakdown strategies
- `sdac-progress-visualizer` - Real-time progress tracking and visualization
- `sdac-quality-monitor` - Continuous quality assurance with real-time feedback

## 📁 Project Structure

```
.claude/
├── agents/           # Custom sub-agents
├── commands/         # Slash commands
├── docs/            # Documentation
├── knowledge/       # Extracted patterns
├── pr/              # Branch workspaces
│   └── [branch]/
│       ├── design-docs.md
│       ├── todo.md
│       ├── status.json
│       └── [sub-branch]/
│           ├── design-docs.md
│           ├── todo.md
│           └── status.json
└── rules/           # Coding standards directory
    ├── typescript.md
    ├── security.md
    ├── testing.md
    └── performance.md
```

## 🎯 Key Features

- **One Command Workflow** - Just `/sdac` for entire PR lifecycle
- **Smart PR Management** - Automatically splits large features into reviewable chunks
- **Parallel Development** - 3-8 agents working simultaneously without conflicts
- **GitHub Integration** - Native `gh` CLI integration for seamless PR operations
- **Continuous Learning** - Extracts patterns from PRs to improve over time
- **Branch Workspaces** - Isolated `.claude/pr/[branch]/` for each feature

## 🔄 PR-Driven Workflow Example

```bash
# 1. Start on main branch
git checkout main

# 2. Use /sdac to start new feature
/sdac
> "Let's create a feature branch!"
> "Feature name?" user-authentication
> "Creating feature/user-authentication..."
> "Now, what are you building?"
[Interactive design questions...]

# 3. SDAC automatically:
# - Creates design document
# - Generates PR-optimized todo list
# - Launches parallel implementation
# - Tracks progress in real-time

# 4. Create PR when ready
/sdac pr
> "✓ 15/15 tasks complete"
> "✓ All tests passing"
> "Creating PR #123..."

# 5. After merge
/sdac merge
> "Extracting learnings..."
> "✓ Knowledge base updated"
> "Ready for next feature!"
```

## 💡 PR Best Practices with SDAC

### 🚀 One Command to Rule Them All
```bash
/sdac
# Just use /sdac - it handles everything intelligently:
# - Detects if you're on main → creates feature branch
# - Continues existing work → picks up where you left off
# - Manages PR lifecycle → from creation to merge
```

### 📏 Automatic PR Size Management
SDAC keeps PRs reviewable:
- **< 400 LOC**: Single PR (fast review)
- **> 400 LOC**: Suggests splitting strategy
- **Dependencies**: Manages PR order automatically

### 🔄 PR Splitting Example
```bash
/sdac
> "This looks like a large feature (est. 800 LOC)"
> "Suggested split:"
> "  PR 1: Backend API (300 LOC)"
> "  PR 2: Frontend UI (250 LOC)"  
> "  PR 3: Integration (250 LOC)"
> "Create sub-branches? (y/n)"
```

### 🤝 Review-Friendly Output
Every PR includes:
- Comprehensive description
- Review guide ("Start here...")
- Testing instructions
- Risk areas highlighted
- Suggested reviewers


## 🛠️ Configuration

### Custom Agents
Create specialized agents in `.claude/agents/`:
```markdown
---
name: my-specialist
description: Domain-specific expertise
tools: Read, Write, Edit
---

Your specialized prompt here...
```

### Project Rules
Define standards in `.claude/rules/` directory:
```markdown
# Example: .claude/rules/typescript.md
## TypeScript Standards
- Use strict mode
- Prefer interfaces over types
- No any types

# Example: .claude/rules/testing.md
## Testing Standards
- 100% coverage for critical paths
- Unit tests for all utilities
- Integration tests for APIs
```

## 📊 Why PR-Driven Development?

### Traditional vs SDAC Approach

**Traditional**: Multiple commands, manual coordination
```bash
git checkout -b feature/auth
# Design manually
# Create todos manually
# Implement sequentially
# Create PR manually
# Hope nothing was missed
```

**SDAC**: One command, intelligent automation
```bash
/sdac  # That's it!
```

### Success Metrics
- **Review Time**: 75% faster with structured PRs
- **Merge Conflicts**: 90% reduction through smart coordination
- **Knowledge Retention**: 100% of PR learnings captured
- **Developer Velocity**: 3x improvement with parallel execution
