---
allowed-tools: Task, TodoWrite
description: Complete SDAC workflow with intelligent orchestration
argument-hint: [start|status|design|implement|monitor]
---

# /sdac - Streamlined Development with Autonomous Coordination

Execute the complete workflow from initial context through parallel implementation with intelligent orchestration.

## Usage

```bash
/sdac start   # Begin with meeting notes/specs/context
/sdac status  # Check current workflow stage
/sdac monitor # Real-time progress monitoring
```

## Complete Workflow Process

**Step 1: Context → Design (Iterative Q&A)**
```bash
/sdac design
# Paste meeting notes, specs, Slack threads
# Answer questions until design is complete
```

**Step 2: Design → Todo List**
```bash
/sdac
# Generates prioritized task list from design
# Reviews for completeness and dependencies
```

**Step 3: Todo → Parallel Implementation**
```bash
/sdac implement
# Launches 3 parallel agents:
# - Implementation Agent (building)
# - Design Reconciler (alignment)
# - Todo Reconciler (verification)
```

**Step 4: Monitor & Guide**
```bash
/sdac monitor
# Watch progress, answer questions
# Light review as needed
```

**Step 5: Completion**
- All todos verified complete
- Design and implementation aligned
- Ready for final review

## Key Workflow Principles

1. **Embrace Incomplete Input**
   - Meeting notes can be rough
   - Specs can have gaps
   - Q&A process fills in details

2. **Trust the Process**
   - Design questioner will ask what's needed
   - Todo generator creates comprehensive lists
   - Reconcilers catch issues

3. **Parallel Efficiency**
   - 3 agents work simultaneously
   - Implementation doesn't wait for perfection
   - Continuous reconciliation

4. **Pragmatic Progress**
   - "TBD during implementation" is OK
   - Design evolves with implementation
   - Focus on working software

## Intelligent Orchestration Features

### Adaptive Agent Selection
- Analyzes project complexity
- Selects optimal number of agents (1-8)
- Maps capabilities to requirements
- Plans coordination patterns

### Smart Conflict Resolution
- Predictive conflict detection
- Automatic resolution for simple conflicts
- Human escalation for complex issues
- Learning from conflict patterns

### Real-time Progress Dashboard
```
╔════════════════════════════════════════════╗
║          SDAC Execution Monitor            ║
╠════════════════════════════════════════════╣
║ Design Phase    [████████████░░] 80%       ║
║ Todo Generation [████████████████] 100%    ║
║ Implementation  [██████░░░░░░░░] 40%       ║
║                                            ║
║ Active Agents: 3/5                         ║
║ ├─ sdac-implementer-1: Task #3 (60%)      ║
║ ├─ sdac-implementer-2: Task #5 (30%)      ║
║ └─ sdac-reconciler: Continuous            ║
║                                            ║
║ Conflicts: 0 | Blocked: 1 | Complete: 7   ║
╚════════════════════════════════════════════╝
```

### Work Distribution Intelligence
- Analyzes task dependencies
- Optimizes parallel execution
- Dynamic load balancing
- Handles blockages gracefully

## Example Flow

```markdown
User: /sdac start
[Pastes rough meeting notes about new feature]

System: Starting design phase...
Q: What specific user types need access?
Q: Should this integrate with existing auth?
[Continues Q&A until design complete]

System: Design complete. Generating todos...
[Creates 15 prioritized tasks]

System: Starting parallel implementation...
Agent 1: Implementing task #1...
Agent 2: Reviewing design compliance...
Agent 3: Verifying completed tasks...

User: [Answers clarification questions]
[Reviews progress periodically]

System: Implementation complete!
- 15/15 todos verified complete
- Design updated with 3 improvements
- All tests passing
```

## Advanced Strategies

### When to Use Multiple Agents
- Complex features with many independent parts
- Time-critical implementations
- Large refactoring projects
- Features requiring different expertise areas

### Communication Patterns
- **Pipeline**: Sequential task dependencies
- **Fork-Join**: Parallel work with merge points
- **Publish-Subscribe**: Real-time updates
- **Leader-Follower**: Complex coordination

### Error Recovery
- Automatic retry for transient failures
- Graceful degradation strategies
- Human escalation when needed
- Learning from failure patterns

## Success Indicators

- **Clear Design**: Q&A eliminates ambiguity
- **Accurate Todos**: Comprehensive task list
- **Quality Implementation**: Working, tested code
- **Verified Completion**: No false completions
- **Design Alignment**: Architecture maintained
- **Efficiency Gain**: 3-5x faster than sequential

## Tips for Best Results

1. **Provide Context Freely**
   - Include meeting notes, Slack threads, specs
   - Don't worry about organization
   - Let the Q&A process structure it

2. **Answer Questions Thoughtfully**
   - Take time to consider design questions
   - "I don't know" is a valid answer
   - Suggest exploring during implementation

3. **Monitor Without Micromanaging**
   - Check progress periodically
   - Answer blocking questions quickly
   - Trust the reconciliation process

4. **Review at Natural Points**
   - After design completion
   - When conflicts arise
   - At implementation milestones
   - Before final completion

Remember: SDAC transforms rough ideas into working software through intelligent coordination and continuous reconciliation.