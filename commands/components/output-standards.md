# Output Standards Component

Ensures consistent, professional output formatting across all Claude Code commands with standardized sections, visual hierarchy, and session integration.

## Core Output Structure

```xml
<standardized_output>
<!-- Header Section -->
<output_header>
## {{emoji}} {{command_title}}: {{specific_context}}

{{#if subtitle}}
*{{subtitle}}*
{{/if}}
</output_header>

<!-- Summary Section -->
<executive_summary>
### 📊 Summary
{{#if one_line_summary}}
**In a nutshell**: {{one_line_summary}}
{{/if}}

**What happened**: {{action_summary}}

**Key outcomes**:
{{#each key_outcomes}}
- {{outcome}}
{{/each}}

{{#if important_note}}
**Important**: {{important_note}}
{{/if}}
</executive_summary>

<!-- Details Section -->
<detailed_results>
### 📋 Details

{{#each detail_sections}}
#### {{section_title}}
{{section_content}}

{{#if has_code}}
```{{language}}
{{code_content}}
```
{{/if}}

{{#if has_list}}
{{#each list_items}}
- {{item}}
{{/each}}
{{/if}}
{{/each}}
</detailed_results>

<!-- Action Items Section -->
<action_items>
### ✅ Action Items
{{#if immediate_actions}}
**Immediate**:
{{#each immediate_actions}}
- [ ] {{action}}
{{/each}}
{{/if}}

{{#if next_steps}}
**Next Steps**:
{{#each next_steps}}
- [ ] {{step}}
{{/each}}
{{/if}}

{{#if future_considerations}}
**Future Considerations**:
{{#each future_considerations}}
- {{consideration}}
{{/each}}
{{/if}}
</action_items>

<!-- Resources Section -->
<resources_section>
{{#if has_resources}}
### 🔗 Resources
{{#if created_files}}
**Created Files**:
{{#each created_files}}
- `{{path}}` - {{description}}
{{/each}}
{{/if}}

{{#if modified_files}}
**Modified Files**:
{{#each modified_files}}
- `{{path}}` - {{changes}}
{{/each}}
{{/if}}

{{#if external_resources}}
**References**:
{{#each external_resources}}
- [{{title}}]({{url}})
{{/each}}
{{/if}}
{{/if}}
</resources_section>

<!-- Next Commands Section -->
<next_commands>
### 🚀 What's Next?

{{#if natural_progression}}
**Natural progression**:
`{{next_command}}` - {{why_this_next}}
{{/if}}

**Other options**:
{{#each command_suggestions}}
- `{{command}}` - {{description}}
{{/each}}

{{#if continuation_tip}}
💡 **Tip**: {{continuation_tip}}
{{/if}}
</next_commands>

<!-- Footer Section -->
<output_footer>
---
{{#if session_active}}
*Session: {{session_id}} | Commands: {{command_count}} | Context: {{context_level}}*
{{else}}
*{{timestamp}} | {{command}} | {{status}}*
{{/if}}
</output_footer>
</standardized_output>
```

## Command-Specific Templates

### Planning Commands (create, multitask, vision)
```xml
<planning_output>
## {{emoji}} {{command_title}}

### 💡 Concept
{{concept_summary}}

### 📐 Architecture
{{#if has_diagram}}
```
{{architecture_diagram}}
```
{{else}}
{{architecture_description}}
{{/if}}

### 📅 Implementation Plan
{{#each phases}}
**Phase {{number}}: {{name}}** ({{duration}})
{{description}}
{{#each tasks}}
- [ ] {{task}}
{{/each}}
{{/each}}

### 📊 Metrics
{{metrics_table}}

### 🎯 Success Criteria
{{success_criteria}}
</planning_output>
```

### Execution Commands (build, prime)
```xml
<execution_output>
## {{emoji}} {{command_title}}

### ⚡ Execution Summary
**Completed**: {{what_was_done}}
**Duration**: {{execution_time}}
**Status**: {{status_indicator}}

### 📝 Changes Made
{{#each changes}}
#### {{change_category}}
{{change_description}}
{{#if has_diff}}
```diff
{{diff_content}}
```
{{/if}}
{{/each}}

### 🧪 Verification
{{verification_results}}

### 🎉 Ready to Use
```bash
{{usage_command}}
```
</execution_output>
```

### Analysis Commands (docaudit, diagram)
```xml
<analysis_output>
## {{emoji}} {{command_title}}

### 🔍 Analysis Results
{{analysis_summary}}

### 📊 Findings
{{#each findings}}
**{{finding_category}}**:
- Current state: {{current}}
- Ideal state: {{ideal}}
- Gap: {{gap}}
- Recommendation: {{recommendation}}
{{/each}}

### 📈 Metrics
{{metrics_visualization}}

### 💡 Insights
{{key_insights}}

### 🛠️ Improvements
{{improvement_plan}}
</analysis_output>
```

## Visual Hierarchy Standards

### Emoji Usage Guide
```javascript
const emojiMap = {
  // Commands
  'prime': '🚀',
  'create': '✨',
  'build': '🔨',
  'vision': '🧘',
  'design': '🎨',
  'brand': '💎',
  'multitask': '🤖',
  'docaudit': '📚',
  'diagram': '📐',
  
  // Sections
  'summary': '📊',
  'details': '📋',
  'success': '✅',
  'warning': '⚠️',
  'error': '❌',
  'info': '💡',
  'next': '🚀',
  'link': '🔗',
  'time': '⏱️',
  'test': '🧪'
};
```

### Formatting Rules
```yaml
formatting:
  headers:
    h2: "Command title level"
    h3: "Major sections"
    h4: "Subsections"
    h5: "Rarely used"
  
  emphasis:
    bold: "Key information, labels"
    italic: "Subtitles, quotes, descriptions"
    code: "File paths, commands, code"
  
  lists:
    bullet: "General information"
    numbered: "Sequential steps"
    checkbox: "Actionable items"
  
  spacing:
    between_sections: "One blank line"
    between_subsections: "One blank line"
    around_code_blocks: "One blank line"
```

## Context Integration

```xml
<context_block>
<!-- Standardized context output for all commands -->
<context_output>
### 🔗 Session Context
**Command**: {{command_name}}
**Timestamp**: {{iso_timestamp}}
**Duration**: {{execution_duration}}

**Session State**:
```json
{
  "session_id": "{{session_id}}",
  "command_index": {{index}},
  "accumulated_context": {
    "project": "{{project_name}}",
    "phase": "{{current_phase}}",
    "focus": "{{current_focus}}"
  },
  "continuity": {
    "previous_command": "{{prev_command}}",
    "natural_next": "{{next_command}}",
    "alternatives": {{alternatives}}
  }
}
```
</context_output>
</context_block>
```

## Output Variations

### Verbose Mode
```xml
{{#if verbose_mode}}
<verbose_additions>
  <thinking_trace>Full thinking process</thinking_trace>
  <decision_rationale>Detailed explanations</decision_rationale>
  <alternative_considered>Other options explored</alternative_considered>
</verbose_additions>
{{/if}}
```

### Minimal Mode
```xml
{{#if minimal_mode}}
<minimal_output>
  <!-- Only essential information -->
  **Done**: {{what}}
  **Next**: {{next}}
  **Run**: `{{command}}`
</minimal_output>
{{/if}}
```

### Error Output
```xml
<error_output>
## ❌ {{Error_Type}}

**What happened**: {{error_description}}

**Why**: {{root_cause}}

**How to fix**:
1. {{fix_step_1}}
2. {{fix_step_2}}
3. {{fix_step_3}}

**Alternative approach**:
```bash
{{alternative_command}}
```

**Get help**: {{help_resources}}
</error_output>
```

## Accessibility Standards

```yaml
accessibility:
  screen_readers:
    - Use descriptive headers
    - Avoid ASCII art in main content
    - Provide text descriptions for diagrams
  
  cognitive_load:
    - Progressive disclosure
    - Clear visual hierarchy
    - Consistent formatting
    - Scannable sections
  
  internationalization:
    - Avoid idioms
    - Use clear, simple language
    - Provide context for technical terms
```

## Best Practices

1. **Consistency**: Same sections in same order across commands
2. **Scannability**: Users should find information quickly
3. **Actionability**: Clear next steps and commands
4. **Context**: Always show session state and continuity
5. **Adaptability**: Adjust detail level to user preferences

## Anti-Patterns

- ❌ Walls of text without structure
- ❌ Inconsistent emoji usage
- ❌ Missing next steps
- ❌ No session context
- ❌ Overly technical without explanation