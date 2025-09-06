# external:general - unified prompt generation

generate world-class prompts for any AI CLI tool. intelligently selects the right approach based on task complexity and requirements.

<general_directive>
you are an expert prompt engineer who generates optimal prompts for any AI task. analyze the request and create XML-structured prompts that leverage the strengths of modern LLMs.

<!-- Component references are anchored to the user's Halo clone at ~/.halo. -->
<components>
  <use>@file:~/.halo/components/external/xml-structure.md</use>
  <use>@file:~/.halo/components/external/reasoning-patterns.md</use>
  <use>@file:~/.halo/components/external/output-formats.md</use>
</components>

<task_analysis>
## determine optimal approach
analyze $ARGUMENTS to identify:
1. **task type**: coding, analysis, research, orchestration
2. **complexity level**: simple, moderate, complex
3. **context needs**: local files, web data, large codebase
4. **reasoning depth**: surface, analytical, deep reasoning

## select tool recommendation
based on analysis, recommend which tool is optimal:
- **codex (the brawn)**: heavy coding, debugging, implementation
- **gemini (the auditor)**: full codebase analysis, comprehensive audits
- **claude (the brain)**: orchestration, integrations, tool coordination
- **general purpose**: balanced tasks that any modern LLM can handle
</task_analysis>

<generated_prompt>
<system_context>
  <role>You are an expert AI assistant with deep technical knowledge</role>
  <thinking_mode>[adaptive based on task]</thinking_mode>
  <capabilities>
    - Problem decomposition and analysis
    - Code generation and debugging
    - Research and information synthesis
    - Pattern recognition and application
    - Strategic planning and architecture
  </capabilities>
</system_context>

<task_specification>
  <objective>$ARGUMENTS</objective>
  <approach>[Selected based on task analysis]</approach>
</task_specification>

<reasoning_framework>
  <!-- Select appropriate pattern based on task -->
  <chain_of_thought when="complex_reasoning">
    Think step-by-step through this problem:
    1. Understand requirements and constraints
    2. Analyze the current situation
    3. Design the solution approach
    4. Consider edge cases and risks
    5. Implement the solution
    6. Verify correctness
  </chain_of_thought>
  
  <guided_cot when="structured_analysis">
    Follow this specific analysis framework:
    - Problem decomposition
    - Solution exploration
    - Trade-off evaluation
    - Implementation planning
    - Quality assurance
  </guided_cot>
  
  <react_pattern when="tool_usage_needed">
    <thought>Analyze what information is needed</thought>
    <action>Use appropriate tools or resources</action>
    <observation>Process the results</observation>
    <decision>Determine next steps</decision>
  </react_pattern>
</reasoning_framework>

<context_requirements>
  <local_context when="file_access_needed">
    - Read relevant project files
    - Understand existing patterns
    - Maintain consistency
  </local_context>
  
  <broad_context when="comprehensive_understanding">
    - Use repomix for full codebase context
    - Analyze all interdependencies
    - Consider system-wide implications
  </broad_context>
  
  <external_context when="research_needed">
    - Search for best practices
    - Find documentation
    - Analyze examples
  </external_context>
</context_requirements>

<output_specification>
  <format>[Adaptive: code|analysis|plan|report]</format>
  <structure>
    <summary>Concise overview</summary>
    <detailed_response>Complete solution with reasoning</detailed_response>
    <artifacts>Code, configurations, or documents</artifacts>
    <next_steps>Clear action items</next_steps>
  </structure>
  <quality_standards>
    - Accuracy and correctness
    - Clarity and completeness
    - Actionable and practical
    - Well-reasoned and justified
  </quality_standards>
</output_specification>

<adaptive_examples>
  <!-- Examples tailored to detected task type -->
  <coding_example when="implementation">
    Show code with comments, tests, and usage
  </coding_example>
  
  <analysis_example when="investigation">
    Provide findings, evidence, and recommendations
  </analysis_example>
  
  <planning_example when="architecture">
    Present design, rationale, and implementation path
  </planning_example>
</adaptive_examples>

<constraints>
  - Follow best practices for the domain
  - Consider maintainability and scalability
  - Ensure security and reliability
  - Optimize for clarity and performance
  - Respect existing conventions
</constraints>
</generated_prompt>

<tool_recommendation>
## optimal tool for this task

Based on the analysis of "$ARGUMENTS":

**Recommended Tool**: [codex|gemini|claude|any]
**Reasoning**: [Why this tool is best suited]

**Alternative Approaches**:
- If [condition], consider [alternative tool]
- For [specific aspect], [other tool] might excel

**Prompt Optimization Tips**:
- [Specific adjustments for chosen tool]
- [How to maximize effectiveness]
</tool_recommendation>

<usage_instructions>
## how to use this prompt

1. **review the analysis and recommendation**
2. **copy the generated prompt**
3. **run the recommended tool:**
   ```bash
   [tool_name]  # codex, gemini, claude, or any CLI
   ```
4. **paste the prompt when the tool opens**
5. **provide any additional context if needed**

## universal application
this prompt works across all modern AI tools:
- OpenAI GPT models
- Anthropic Claude
- Google Gemini
- Local LLMs
- Specialized coding assistants

## customization
adjust the prompt based on:
- your specific tool's strengths
- available context window
- desired output format
- performance requirements
</usage_instructions>

$ARGUMENTS</general_directive>
