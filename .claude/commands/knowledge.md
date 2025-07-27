---
allowed-tools: Task, Read, Write, Grep
description: Comprehensive knowledge management for docs, rules, and patterns
argument-hint: [update|sync|learn|status]
---

# /knowledge - Intelligent Knowledge Management System

Automatically maintain documentation, rules, and patterns to ensure knowledge accumulates and evolves.

## Core Functions

### 1. Documentation Management
```bash
/knowledge update docs    # Update all documentation
/knowledge update api     # Update API docs only
/knowledge update guides  # Update user guides
```

### 2. Rule Evolution
```bash
/knowledge update rules   # Generate/update coding rules
/knowledge rules status   # Check rule effectiveness
/knowledge rules sync     # Sync rules from patterns
```

### 3. Pattern Learning
```bash
/knowledge learn          # Extract patterns from recent code
/knowledge learn pr 123   # Learn from specific PR
/knowledge patterns       # View discovered patterns
```

### 4. Full Synchronization
```bash
/knowledge sync          # Complete knowledge base update
/knowledge status        # Knowledge health check
```

## Automated Knowledge Accumulation

### Phase 1: Documentation Auto-Update
Task(
  subagent_type="sdac-doc-updater",
  description="Automatically update documentation",
  prompt="""
Systematically update all documentation to stay current:

1. **Change Detection**
   - Scan for API changes since last update
   - Identify new features and components
   - Find deprecated or removed functionality
   - Detect behavioral changes

2. **Documentation Updates**
   - API Reference: Update endpoints, parameters, responses
   - Architecture Docs: Reflect design evolution
   - Guides: Update examples and procedures
   - Troubleshooting: Add new issues and solutions

3. **File Organization**
   ```
   .claude/docs/
   ├── architecture/
   │   ├── system-overview.md
   │   ├── component-design.md
   │   └── data-flow.md
   ├── api/
   │   ├── rest-api.md
   │   ├── graphql-schema.md
   │   └── webhooks.md
   ├── guides/
   │   ├── getting-started.md
   │   ├── deployment.md
   │   └── migration.md
   └── patterns/
       ├── success-patterns.md
       ├── anti-patterns.md
       └── best-practices.md
   ```

4. **Quality Assurance**
   - Test all code examples
   - Verify links and references
   - Check for completeness
   - Ensure consistency

Save all updates with clear versioning and changelog.
"""
)

### Phase 2: Rule Generation & Evolution
Task(
  subagent_type="sdac-pattern-learner",
  description="Generate and evolve coding rules",
  prompt="""
Transform learned patterns into enforceable rules:

1. **Pattern Analysis**
   - Extract patterns from successful implementations
   - Identify common mistakes and anti-patterns
   - Analyze team coding preferences
   - Study performance optimizations

2. **Rule Creation**
   - Convert patterns to specific rules
   - Set severity levels (error/warning/info)
   - Create fix suggestions
   - Add code examples

3. **Rule Organization**
   ```
   .claude/rules/
   ├── code-quality/
   │   ├── naming-conventions.md
   │   ├── function-complexity.md
   │   └── documentation.md
   ├── security/
   │   ├── input-validation.md
   │   ├── authentication.md
   │   └── secrets-handling.md
   ├── performance/
   │   ├── query-optimization.md
   │   ├── caching-rules.md
   │   └── async-patterns.md
   └── testing/
       ├── coverage-requirements.md
       ├── test-patterns.md
       └── mock-guidelines.md
   ```

4. **Rule Evolution**
   - Track rule effectiveness
   - Update based on violations
   - Remove ineffective rules
   - Add new rules from learnings

Create actionable, team-specific rules that improve code quality.
"""
)

### Phase 3: Pattern Learning & Storage
Task(
  subagent_type="sdac-pattern-learner",
  description="Extract and store reusable patterns",
  prompt="""
Continuously learn from implementations:

1. **Pattern Extraction**
   - Analyze recent implementations
   - Identify successful code structures
   - Extract architectural patterns
   - Find optimization techniques

2. **Pattern Categorization**
   ```json
   {
     "patterns": {
       "architectural": [
         {
           "name": "Repository Pattern",
           "context": "Data access layer",
           "implementation": "...",
           "benefits": ["testability", "flexibility"],
           "examples": ["user-repository.ts"]
         }
       ],
       "performance": [
         {
           "name": "Batch Processing",
           "context": "Large data operations",
           "technique": "Process in chunks of 1000",
           "improvement": "3x faster",
           "code": "..."
         }
       ],
       "error-handling": [...],
       "testing": [...]
     }
   }
   ```

3. **Anti-Pattern Documentation**
   - Common mistakes found
   - Why they're problematic
   - How to fix them
   - Prevention strategies

4. **Knowledge Persistence**
   - Save to `.claude/knowledge/patterns.json`
   - Update `.claude/docs/patterns/`
   - Generate rules from patterns
   - Create reusable templates

Build a growing library of team-specific patterns.
"""
)

### Phase 4: Knowledge Integration
Task(
  subagent_type="sdac-knowledge-synthesizer",
  description="Integrate all knowledge sources",
  prompt="""
Synthesize knowledge from all sources:

1. **Knowledge Aggregation**
   - Combine learnings from implementations
   - Integrate PR feedback and reviews
   - Include test results and metrics
   - Add team discussions and decisions

2. **Cross-Reference Creation**
   - Link patterns to rules
   - Connect docs to examples
   - Map problems to solutions
   - Create knowledge graph

3. **Actionable Insights**
   - Generate improvement recommendations
   - Identify training needs
   - Suggest process optimizations
   - Highlight recurring issues

4. **Knowledge Distribution**
   - Update all relevant documentation
   - Create quick reference guides
   - Generate team notifications
   - Export shareable insights

Ensure knowledge is accessible and actionable.
"""
)

## Automatic Triggers

### Continuous Learning Hooks
```python
# After each implementation
def post_implementation_hook():
    extract_patterns()
    update_relevant_docs()
    check_rule_violations()
    
# After PR merge
def post_pr_merge_hook():
    analyze_pr_changes()
    update_api_docs()
    extract_learnings()
    generate_new_rules()
    
# Weekly scheduled
def weekly_knowledge_sync():
    full_documentation_update()
    pattern_analysis()
    rule_effectiveness_review()
    knowledge_report_generation()
```

## Knowledge Persistence Structure

### Documentation Storage
```
.claude/docs/
├── README.md                 # Auto-generated index
├── CHANGELOG.md             # Document version history
├── architecture/            # System design docs
├── api/                    # API documentation
├── guides/                 # User guides
├── patterns/              # Pattern library
└── troubleshooting/       # Known issues & solutions
```

### Rule Storage
```
.claude/rules/
├── .ruleset.json          # Rule configuration
├── code-quality/          # Code standards
├── security/              # Security rules
├── performance/           # Performance rules
├── testing/               # Test requirements
└── custom/                # Project-specific rules
```

### Pattern Storage
```
.claude/knowledge/
├── patterns.json          # Pattern database
├── anti-patterns.json     # What to avoid
├── learnings.json         # Extracted insights
├── metrics.json           # Effectiveness data
└── templates/             # Reusable code templates
```

## Success Metrics

### Documentation Health
- **Coverage**: >95% of public APIs documented
- **Currency**: <1 week since last update
- **Accuracy**: 100% examples tested
- **Completeness**: All features documented

### Rule Effectiveness
- **Violation Reduction**: >70% decrease
- **False Positive Rate**: <5%
- **Auto-Fix Success**: >80%
- **Team Adoption**: >90%

### Learning Velocity
- **Patterns/Week**: >5 new patterns
- **Rule Generation**: >2 new rules/week
- **Knowledge Queries**: >20/week
- **Reuse Rate**: >50% pattern adoption

## Usage Examples

### Daily Workflow Integration
```bash
# After completing feature
/knowledge learn --recent
# Extracts patterns from recent work

# Before starting new feature
/knowledge search "api client"
# Finds relevant patterns and examples

# After PR merge
/knowledge update docs --pr 123
# Updates docs based on PR changes
```

### Maintenance Tasks
```bash
# Weekly sync
/knowledge sync
# Full knowledge base update

# Monthly review
/knowledge status --detailed
# Comprehensive knowledge health check

# Quarterly cleanup
/knowledge prune --outdated
# Remove obsolete knowledge
```

Remember: Knowledge that isn't captured is knowledge lost. This system ensures every implementation contributes to collective intelligence.