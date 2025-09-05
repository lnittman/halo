# XML Structure Template

## Core XML Tags for Structured Prompts

### Essential Structure
```xml
<system_context>
  <role>Define the AI's persona and expertise</role>
  <capabilities>List available tools and resources</capabilities>
  <constraints>Define boundaries and limitations</constraints>
</system_context>

<task_specification>
  <objective>Clear, specific goal statement</objective>
  <success_criteria>Measurable outcomes</success_criteria>
  <deliverables>Expected outputs and formats</deliverables>
</task_specification>

<context>
  <current_state>Present situation and relevant background</current_state>
  <previous_work>Prior attempts, learnings, or related work</previous_work>
  <dependencies>External factors or requirements</dependencies>
</context>

<instructions>
  <step>Numbered, explicit action items</step>
  <decision_points>Where judgment or selection is needed</decision_points>
  <error_handling>How to handle edge cases</error_handling>
</instructions>

<examples>
  <example>
    <input>Sample input</input>
    <reasoning>Step-by-step thought process</reasoning>
    <output>Expected result</output>
  </example>
</examples>

<output_specification>
  <format>JSON, Markdown, Code, etc.</format>
  <structure>Exact schema or template</structure>
  <constraints>Length, style, tone requirements</constraints>
</output_specification>
```

### Advanced Patterns
```xml
<thinking_framework>
  <analysis_phase>Break down the problem</analysis_phase>
  <planning_phase>Design the solution</planning_phase>
  <execution_phase>Implement the plan</execution_phase>
  <verification_phase>Validate the results</verification_phase>
</thinking_framework>

<quality_control>
  <requirements>Must-have elements</requirements>
  <validation>How to check correctness</validation>
  <iteration>When to refine or retry</iteration>
</quality_control>
```

## Best Practices
1. **Consistency** - Use same tag names throughout
2. **Hierarchy** - Nest tags logically: `<outer><inner></inner></outer>`
3. **Clarity** - Tag names should describe content
4. **Reference** - Refer to tags explicitly: "Using the context in <context> tags..."
5. **Modularity** - Each tag serves one clear purpose