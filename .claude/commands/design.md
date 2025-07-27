---
allowed-tools: Task, TodoWrite, Read, Write
description: Advanced design creation with persistent Q&A and intelligent refinement
argument-hint: [start|qa|refine|status]
---

# /design - Intelligent Design Creation System

Transform any context into comprehensive design documents through advanced Q&A orchestration.

## Enhanced Execution Framework

### Phase 1: Intelligent Context Analysis
Task(
  subagent_type="sdac-design-questioner",
  description="Analyze context with advanced pattern recognition",
  prompt="""
Analyze provided context using sophisticated extraction:

1. **Multi-Source Context Processing**
   - Meeting notes: Extract decisions, concerns, requirements
   - Slack threads: Identify consensus, debates, decisions
   - Specs: Parse formal requirements and constraints
   - Emails: Extract commitments and clarifications
   - Code comments: Understand technical context

2. **Intelligent Requirement Extraction**
   ```python
   def extract_requirements(context):
       explicit_reqs = parse_stated_requirements(context)
       implicit_reqs = infer_unstated_requirements(context)
       constraints = identify_constraints(context)
       assumptions = surface_hidden_assumptions(context)
       
       return synthesize_requirements(
           explicit_reqs, implicit_reqs, 
           constraints, assumptions
       )
   ```

3. **Strategic Question Generation**
   - Identify critical unknowns blocking implementation
   - Surface hidden complexity early
   - Clarify ambiguous terminology
   - Validate assumptions explicitly

4. **Adaptive Q&A Strategy**
   - Start with highest-impact questions
   - Adjust based on answer patterns
   - Know when to mark "TBD during implementation"
   - Balance thoroughness with progress

Continue asking until design is implementation-ready.
"""
)

### Phase 2: Deep Dive Refinement
Task(
  subagent_type="sdac-design-questioner",
  description="Persistent refinement through intelligent Q&A",
  prompt="""
Execute sophisticated design refinement:

1. **Domain-Specific Deep Dives**
   ```yaml
   technical_questions:
     - Architecture: Service boundaries, data flow, APIs
     - Performance: Latency requirements, throughput, scale
     - Security: Auth, encryption, compliance needs
     - Integration: External systems, protocols, formats
   
   business_questions:
     - Users: Personas, workflows, pain points
     - Value: Success metrics, ROI, priorities  
     - Constraints: Timeline, budget, resources
     - Future: Extensibility, migration, growth
   ```

2. **Intelligent Follow-ups**
   - Never accept vague answers
   - Drill down on "it depends" responses
   - Quantify qualitative requirements
   - Challenge implicit assumptions

3. **Design Pattern Matching**
   - Recognize common patterns
   - Suggest proven solutions
   - Identify anti-patterns early
   - Learn from past designs

4. **Completeness Validation**
   - Check all scenarios covered
   - Verify error paths defined
   - Ensure NFRs specified
   - Validate acceptance criteria

Keep refining until ambiguity is minimized.
"""
)

### Phase 3: Design Document Assembly
Task(
  subagent_type="general-purpose",
  description="Assemble comprehensive design document",
  prompt="""
Create structured design document with:

1. **Executive Summary**
   - Problem statement
   - Solution overview
   - Key benefits
   - Success metrics

2. **Detailed Requirements**
   - Functional requirements (user stories)
   - Non-functional requirements (performance, security)
   - Constraints and assumptions
   - Out of scope items

3. **Technical Architecture**
   ```
   ┌─────────────────────────────────┐
   │      Component Diagram          │
   ├─────────────────────────────────┤
   │  - Services and boundaries      │
   │  - Data flow and storage        │
   │  - External integrations        │
   │  - Security boundaries          │
   └─────────────────────────────────┘
   ```

4. **Implementation Guidance**
   - Suggested approach
   - Key technical decisions
   - Risk mitigation strategies
   - TBD items for implementation phase

5. **Validation Criteria**
   - Acceptance tests
   - Performance benchmarks
   - Security requirements
   - Quality gates

Save as structured markdown for todo generation.
"""
)

### Phase 4: Intelligent Todo Preparation
Task(
  subagent_type="general-purpose",
  description="Optimize design for todo generation",
  prompt="""
Prepare design for optimal todo generation:

1. **Task Extraction Hints**
   - Mark clear implementation boundaries
   - Identify parallel work opportunities
   - Highlight dependencies explicitly
   - Estimate complexity indicators

2. **Priority Signals**
   - Critical path items
   - Risk mitigation tasks
   - User-facing features
   - Technical debt prevention

3. **Parallelization Opportunities**
   ```yaml
   parallel_work_streams:
     - Frontend components (isolated)
     - Backend services (by domain)
     - Database changes (staged)
     - Integration tests (per feature)
   ```

4. **Success Criteria Mapping**
   - Link requirements to tasks
   - Define "done" for each component
   - Include test requirements
   - Specify quality standards

Output design ready for automatic todo generation.
"""
)

## Advanced Q&A Patterns

### Pattern 1: Clarification Cascade
```
Initial: "We need better performance"
Q1: "What specific operations need optimization?"
A1: "User search is slow"
Q2: "What's the current response time and target?"
A2: "Currently 3s, need <500ms"
Q3: "What's the data volume and growth rate?"
A3: "1M records, growing 10% monthly"
Result: Clear performance requirements with context
```

### Pattern 2: Assumption Validation
```
Statement: "Users will upload files"
Q1: "What file types and sizes?"
Q2: "What's the upload frequency?"
Q3: "Storage requirements and retention?"
Q4: "Processing needed after upload?"
Result: Complete file handling requirements
```

### Pattern 3: Edge Case Exploration
```
Feature: "User authentication"
Q1: "What about password resets?"
Q2: "Account lockout policies?"
Q3: "Multi-factor authentication?"
Q4: "Session management requirements?"
Result: Comprehensive auth specification
```

## Intelligent Design Storage

### State Management
```yaml
design_state:
  version: 1.0
  status: draft|reviewing|approved
  completeness_score: 85%
  
  sections:
    overview: complete
    requirements: complete
    architecture: in_progress
    implementation: pending
    
  open_questions:
    - id: q1
      question: "Caching strategy for search?"
      priority: high
      blocking: true
      
  decisions:
    - id: d1
      decision: "Use PostgreSQL for primary storage"
      rationale: "Team expertise, scaling needs"
      alternatives_considered: ["MongoDB", "DynamoDB"]
```

## Success Metrics

- **Ambiguity Reduction**: 90% of requirements clarified
- **Question Efficiency**: Average 10-15 high-impact questions
- **Design Completeness**: 95% ready for implementation
- **Todo Generation**: Automatic task extraction accuracy
- **Rework Prevention**: <10% design changes during implementation

## Usage Examples

### Starting from Rough Notes
```bash
/design start
# Paste: "Discussion about adding search. Should be fast. 
# Maybe use that new AI thing? John mentioned Elasticsearch"

System: Analyzing context and generating questions...
Q1: What types of content need to be searchable?
Q2: What's the expected query complexity?
[Continues until clear specification emerges]
```

### Continuous Refinement
```bash
/design qa
System: Reviewing current design for gaps...
Q: How should search results be ranked?
Q: What about search analytics requirements?
[Continues until no ambiguity remains]
```

Remember: The goal is to extract maximum clarity before implementation begins, preventing costly rework and ensuring smooth parallel execution.