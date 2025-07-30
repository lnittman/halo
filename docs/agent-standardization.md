# 🔧 Agent Standardization Guide

This guide standardizes how agents follow component patterns from the command system, ensuring consistency across the halo ecosystem.

## 🎯 Core Principles

### 1. Component-Based Architecture
Like commands, agents should be composed of standardized sections:
- **Header**: Name, description, tools
- **Directive**: Core personality and capabilities
- **Process Patterns**: Structured workflows
- **Output Template**: Consistent reporting format
- **Integration Points**: How they connect with other agents

### 2. Structured Thinking
Agents should show their reasoning process transparently:

```xml
<agent_thinking>
  <understanding_phase>
    What I need to do: {{task_interpretation}}
    Available tools: {{tool_analysis}}
    Context awareness: {{relevant_context}}
  </understanding_phase>
  
  <analysis_phase>
    Approaches considered: {{options}}
    Selected approach: {{choice}}
    Rationale: {{reasoning}}
  </analysis_phase>
  
  <execution_phase>
    Steps to take: {{plan}}
    Expected outcomes: {{predictions}}
    Verification method: {{checks}}
  </execution_phase>
</agent_thinking>
```

### 3. Universal Input Handling
Agents should process various input types intelligently:

```yaml
input_handlers:
  urls_detected:
    - fetch and analyze content
    - extract relevant patterns
    - apply to current task
  
  code_detected:
    - parse language and structure
    - identify patterns and issues
    - adapt to project style
  
  files_detected:
    - read and understand context
    - extract actionable items
    - maintain consistency
  
  mixed_content:
    - separate by type
    - process each appropriately
    - synthesize insights
```

## 📋 Standard Agent Structure

### Required Sections (in order)

```markdown
---
name: agent-name
description: use PROACTIVELY when [trigger condition]. [core capability description].
tools: [comma-separated tool list]
---

## 🦊 agent personality
[opening statement establishing the agent's expertise and approach]

## 🎯 core capabilities
### capability group 1
- specific ability
- specific ability
- specific ability

### capability group 2
- specific ability
- specific ability

## 🔄 operational patterns
### pattern name
```[code/yaml/bash]
structured approach
```

## 📋 output template
### standard report format
```markdown
[consistent output structure]
```

## 🔗 integration points
### handoff to: [agent-name]
- when: [condition]
- data: [what's passed]

### receives from: [agent-name]
- expects: [data format]
- action: [what to do]

## 🎨 best practices
- principle 1
- principle 2
- principle 3

[closing statement reinforcing agent's mission]
```

## 🔄 Thinking Process Integration

### Before Major Operations
```typescript
// Agent should "think aloud" before complex tasks
interface AgentThinking {
  understanding: {
    task: string;
    constraints: string[];
    resources: string[];
  };
  approach: {
    options: ApproachOption[];
    selected: string;
    rationale: string;
  };
  risks: {
    identified: Risk[];
    mitigation: string[];
  };
}
```

### During Execution
```yaml
execution_feedback:
  - "Analyzing {{current_file}}..."
  - "Found {{pattern_count}} instances"
  - "Applying {{selected_fix}}..."
  - "Verifying changes..."
```

## 📊 Output Standardization

### Status Indicators
```javascript
const agentIndicators = {
  // Analysis states
  analyzing: '🔍',
  found: '💡',
  warning: '⚠️',
  error: '❌',
  success: '✅',
  
  // Progress states
  starting: '🚀',
  processing: '⚙️',
  completing: '🏁',
  
  // Health scores
  excellent: '🟢',
  good: '🟡',
  poor: '🔴'
};
```

### Report Sections
Every agent report should include:
1. **Header**: Clear title with emoji
2. **Metadata**: Timestamp, scope, status
3. **Summary**: Key findings/actions at a glance
4. **Details**: Structured breakdown
5. **Recommendations**: Actionable next steps
6. **Footer**: Attribution and context

## 🔗 Inter-Agent Communication

### Handoff Protocol
```yaml
handoff_standard:
  from_agent: 
    prepare:
      - summarize findings
      - package relevant data
      - suggest next actions
    
  to_agent:
    receive:
      - acknowledge handoff
      - validate data format
      - confirm understanding
    
  shared_context:
    - session state
    - project understanding
    - user preferences
```

### Data Passing Format
```typescript
interface AgentHandoff {
  from: string;
  to: string;
  timestamp: string;
  context: {
    task: string;
    findings: any[];
    recommendations: string[];
  };
  data: {
    files: string[];
    metrics: Record<string, any>;
    flags: string[];
  };
}
```

## 🎮 Command Integration

### Agents Called by Commands
```yaml
command_integration:
  /build:
    may_invoke:
      - test-coverage (after implementation)
      - lint-fix (for cleanup)
      - git-commit (when complete)
  
  /audit:
    may_invoke:
      - audit-codebase (for analysis)
      - dependency-doctor (for packages)
      - test-coverage (for coverage)
  
  /vision:
    may_invoke:
      - tech-researcher (for capabilities)
      - pattern-extractor (for examples)
```

## 📈 Quality Metrics

### Agent Performance Standards
- **Response Time**: < 30s for analysis, < 2m for generation
- **Accuracy**: 95%+ for pattern detection
- **Completeness**: All sections of template filled
- **Actionability**: Every report includes next steps
- **Consistency**: Same input = similar output

### Self-Assessment
Agents should periodically assess their own performance:
```yaml
self_assessment:
  check_output_quality:
    - follows_template: boolean
    - includes_all_sections: boolean
    - actionable_recommendations: count
  
  check_integration:
    - clean_handoffs: boolean
    - data_validation: boolean
    - context_preservation: boolean
```

## 🚀 Migration Guide

### For Existing Agents
1. **Audit Current Structure**: Compare against standard
2. **Add Missing Sections**: Thinking process, integration points
3. **Standardize Output**: Use consistent template
4. **Test Integration**: Verify handoffs work
5. **Update Documentation**: Reflect new patterns

### Checklist for Standardization
- [ ] Has proper YAML frontmatter
- [ ] Includes personality statement
- [ ] Shows thinking process
- [ ] Has operational patterns section
- [ ] Includes output template
- [ ] Defines integration points
- [ ] Uses consistent status indicators
- [ ] Follows naming conventions
- [ ] Includes best practices
- [ ] Has closing mission statement

## 🔮 Future Enhancements

### Planned Improvements
- Automated agent testing framework
- Performance profiling tools
- Integration test suite
- Visual agent network diagram
- Agent capability matrix

### Research Areas
- Multi-agent collaboration patterns
- Parallel agent execution
- Agent learning from outcomes
- Cross-session agent memory
- Agent specialization evolution

---

*This guide ensures all halo agents follow consistent patterns, making them predictable, composable, and powerful.*