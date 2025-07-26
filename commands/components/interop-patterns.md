# Interoperability Patterns Component

Defines how Claude Code commands work together seamlessly, sharing context, building on each other's outputs, and creating coherent workflows.

## Command Interoperability Matrix

```yaml
command_relationships:
  prime:
    provides: ["project_context", "current_state", "patterns"]
    consumes: []
    naturally_leads_to: ["create", "build", "vision"]
    
  create:
    provides: ["project_structure", "implementation_plan", "architecture"]
    consumes: ["project_context", "patterns"]
    naturally_leads_to: ["build", "vision", "design"]
    
  build:
    provides: ["implemented_features", "code_changes", "test_results"]
    consumes: ["implementation_plan", "project_structure", "previous_builds"]
    naturally_leads_to: ["build", "docaudit", "brand"]
    
  vision:
    provides: ["creative_concepts", "ai_features", "design_philosophy"]
    consumes: ["project_context", "user_intent"]
    naturally_leads_to: ["design", "create", "build"]
    
  design:
    provides: ["design_system", "ui_patterns", "component_library"]
    consumes: ["creative_concepts", "project_structure"]
    naturally_leads_to: ["build", "brand"]
    
  brand:
    provides: ["brand_identity", "production_readiness", "launch_plan"]
    consumes: ["design_system", "project_context", "vision"]
    naturally_leads_to: ["build", "docaudit"]
    
  multitask:
    provides: ["agent_plans", "task_decomposition", "dependency_matrix"]
    consumes: ["project_context", "complexity_analysis"]
    naturally_leads_to: ["build", "create"]
    
  docaudit:
    provides: ["documentation_gaps", "improvement_plan", "quality_metrics"]
    consumes: ["project_structure", "existing_docs"]
    naturally_leads_to: ["build", "create"]
    
  diagram:
    provides: ["visual_architecture", "flow_diagrams", "relationships"]
    consumes: ["project_structure", "system_design"]
    naturally_leads_to: ["docaudit", "vision"]
```

## Context Passing Patterns

### Forward Context Propagation
```xml
<context_propagation>
  <!-- From prime to other commands -->
  <prime_output>
    <project_understanding>
      <architecture>{{architecture_type}}</architecture>
      <tech_stack>{{technologies}}</tech_stack>
      <patterns>{{detected_patterns}}</patterns>
    </project_understanding>
  </prime_output>
  
  <!-- Consumed by create -->
  <create_input>
    <from_prime>
      <use_architecture>{{architecture_type}}</use_architecture>
      <follow_patterns>{{detected_patterns}}</follow_patterns>
      <align_with_stack>{{technologies}}</align_with_stack>
    </from_prime>
  </create_input>
  
  <!-- Which feeds into build -->
  <build_input>
    <from_create>
      <implementation_plan>{{plan}}</implementation_plan>
      <project_structure>{{structure}}</project_structure>
    </from_create>
    <from_prime>
      <conventions>{{coding_conventions}}</conventions>
    </from_prime>
  </build_input>
</context_propagation>
```

### Bidirectional Enhancement
```xml
<bidirectional_flow>
  <!-- Vision enhances create -->
  <vision_to_create>
    <creative_features>{{ai_native_features}}</creative_features>
    <design_principles>{{principles}}</design_principles>
  </vision_to_create>
  
  <!-- Create enhances vision -->
  <create_to_vision>
    <technical_constraints>{{constraints}}</technical_constraints>
    <implementation_reality>{{feasibility}}</implementation_reality>
  </create_to_vision>
</bidirectional_flow>
```

## Command Chaining Patterns

### Sequential Chain
```javascript
// Natural progression workflow
const sequentialChain = {
  workflow: "new_project",
  steps: [
    { command: "prime", purpose: "understand_context" },
    { command: "vision", purpose: "explore_possibilities" },
    { command: "create", purpose: "plan_implementation" },
    { command: "build", purpose: "execute_plan" },
    { command: "docaudit", purpose: "ensure_quality" }
  ]
};
```

### Iterative Chain
```javascript
// Build-test-improve cycle
const iterativeChain = {
  workflow: "feature_development",
  steps: [
    { command: "build", iteration: 1 },
    { command: "build", iteration: 2, input: "test results" },
    { command: "build", iteration: 3, input: "user feedback" },
    { command: "brand", input: "prepare for release" }
  ]
};
```

### Parallel Chain
```javascript
// Multiple aspects simultaneously
const parallelChain = {
  workflow: "full_system_design",
  parallel_tracks: [
    { track: "technical", commands: ["create", "multitask", "build"] },
    { track: "creative", commands: ["vision", "design", "brand"] },
    { track: "quality", commands: ["prime", "docaudit", "diagram"] }
  ],
  convergence: "build"
};
```

## Shared State Schema

```typescript
interface SharedCommandState {
  // Project Context (from prime)
  project: {
    name: string;
    type: string;
    stack: string[];
    patterns: Pattern[];
    conventions: Convention[];
  };
  
  // Creative Vision (from vision/design)
  creative: {
    philosophy: string;
    principles: string[];
    features: AIFeature[];
    aesthetics: DesignLanguage;
  };
  
  // Implementation (from create/build)
  implementation: {
    architecture: Architecture;
    plan: ImplementationPlan;
    progress: Progress;
    blockers: Blocker[];
  };
  
  // Quality (from docaudit/diagram)
  quality: {
    documentation_coverage: number;
    test_coverage: number;
    code_quality: Metrics;
    diagrams: Diagram[];
  };
}
```

## Context Resolution Strategies

### Priority-Based Resolution
```javascript
// When multiple commands provide same context type
function resolveContext(contextType, sources) {
  const priority = {
    'architecture': ['create', 'multitask', 'prime'],
    'patterns': ['prime', 'design', 'vision'],
    'features': ['vision', 'create', 'build'],
    'quality': ['docaudit', 'build', 'prime']
  };
  
  return selectByPriority(contextType, sources, priority);
}
```

### Timestamp-Based Resolution
```javascript
// Prefer most recent context
function resolveByRecency(contexts) {
  return contexts.sort((a, b) => 
    new Date(b.timestamp) - new Date(a.timestamp)
  )[0];
}
```

### Merge Strategy
```javascript
// Combine complementary contexts
function mergeContexts(contexts) {
  return {
    ...deepMerge(contexts),
    _sources: contexts.map(c => c.source),
    _merged_at: new Date().toISOString()
  };
}
```

## Command Handoff Patterns

### Explicit Handoff
```xml
<command_handoff>
  <!-- Create hands off to build -->
  <create_output>
    <handoff_to_build>
      <ready_to_implement>
        <phase>1</phase>
        <tasks>{{phase_1_tasks}}</tasks>
        <entry_point>{{suggested_file}}</entry_point>
        <first_command>npm init</first_command>
      </ready_to_implement>
    </handoff_to_build>
  </create_output>
  
  <!-- Build receives handoff -->
  <build_input>
    <from_create_handoff>
      <continue_from>{{phase}}</continue_from>
      <execute_tasks>{{tasks}}</execute_tasks>
    </from_create_handoff>
  </build_input>
</command_handoff>
```

### Implicit Handoff
```javascript
// Commands automatically detect relevant context
function detectRelevantContext(command, sessionState) {
  const relevanceMap = {
    'build': ['create.plan', 'vision.features', 'prime.patterns'],
    'design': ['vision.aesthetics', 'create.structure', 'brand.identity'],
    'docaudit': ['build.changes', 'create.architecture', 'prime.docs']
  };
  
  return filterRelevantContext(sessionState, relevanceMap[command]);
}
```

## Workflow Templates

### New Project Workflow
```yaml
new_project_workflow:
  name: "Complete New Project"
  description: "From idea to running application"
  steps:
    - command: "vision"
      input: "initial idea"
      output: "refined concept"
    - command: "create"
      input: "vision output"
      output: "project structure"
    - command: "design"
      input: "creative direction"
      output: "design system"
    - command: "build"
      input: "implementation plan"
      output: "working application"
    - command: "brand"
      input: "prepare for launch"
      output: "production ready"
```

### Enhancement Workflow
```yaml
enhancement_workflow:
  name: "Add Major Feature"
  description: "Add significant new capability"
  steps:
    - command: "prime"
      input: "current state"
      output: "context loaded"
    - command: "vision"
      input: "feature idea"
      output: "feature design"
    - command: "multitask"
      input: "complex feature"
      output: "agent breakdown"
    - command: "build"
      input: "implement agents"
      output: "feature complete"
```

## Best Practices

1. **Context Preservation**: Never lose context between commands
2. **Smart Defaults**: Use previous command output as next input
3. **Clear Handoffs**: Make command transitions obvious
4. **Workflow Awareness**: Suggest natural next commands
5. **State Hygiene**: Clean up irrelevant context

## Anti-Patterns

- ❌ Forcing unnatural command sequences
- ❌ Losing context between commands
- ❌ Circular dependencies
- ❌ Overloading session with all context
- ❌ Ignoring user's workflow preferences