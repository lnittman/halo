# Enhanced XML Prompt Transformer Component

A sophisticated input transformation system that converts any user input into structured, actionable XML while maintaining transparency and building user trust.

## Core Transformation Pattern

```xml
<prompt_transformation>
<!-- Phase 1: Input Analysis -->
<input_analysis>
  <raw_input>$ARGUMENTS</raw_input>
  
  <detected_elements>
    <urls count="{{url_count}}">
      {{#each urls}}
      <url type="{{type}}">{{url}}</url>
      {{/each}}
    </urls>
    
    <code_blocks count="{{code_count}}">
      {{#each code_blocks}}
      <code language="{{lang}}">{{preview}}</code>
      {{/each}}
    </code_blocks>
    
    <file_paths count="{{file_count}}">
      {{#each files}}
      <file>{{path}}</file>
      {{/each}}
    </file_paths>
    
    <images count="{{image_count}}">
      {{#each images}}
      <image>{{path}}</image>
      {{/each}}
    </images>
    
    <natural_language>
      <sentences>{{sentence_count}}</sentences>
      <questions>{{question_count}}</questions>
      <commands>{{command_count}}</commands>
    </natural_language>
  </detected_elements>
</input_analysis>

<!-- Phase 2: Semantic Extraction -->
<semantic_extraction>
  <intent>
    <primary>{{main_intent}}</primary>
    <secondary>{{secondary_intents}}</secondary>
    <confidence>{{0.0-1.0}}</confidence>
  </intent>
  
  <context>
    <project_name>{{extracted_or_inferred}}</project_name>
    <domain>{{web|mobile|api|cli|ml|data|infra}}</domain>
    <technology_stack>
      {{#each detected_technologies}}
      <tech>{{name}}</tech>
      {{/each}}
    </technology_stack>
    <phase>{{planning|building|debugging|optimizing|documenting}}</phase>
  </context>
  
  <requirements>
    <explicit>
      {{#each explicit_requirements}}
      <requirement priority="{{priority}}">{{text}}</requirement>
      {{/each}}
    </explicit>
    <implicit>
      {{#each inferred_requirements}}
      <requirement confidence="{{confidence}}">{{text}}</requirement>
      {{/each}}
    </implicit>
    <anti_requirements>
      {{#each things_to_avoid}}
      <avoid>{{text}}</avoid>
      {{/each}}
    </anti_requirements>
  </requirements>
  
  <constraints>
    <technical>
      {{#each technical_constraints}}
      <constraint>{{text}}</constraint>
      {{/each}}
    </technical>
    <business>
      {{#each business_constraints}}
      <constraint>{{text}}</constraint>
      {{/each}}
    </business>
    <timeline>{{timeline_if_mentioned}}</timeline>
  </constraints>
  
  <emotional_context>
    <urgency>{{low|medium|high}}</urgency>
    <frustration_level>{{detected_frustration}}</frustration_level>
    <excitement_level>{{detected_excitement}}</excitement_level>
    <clarity>{{clear|confused|exploring}}</clarity>
  </emotional_context>
</semantic_extraction>

<!-- Phase 3: Session Integration -->
<session_integration>
  <previous_context>
    <last_command>{{previous_command}}</last_command>
    <last_outcome>{{success|partial|failed}}</last_outcome>
    <accumulated_decisions>
      {{#each session_decisions}}
      <decision>{{text}}</decision>
      {{/each}}
    </accumulated_decisions>
  </previous_context>
  
  <continuity_analysis>
    <is_continuation>{{true|false}}</is_continuation>
    <context_shift>{{none|minor|major}}</context_shift>
    <should_reference_previous>{{true|false}}</should_reference_previous>
  </continuity_analysis>
</session_integration>

<!-- Phase 4: Structured Output -->
<transformed_output>
  <command_context>
    <interpreted_as>{{command_specific_interpretation}}</interpreted_as>
    <execution_mode>{{planning|immediate|exploratory}}</execution_mode>
    <verification_needed>{{true|false}}</verification_needed>
  </command_context>
  
  <action_items>
    {{#each actions}}
    <action priority="{{priority}}" parallel="{{can_parallelize}}">
      <description>{{text}}</description>
      <prerequisites>{{prereqs}}</prerequisites>
    </action>
    {{/each}}
  </action_items>
  
  <clarifications_needed>
    {{#each ambiguities}}
    <clarification>
      <area>{{topic}}</area>
      <question>{{question}}</question>
      <default>{{assumed_answer}}</default>
    </clarification>
    {{/each}}
  </clarifications_needed>
</transformed_output>

<!-- User-Visible Transformation Summary -->
<transformation_feedback>
## 🔄 Input Transformation

**What I understood**: {{natural_language_summary}}

**Key elements detected**:
{{#if urls}}
- 🌐 {{url_count}} URL(s): {{url_summary}}
{{/if}}
{{#if code_blocks}}
- 💻 {{code_count}} code block(s): {{code_summary}}
{{/if}}
{{#if files}}
- 📁 {{file_count}} file reference(s): {{file_summary}}
{{/if}}
{{#if images}}
- 🖼️ {{image_count}} image(s): {{image_summary}}
{{/if}}

**Intent classification**: {{intent_category}} with {{confidence_word}} confidence

{{#if clarifications_needed}}
**Quick clarification**:
{{first_clarification_question}}
*Proceeding with assumption: {{default_assumption}}*
{{/if}}
</transformation_feedback>
</prompt_transformation>
```

## Command-Specific Transformations

### For Creative Commands (create, vision, brand)
```xml
<creative_transformation>
  <inspiration_extraction>
    <mood>{{detected_mood}}</mood>
    <style_preferences>{{style_hints}}</style_preferences>
    <innovation_level>{{conservative|balanced|experimental}}</innovation_level>
  </inspiration_extraction>
</creative_transformation>
```

### For Technical Commands (build, prime)
```xml
<technical_transformation>
  <specificity_analysis>
    <detail_level>{{high|medium|low}}</detail_level>
    <technical_depth>{{surface|standard|deep}}</technical_depth>
    <assumed_expertise>{{beginner|intermediate|expert}}</assumed_expertise>
  </specificity_analysis>
</technical_transformation>
```

### For Planning Commands (multitask, design)
```xml
<planning_transformation>
  <scope_analysis>
    <estimated_complexity>{{simple|moderate|complex}}</estimated_complexity>
    <decomposition_hint>{{suggested_breakdown}}</decomposition_hint>
    <collaboration_needs>{{solo|team|multi_team}}</collaboration_needs>
  </scope_analysis>
</planning_transformation>
```

## Transformation Rules

### Intent Mapping
```javascript
// Pseudo-code for intent detection
const intentMap = {
  create: ['build', 'make', 'create', 'start', 'scaffold', 'generate'],
  fix: ['fix', 'debug', 'solve', 'repair', 'patch', 'resolve'],
  improve: ['improve', 'optimize', 'enhance', 'refactor', 'upgrade'],
  analyze: ['analyze', 'review', 'audit', 'inspect', 'examine'],
  plan: ['plan', 'design', 'architect', 'structure', 'organize']
}
```

### Confidence Scoring
```javascript
// Factors affecting confidence
const confidenceFactors = {
  explicit_command: 0.3,      // User specified exact command
  clear_intent: 0.2,          // Unambiguous language
  context_continuity: 0.2,    // Follows from previous
  complete_info: 0.2,         // All needed info present
  domain_match: 0.1           // Matches command's domain
}
```

## Integration with Session State

```json
{
  "transformation_history": [
    {
      "timestamp": "ISO_8601",
      "raw_input_hash": "hash",
      "detected_intent": "create",
      "confidence": 0.85,
      "clarifications_made": [],
      "assumptions": [
        "User wants web application",
        "Using established patterns"
      ]
    }
  ]
}
```

## Error Handling

```xml
<transformation_error>
  <type>{{ambiguous_intent|missing_context|conflicting_requirements}}</type>
  <resolution_strategy>
    <ask_user>{{specific_question}}</ask_user>
    <make_assumption>{{safe_default}}</make_assumption>
    <provide_options>{{option_list}}</provide_options>
  </resolution_strategy>
</transformation_error>
```

## Best Practices

1. **Always Show Work**: Users should see how their input was interpreted
2. **Graceful Assumptions**: Make reasonable defaults but state them clearly
3. **Progressive Enhancement**: Start simple, add detail as patterns emerge
4. **Context Awareness**: Use session history to improve transformations
5. **Error Recovery**: Handle ambiguity without blocking progress

## Anti-Patterns

- ❌ Over-analyzing simple requests
- ❌ Hiding transformation logic from users
- ❌ Making assumptions without stating them
- ❌ Ignoring emotional context
- ❌ Losing information during transformation