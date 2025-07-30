# 🔧 Agent Component Integration Guide

This guide shows how to integrate command components into agents for consistency across the halo ecosystem.

## 🎯 Component Integration Map

### Core Components for Agents

| Component | Purpose | When to Use | Integration Pattern |
|-----------|---------|-------------|-------------------|
| `@thinking-blocks` | Structured reasoning | Complex decisions, multiple approaches | Before major operations |
| `@verification-patterns` | Safety checks | Dangerous operations, state changes | Before execution |
| `@output-standards` | Consistent output | All agent reports | In output template |
| `@planning-phases` | Structured planning | Multi-step operations | In operational patterns |
| `@xml-transformer` | Input parsing | Complex user requests | In input handlers |
| `@session-state` | Context persistence | Cross-agent workflows | For handoffs |

## 📋 Integration Template

```markdown
---
name: agent-name
description: use PROACTIVELY when [trigger]. [capability summary].
tools: [tool-list]
---

[personality statement]

<components>
  <use>@thinking-blocks</use>
  <use>@verification-patterns</use>
  <use>@output-standards</use>
  <!-- Add others as needed -->
</components>

## 🦊 core capabilities
[capabilities section]

## 🔄 operational patterns

### [pattern name]
<thinking_process>
<!-- Use thinking-blocks structure -->
<understanding_phase>
What I understand: [interpretation]
Requirements: [extracted needs]
</understanding_phase>

<analysis_phase>
Options: [approaches considered]
Selected: [chosen approach]
Rationale: [why this way]
</analysis_phase>

<planning_phase>
Steps: [execution plan]
</planning_phase>
</thinking_process>

```[code]
[implementation]
```

### [verification pattern]
<verification_phase>
<!-- Use verification-patterns -->
<safety_check>
What will change: [impacts]
Risk level: [assessment]
</safety_check>

<confirmation>
Proceeding with: [action]
Expected outcome: [result]
</confirmation>
</verification_phase>

## 📋 output template
<!-- Use output-standards formatting -->
[standard report structure with emojis and sections]

## 🔗 integration points
[handoff patterns]

## 🎨 best practices
[principles]

[closing statement]
```

## 🔄 Component Usage by Agent Type

### 🔍 Analyzer Agents (Read-Only)
```yaml
required_components:
  - "@thinking-blocks": For analysis reasoning
  - "@output-standards": For consistent reports
  
optional_components:
  - "@xml-transformer": For complex input parsing
  - "@verification-patterns": For validating findings
  
example_agents:
  - audit-codebase
  - pattern-extractor
  - tech-researcher
```

### 🏗️ Builder Agents (Read-Write)
```yaml
required_components:
  - "@thinking-blocks": For implementation decisions
  - "@verification-patterns": For safe execution
  - "@planning-phases": For structured building
  - "@output-standards": For progress reports
  
optional_components:
  - "@session-state": For complex workflows
  - "@xml-transformer": For requirement parsing
  
example_agents:
  - motion-expert
  - video-studio
  - 3d-artist
```

### 🔗 Integration Agents (Service-Specific)
```yaml
required_components:
  - "@thinking-blocks": For workflow decisions
  - "@verification-patterns": For API safety
  - "@output-standards": For status reports
  - "@session-state": For maintaining context
  
optional_components:
  - "@planning-phases": For complex operations
  
example_agents:
  - linear-whisperer
  - github-whisperer
  - cloudflare-whisperer
```

## 📊 Component Integration Examples

### Thinking Blocks in Action
```typescript
// Before complex operation
interface AgentThinking {
  understanding: {
    task: "Create smooth scroll animation",
    constraints: ["Performance", "Accessibility"],
    tools: ["Framer Motion", "Lenis"]
  },
  analysis: {
    options: [
      { name: "CSS-only", pros: ["No JS"], cons: ["Limited"] },
      { name: "Lenis", pros: ["Smooth"], cons: ["Bundle size"] },
      { name: "Framer", pros: ["Flexible"], cons: ["Complexity"] }
    ],
    selected: "Lenis",
    rationale: "Best performance with smoothness"
  }
}
```

### Verification Patterns
```yaml
before_deployment:
  checks:
    - All tests passing
    - No console errors
    - Bundle size acceptable
    - Performance metrics met
  
  risk_assessment:
    changes: "New animation library"
    impact: "Medium - affects UX"
    rollback: "Feature flag ready"
  
  approval:
    automated: true
    criteria: "All checks green"
```

### Output Standards Application
```markdown
## ✅ Animation System Implemented

**Components**: 12 created  
**Performance**: 60fps maintained  
**Bundle Impact**: +12kb  
**Accessibility**: ✅ Respects prefers-reduced-motion  

### 📊 Implementation Details
- Lenis for smooth scroll
- Framer Motion for component animations
- GPU-accelerated transforms only
- Lazy-loaded animation chunks

**Next**: [TEST] [DEPLOY] [DOCUMENT]
```

## 🚀 Migration Checklist

For each agent:

### 1. Add Component Declaration
```xml
<components>
  <use>@thinking-blocks</use>
  <use>@verification-patterns</use>
  <use>@output-standards</use>
</components>
```

### 2. Integrate Thinking Process
- Add `<thinking_process>` blocks before complex operations
- Show understanding, analysis, and planning phases
- Make reasoning transparent

### 3. Add Verification Steps
- Include `<verification_phase>` for state changes
- Check safety before dangerous operations
- Confirm expected outcomes

### 4. Standardize Output
- Use emoji-rich headers
- Consistent status indicators
- Structured sections
- Clear next steps

### 5. Test Integration
- Verify component usage
- Check output formatting
- Test handoff patterns
- Validate thinking display

## 📈 Quality Metrics

### Component Integration Score
```yaml
scoring:
  has_components_declaration: 20%
  uses_thinking_blocks: 20%
  includes_verification: 20%
  follows_output_standards: 20%
  proper_integration: 20%
  
target: 90%+ for all agents
```

### Integration Health Checks
- Components properly declared
- Thinking process visible
- Verification prevents errors
- Output consistently formatted
- Handoffs preserve context

## 🔮 Advanced Patterns

### Conditional Component Loading
```xml
<components>
  <use>@thinking-blocks</use>
  <use when="complex_task">@extended-thinking</use>
  <use when="dangerous_op">@verification-patterns</use>
  <use>@output-standards</use>
</components>
```

### Component Composition
```typescript
// Combining multiple components
const executeWithComponents = async (task: Task) => {
  // Thinking phase
  const thinking = await generateThinking(task);
  
  // Verification phase
  const verified = await verifyApproach(thinking);
  
  // Execution with standards
  const result = await execute(verified);
  
  // Standardized output
  return formatOutput(result);
};
```

## 🎯 Next Steps

1. **Audit Current Agents**: Check component usage
2. **Prioritize Updates**: Start with most-used agents
3. **Apply Templates**: Use standardized structure
4. **Test Integration**: Verify components work together
5. **Document Changes**: Update agent docs

---

*This guide ensures all agents leverage the power of command components for consistency and quality.*