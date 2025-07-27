# SDAC - Spec Driven Agentic Coding

Transform your development workflow with intelligent AI agents that design, build, and test software systematically. 

## 🚀 Quick Start

```bash
git clone https://github.com/yutaro/claude-settings.git /tmp/sdac
mkdir -p ~/.claude/commands ~/.claude/agents
cp -n /tmp/sdac/.claude/commands/*.md ~/.claude/commands/
cp -n /tmp/sdac/.claude/agents/*.md ~/.claude/agents/
rm -rf /tmp/sdac
```

That's it! SDAC handles everything: design, implementation, testing, and quality checks.

## 📋 Commands 

### Core Workflow
- `/design [start|refine|status]` - Complete design workflow
- `/todo` - Generate tasks with PR splitting strategy
- `/implement [parallel N|sequential|status]` - Scalable implementation (3-8 workers)

### Quality & Knowledge
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

- **Smart PR Management** - Automatically splits large features into reviewable chunks
- **Parallel Development** - 3-8 agents working simultaneously without conflicts
- **Just 6 Commands** - Simple interface to powerful agent orchestration
- **Continuous Learning** - Extracts patterns from PRs to improve over time

## 🔄 Development Workflow

1. **Design** → `/design` - Create specifications
2. **Plan** → `/todo` - Generate tasks  
3. **Build** → `/implement` - Parallel execution
4. **Test** → `/test` - Ensure quality
5. **Learn** → `/knowledge` - Extract patterns

## 💡 Best Practices

### Smart Design Process
```bash
/design
# Automatically:
# - Sets up workspace
# - Creates comprehensive design
# - Analyzes PR splitting needs
# - Suggests parallelism level
```

### Scalable Implementation
```bash
/implement parallel 6
# Based on todo analysis:
# - 6 workers on non-conflicting tasks
# - File-level isolation
# - Real-time coordination
# - 3x faster delivery
```


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
