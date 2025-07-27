---
allowed-tools: Task, TodoWrite, Read, Write, Bash
description: Advanced parallel implementation with intelligent orchestration
argument-hint: [start|status|reconcile|optimize]
---

# /implement - Intelligent Parallel Implementation System

Execute sophisticated parallel implementation with dynamic agent orchestration and continuous reconciliation.

## Advanced Execution Architecture

### Dynamic Agent Orchestration
```python
def orchestrate_implementation(design_complexity, todo_count):
    # Intelligent agent configuration
    if todo_count < 5:
        return SingleAgentExecution()
    elif todo_count < 15:
        return TripleAgentParallel()  # Your proven pattern
    elif todo_count < 30:
        return ScaledParallelExecution(agents=5)
    else:
        return DistributedExecution(agents=8, coordinators=2)
```

## Core 3-Agent Parallel Pattern (Your Workflow)

### Agent 1: Primary Implementer
Task(
  subagent_type="sdac-implementer",
  description="Execute implementation with intelligent progress tracking",
  prompt="""
Execute implementation with sophisticated coordination:

1. **Intelligent Task Selection**
   ```python
   def select_next_task(todos, context):
       # Priority-based selection
       high_priority = filter_high_priority(todos)
       
       # Dependency analysis
       ready_tasks = filter_ready_tasks(high_priority)
       
       # Conflict avoidance
       non_conflicting = avoid_active_conflicts(ready_tasks)
       
       return select_optimal_task(non_conflicting)
   ```

2. **Implementation Excellence**
   - Read design section thoroughly
   - Analyze existing patterns
   - Implement complete functionality
   - Include comprehensive error handling
   - Write production-ready code

3. **Progress Communication Protocol**
   ```yaml
   progress_updates:
     task_start:
       - task_id: current
       - estimated_time: calculated
       - dependencies: identified
       
     progress_checkpoint:
       - completion: percentage
       - blockers: identified
       - next_milestone: planned
       
     task_complete:
       - implementation: verified
       - tests: status
       - integration: checked
   ```

4. **Intelligent Blocker Handling**
   - Identify blocker type (technical/requirement/dependency)
   - Attempt resolution strategies
   - Escalate with context if needed
   - Continue with non-blocked tasks

Maintain continuous progress with clear communication.
"""
)

### Agent 2: Design-Implementation Reconciler
Task(
  subagent_type="sdac-design-reconciler",
  description="Continuous alignment with intelligent decision-making",
  prompt="""
Monitor implementation alignment with sophisticated analysis:

1. **Real-time Alignment Monitoring**
   ```python
   def monitor_alignment(implementation_stream, design_spec):
       while implementation_active:
           changes = detect_implementation_changes()
           
           for change in changes:
               alignment = analyze_design_compliance(change, design_spec)
               
               if alignment.deviation_detected:
                   decision = make_reconciliation_decision(
                       deviation_type=alignment.type,
                       impact_level=alignment.impact,
                       implementation_quality=alignment.quality
                   )
                   
                   execute_reconciliation(decision)
   ```

2. **Intelligent Decision Framework**
   ```yaml
   decision_matrix:
     implementation_superior:
       action: update_design
       when: 
         - Better performance achieved
         - Simpler solution found
         - Maintains all requirements
         
     design_critical:
       action: fix_implementation
       when:
         - Architectural boundary violated
         - Security requirement missed
         - Core principle compromised
         
     pragmatic_compromise:
       action: document_deviation
       when:
         - 90% compliance achieved
         - Full compliance too costly
         - Can address in phase 2
   ```

3. **Continuous Design Evolution**
   - Track implementation insights
   - Update design documentation
   - Maintain architectural integrity
   - Document decision rationale

4. **Proactive Conflict Prevention**
   - Identify potential misalignments early
   - Suggest course corrections
   - Prevent architectural drift
   - Maintain quality standards

Balance ideal design with practical implementation.
"""
)

### Agent 3: Todo-Implementation Verifier
Task(
  subagent_type="sdac-todo-reconciler",
  description="Ruthless verification with intelligent gap detection",
  prompt="""
Verify implementation completeness with forensic precision:

1. **Multi-Layer Verification Protocol**
   ```python
   def verify_todo_completion(todo, implementation):
       verification_layers = {
           'existence': check_code_exists(todo, implementation),
           'completeness': check_functionality_complete(todo, implementation),
           'integration': check_integration_working(todo, implementation),
           'quality': check_quality_standards(todo, implementation),
           'testing': check_test_coverage(todo, implementation)
       }
       
       return aggregate_verification_results(verification_layers)
   ```

2. **Common Incompleteness Patterns**
   ```yaml
   detection_patterns:
     surface_implementation:
       - Function signatures without logic
       - TODO comments in code
       - Stub returns without processing
       
     missing_error_handling:
       - No try-catch blocks
       - Happy path only
       - No validation logic
       
     incomplete_integration:
       - Hardcoded values
       - Missing configuration
       - Incomplete API calls
   ```

3. **Intelligent Gap Analysis**
   - Compare todo requirements vs implementation
   - Identify missing functionality
   - Detect partial implementations
   - Find hidden dependencies

4. **Accurate Status Management**
   ```python
   def update_todo_status(todo, verification_result):
       if verification_result.fully_complete:
           todo.status = 'completed'
           todo.verified_at = timestamp()
       
       elif verification_result.partially_complete:
           todo.status = 'in_progress'
           todo.completion = verification_result.percentage
           create_subtasks_for_gaps(verification_result.gaps)
       
       else:
           todo.status = 'pending'
           todo.false_completion = True
           alert_implementation_agent(todo.id)
   ```

Ensure real completion, not just claimed completion.
"""
)

## Advanced Coordination Patterns

### Pattern 1: Intelligent Work Distribution
```yaml
work_distribution:
  spatial_isolation:
    - Assign by file/module boundaries
    - Prevent file-level conflicts
    - Enable true parallelism
    
  temporal_coordination:
    - Stagger dependent tasks
    - Pipeline integration work
    - Batch similar changes
    
  capability_matching:
    - Match task complexity to agent strength
    - Distribute by domain expertise
    - Balance cognitive load
```

### Pattern 2: Continuous State Synchronization
```python
class StateCoordinator:
    def __init__(self):
        self.design_state = VersionedState()
        self.todo_state = VersionedState()
        self.implementation_state = VersionedState()
    
    def synchronize(self):
        # Vector clock synchronization
        changes = self.detect_state_changes()
        
        # Conflict-free merge
        merged_state = self.crdt_merge(changes)
        
        # Broadcast updates
        self.broadcast_state_update(merged_state)
```

### Pattern 3: Adaptive Execution Strategy
```python
def adapt_execution_strategy(metrics):
    if metrics.conflict_rate > 0.1:
        # Too many conflicts, increase isolation
        return increase_spatial_isolation()
    
    elif metrics.idle_time > 0.2:
        # Agents waiting, improve distribution
        return optimize_work_distribution()
    
    elif metrics.rework_rate > 0.15:
        # Quality issues, increase verification
        return strengthen_verification()
    
    else:
        # Running well, try to optimize further
        return increase_parallelism()
```

## Intelligent Progress Monitoring

### Real-time Execution Dashboard
```markdown
## Implementation Progress

### Overall Status
- Design Completeness: ████████████████████ 100%
- Todo Generation: ████████████████████ 100%
- Implementation: ████████████░░░░░░░░ 65%
- Verification: ████████░░░░░░░░░░░░ 40%

### Active Agents (3/3)
1. **Implementer**
   - Current: Task #7 (Authentication middleware)
   - Progress: 75% complete
   - Status: Writing error handlers
   - ETA: 15 minutes

2. **Design Reconciler**
   - Monitoring: Continuous
   - Alignments: 12 verified, 2 updated
   - Issues: None critical
   
3. **Todo Verifier**
   - Verified: 8/15 tasks
   - Issues Found: 2 incomplete
   - Status: Checking task #6

### Execution Metrics
- Parallel Efficiency: 87%
- Conflict Rate: 2%
- Rework Rate: 5%
- Quality Score: 9.2/10
```

### Intelligent Alerting System
```python
def monitor_execution_health(agents, metrics):
    alerts = []
    
    # Blocker detection
    if any(agent.blocked for agent in agents):
        alerts.append(create_blocker_alert(agent))
    
    # Performance degradation
    if metrics.velocity < historical_average * 0.8:
        alerts.append(create_performance_alert(metrics))
    
    # Quality concerns
    if metrics.verification_failure_rate > 0.2:
        alerts.append(create_quality_alert(metrics))
    
    return prioritize_alerts(alerts)
```

## Error Recovery & Resilience

### Intelligent Failure Handling
```python
def handle_agent_failure(agent, context):
    failure_type = diagnose_failure(agent)
    
    if failure_type == 'transient':
        # Retry with backoff
        return retry_with_exponential_backoff(agent)
    
    elif failure_type == 'resource':
        # Reallocate resources
        return reallocate_and_restart(agent)
    
    elif failure_type == 'logic':
        # Rollback and reassign
        rollback_changes(agent.completed_work)
        return reassign_to_different_agent(agent.current_task)
    
    else:
        # Escalate for human intervention
        return escalate_with_context(agent, context)
```

### Checkpoint & Recovery System
```yaml
checkpointing:
  automatic_checkpoints:
    - Every 5 completed tasks
    - Before high-risk operations
    - After successful integrations
    
  checkpoint_contents:
    - All agent states
    - Completed work artifacts
    - Current todo status
    - Design evolution history
    
  recovery_strategies:
    - Resume from last checkpoint
    - Selective work replay
    - Parallel path exploration
```

## Success Optimization

### Continuous Learning System
```python
def learn_from_execution(execution_history):
    patterns = extract_execution_patterns(execution_history)
    
    # Learn optimal configurations
    optimal_agent_count = learn_agent_scaling(patterns)
    optimal_batch_size = learn_task_batching(patterns)
    optimal_sync_frequency = learn_sync_timing(patterns)
    
    # Update execution strategies
    update_orchestration_config({
        'agent_count': optimal_agent_count,
        'batch_size': optimal_batch_size,
        'sync_frequency': optimal_sync_frequency
    })
    
    # Share learnings
    persist_learnings_for_future_runs(patterns)
```

## Usage Examples

### Standard 3-Agent Execution
```bash
/implement start
# Launches your proven 3-agent pattern
# Implementer + Design Reconciler + Todo Verifier
# Optimal for most features
```

### Scaled Execution for Large Features
```bash
/implement start scale=5
# Launches 5 implementers + reconciliation agents
# For features with 30+ todos
# Automatic conflict prevention
```

### Recovery from Interruption
```bash
/implement status
# Shows current progress and agent states

/implement resume
# Resumes from last checkpoint
# Redistributes incomplete work
# Maintains quality standards
```

Remember: The sophistication is in the coordination, not the complexity. Your 3-agent pattern is proven—we're making it smarter, not more complicated.