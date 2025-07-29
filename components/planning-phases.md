# Planning Phases Component

Provides consistent planning patterns across all Claude Code commands that involve strategic thinking, architecture, or multi-step execution.

## Core Planning Pattern

```xml
<planning_phases>
<!-- Phase 1: Discovery -->
<discovery_phase>
  <context_gathering>
    <existing_code>
      - Analyze current codebase structure
      - Identify patterns and conventions
      - Map dependencies and relationships
    </existing_code>
    
    <requirements_extraction>
      - Explicit requirements from input
      - Implicit requirements from context
      - Constraints and limitations
    </requirements_extraction>
    
    <research_tasks>
      {{#each research_needs}}
      <research topic="{{topic}}">
        <source>{{source_type}}</source>
        <purpose>{{why_needed}}</purpose>
      </research>
      {{/each}}
    </research_tasks>
  </context_gathering>
  
  <discovery_summary>
    ## 📊 Discovery Findings
    
    **Current State**: {{state_summary}}
    
    **Key Requirements**: {{requirements_summary}}
    
    **Constraints**: {{constraints_summary}}
    
    **Research Insights**: {{research_summary}}
  </discovery_summary>
</discovery_phase>

<!-- Phase 2: Analysis -->
<analysis_phase>
  <options_exploration>
    {{#each options}}
    <option name="{{name}}">
      <description>{{description}}</description>
      <pros>{{pros_list}}</pros>
      <cons>{{cons_list}}</cons>
      <effort>{{effort_estimate}}</effort>
      <risk>{{risk_level}}</risk>
    </option>
    {{/each}}
  </options_exploration>
  
  <tradeoff_analysis>
    <criteria>
      - {{criterion_1}}: Weight {{weight_1}}
      - {{criterion_2}}: Weight {{weight_2}}
      - {{criterion_3}}: Weight {{weight_3}}
    </criteria>
    
    <scoring>
      {{#each options}}
      <option name="{{name}}" score="{{total_score}}">
        {{#each criteria_scores}}
        <criterion name="{{name}}" score="{{score}}"/>
        {{/each}}
      </option>
      {{/each}}
    </scoring>
  </tradeoff_analysis>
  
  <recommendation>
    <selected_option>{{best_option}}</selected_option>
    <rationale>{{why_selected}}</rationale>
    <runner_up>{{second_best}}</runner_up>
  </recommendation>
</analysis_phase>

<!-- Phase 3: Design -->
<design_phase>
  <architecture_design>
    <high_level>
      {{architecture_overview}}
    </high_level>
    
    <components>
      {{#each components}}
      <component name="{{name}}">
        <purpose>{{purpose}}</purpose>
        <interfaces>{{interfaces}}</interfaces>
        <dependencies>{{dependencies}}</dependencies>
      </component>
      {{/each}}
    </components>
    
    <data_flow>
      {{data_flow_description}}
    </data_flow>
  </architecture_design>
  
  <implementation_strategy>
    <approach>{{selected_approach}}</approach>
    <phases>
      {{#each phases}}
      <phase number="{{num}}">
        <name>{{name}}</name>
        <deliverables>{{deliverables}}</deliverables>
        <duration>{{duration}}</duration>
      </phase>
      {{/each}}
    </phases>
  </implementation_strategy>
  
  <success_criteria>
    {{#each criteria}}
    <criterion priority="{{priority}}">
      <description>{{description}}</description>
      <measurement>{{how_measured}}</measurement>
      <target>{{target_value}}</target>
    </criterion>
    {{/each}}
  </success_criteria>
</design_phase>

<!-- Phase 4: Planning Output -->
<planning_output>
  ## 📋 Implementation Plan
  
  ### Selected Approach
  **{{approach_name}}**
  
  {{approach_description}}
  
  ### Architecture
  ```
  {{architecture_diagram}}
  ```
  
  ### Implementation Phases
  {{#each phases}}
  
  #### Phase {{number}}: {{name}} ({{duration}})
  **Deliverables**:
  {{#each deliverables}}
  - {{deliverable}}
  {{/each}}
  
  **Key Tasks**:
  {{#each tasks}}
  - [ ] {{task}}
  {{/each}}
  {{/each}}
  
  ### Success Metrics
  {{#each metrics}}
  - **{{name}}**: {{target}} ({{measurement}})
  {{/each}}
  
  ### Risk Mitigation
  {{#each risks}}
  - **Risk**: {{risk}} → **Mitigation**: {{mitigation}}
  {{/each}}
</planning_output>
</planning_phases>
```

## Command-Specific Planning Variants

### For Creative Commands (vision, brand)
```xml
<creative_planning>
  <inspiration_phase>
    <mood_board>{{inspiration_sources}}</mood_board>
    <design_principles>{{principles}}</design_principles>
    <emotional_targets>{{feelings}}</emotional_targets>
  </inspiration_phase>
  
  <concept_development>
    {{#each concepts}}
    <concept name="{{name}}">
      <description>{{description}}</description>
      <visual_language>{{visuals}}</visual_language>
      <experience_flow>{{flow}}</experience_flow>
    </concept>
    {{/each}}
  </concept_development>
</creative_planning>
```

### For Technical Commands (build, create)
```xml
<technical_planning>
  <feasibility_check>
    <technical_requirements>{{requirements}}</technical_requirements>
    <available_resources>{{resources}}</available_resources>
    <skill_gaps>{{gaps}}</skill_gaps>
  </feasibility_check>
  
  <technical_design>
    <stack_selection>{{selected_stack}}</stack_selection>
    <api_design>{{api_structure}}</api_design>
    <database_schema>{{schema}}</database_schema>
    <security_model>{{security}}</security_model>
  </technical_design>
</technical_planning>
```

### For Analysis Commands (docaudit, prime)
```xml
<analytical_planning>
  <scope_definition>
    <included>{{what_to_analyze}}</included>
    <excluded>{{what_to_skip}}</excluded>
    <depth>{{analysis_depth}}</depth>
  </scope_definition>
  
  <analysis_framework>
    <dimensions>{{analysis_dimensions}}</dimensions>
    <metrics>{{metrics_to_collect}}</metrics>
    <comparison_baseline>{{baseline}}</comparison_baseline>
  </analysis_framework>
</analytical_planning>
```

## Planning Quality Indicators

```xml
<quality_indicators>
  <completeness>
    - [ ] All requirements addressed
    - [ ] All constraints considered
    - [ ] All risks identified
    - [ ] All dependencies mapped
  </completeness>
  
  <clarity>
    - [ ] Clear success criteria
    - [ ] Measurable outcomes
    - [ ] Unambiguous tasks
    - [ ] Defined timelines
  </clarity>
  
  <feasibility>
    - [ ] Realistic estimates
    - [ ] Available resources
    - [ ] Manageable complexity
    - [ ] Acceptable risk level
  </feasibility>
</quality_indicators>
```

## Planning State Persistence

```json
{
  "planning_history": [
    {
      "command": "create",
      "timestamp": "ISO_8601",
      "planning_type": "technical",
      "selected_approach": "approach_name",
      "phases": ["phase1", "phase2", "phase3"],
      "estimated_effort": "days",
      "actual_effort": "days",
      "outcome": "success|partial|pivoted"
    }
  ],
  "planning_patterns": {
    "successful_approaches": [],
    "avoided_pitfalls": [],
    "refined_estimates": {}
  }
}
```

## Integration Guidelines

### Placement
1. After thinking blocks
2. Before verification phase
3. Can be iterative for complex planning

### Depth Control
```javascript
// Adjust planning depth based on complexity
const planningDepth = {
  simple: ['discovery', 'design'],
  moderate: ['discovery', 'analysis', 'design'],
  complex: ['discovery', 'analysis', 'design', 'validation']
};
```

## Best Practices

1. **Progressive Elaboration**: Start high-level, add detail as needed
2. **Option Exploration**: Always consider multiple approaches
3. **Risk-First Thinking**: Identify and address risks early
4. **Measurable Outcomes**: Define clear success criteria
5. **Iterative Refinement**: Plans can evolve with new information

## Anti-Patterns

- ❌ Analysis paralysis - planning forever
- ❌ Over-detailed initial plans
- ❌ Ignoring constraints until late
- ❌ Planning without research
- ❌ Rigid plans that can't adapt