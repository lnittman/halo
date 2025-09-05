# Output Format Specifications

## Structured JSON Output
```xml
<output format="json">
  <schema>
    {
      "analysis": {
        "summary": "string",
        "key_findings": ["string"],
        "risk_level": "low|medium|high|critical",
        "confidence": "number (0-1)"
      },
      "recommendations": {
        "immediate": ["string"],
        "short_term": ["string"],
        "long_term": ["string"]
      },
      "next_steps": {
        "action": "string",
        "rationale": "string",
        "dependencies": ["string"]
      }
    }
  </schema>
  <constraints>
    <required_fields>All fields must be present</required_fields>
    <value_types>Strict type compliance</value_types>
    <no_nulls>Use empty arrays/strings instead</no_nulls>
  </constraints>
</output>
```

## Implementation Plan Format
```xml
<implementation_plan>
  <overview>High-level approach and strategy</overview>
  <phases>
    <phase number="1">
      <name>Setup and Prerequisites</name>
      <tasks>Specific action items</tasks>
      <deliverables>Concrete outputs</deliverables>
      <duration>Time estimate</duration>
    </phase>
    <phase number="2">
      <name>Core Implementation</name>
      <tasks>Main development work</tasks>
      <deliverables>Feature completion</deliverables>
      <risks>Potential blockers</risks>
    </phase>
    <phase number="3">
      <name>Testing and Validation</name>
      <tasks>Quality assurance steps</tasks>
      <success_metrics>How to measure completion</success_metrics>
    </phase>
  </phases>
  <dependencies>External requirements</dependencies>
  <rollback_plan>How to revert if needed</rollback_plan>
</implementation_plan>
```

## Code Generation Format
```xml
<code_output>
  <language>TypeScript/Python/Go/Rust</language>
  <style_guide>
    <naming>camelCase/snake_case conventions</naming>
    <structure>Module/class organization</structure>
    <comments>When and how to comment</comments>
  </style_guide>
  <requirements>
    <type_safety>Full type annotations</type_safety>
    <error_handling>Try-catch patterns</error_handling>
    <testing>Unit test alongside</testing>
    <documentation>JSDoc/docstrings</documentation>
  </requirements>
  <delivery>
    <files>List of files to create/modify</files>
    <diff_format>Show changes clearly</diff_format>
    <test_commands>How to verify</test_commands>
  </delivery>
</code_output>
```

## Analysis Report Format
```xml
<analysis_report>
  <executive_summary>1-2 paragraph overview</executive_summary>
  <detailed_findings>
    <finding priority="high">
      <issue>Problem description</issue>
      <impact>Business/technical impact</impact>
      <evidence>Supporting data</evidence>
      <recommendation>Suggested action</recommendation>
    </finding>
  </detailed_findings>
  <metrics>
    <quantitative>Numbers, percentages, counts</quantitative>
    <qualitative>Observations, patterns</qualitative>
  </metrics>
  <action_matrix>
    <immediate>Do within 24 hours</immediate>
    <short_term>Do within 1 week</short_term>
    <long_term>Strategic improvements</long_term>
  </action_matrix>
</analysis_report>
```

## Prompt Generation Format
```xml
<generated_prompt>
  <metadata>
    <target_tool>codex|gemini|cursor|claude</target_tool>
    <complexity>simple|moderate|complex</complexity>
    <estimated_tokens>number</estimated_tokens>
  </metadata>
  <system_prompt>Tool-specific context and role</system_prompt>
  <user_prompt>Main task specification</user_prompt>
  <examples>Optional few-shot examples</examples>
  <constraints>Boundaries and requirements</constraints>
  <expected_output>What success looks like</expected_output>
</generated_prompt>
```