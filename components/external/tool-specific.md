# Tool-Specific Orchestration Templates

## Codex (GPT-5 Deep Reasoning)
```xml
<codex_orchestration>
  <model_directive>Use GPT-5 for maximum reasoning depth</model_directive>
  <thinking_mode>deep_analytical</thinking_mode>
  
  <task_types>
    <architecture>System design and technical architecture</architecture>
    <debugging>Root cause analysis and complex troubleshooting</debugging>
    <strategy>Technical planning and optimization</strategy>
    <research>Technical evaluation and comparison</research>
  </task_types>
  
  <prompt_structure>
    <prefix>Think deeply and reason step-by-step:</prefix>
    <context>Comprehensive problem background</context>
    <requirements>
      <systematic_breakdown>Decompose the problem methodically</systematic_breakdown>
      <trade_off_analysis>Evaluate multiple approaches</trade_off_analysis>
      <detailed_reasoning>Provide thorough justification</detailed_reasoning>
      <risk_assessment>Identify and mitigate risks</risk_assessment>
    </requirements>
  </prompt_structure>
</codex_orchestration>
```

## Gemini (2M Context Analysis)
```xml
<gemini_orchestration>
  <context_preparation>
    <repomix_config>
      <include>**/*.{ts,tsx,js,jsx,py,go,rs,md,json,yaml}</include>
      <exclude>node_modules/**, .git/**, dist/**, build/**</exclude>
      <output>.gemini-context.md</output>
    </repomix_config>
    <token_optimization>Progressive refinement for 2M window</token_optimization>
  </context_preparation>
  
  <analysis_types>
    <codebase_audit>Security, performance, quality</codebase_audit>
    <pattern_extraction>Identify recurring patterns</pattern_extraction>
    <dependency_mapping>Understand interconnections</dependency_mapping>
    <refactor_planning>Large-scale improvements</refactor_planning>
  </analysis_types>
  
  <prompt_structure>
    <instruction>Analyze the entire codebase comprehensively</instruction>
    <focus_areas>Specific aspects to examine</focus_areas>
    <deliverables>Actionable findings and recommendations</deliverables>
  </prompt_structure>
</gemini_orchestration>
```

## Cursor (Implementation Engine)
```xml
<cursor_orchestration>
  <model_selection>
    <condition test="context_size > 100000">sonnet-4</condition>
    <condition test="complexity == high">gpt-5</condition>
    <default>gpt-5</default>
    <never>opus</never>
  </model_selection>
  
  <implementation_spec>
    <requirements>
      <follow_patterns>Match existing code style</follow_patterns>
      <type_safety>Maintain TypeScript compliance</type_safety>
      <error_handling>Comprehensive try-catch</error_handling>
      <test_coverage>Update/add tests</test_coverage>
    </requirements>
    
    <success_criteria>
      <functional>Feature works as specified</functional>
      <quality>Clean, maintainable code</quality>
      <testing>All tests pass</testing>
      <typing>No type errors</typing>
    </success_criteria>
  </implementation_spec>
</cursor_orchestration>
```

## Claude (MCP Orchestrator)
```xml
<claude_orchestration>
  <mcp_tools>
    <firecrawl>Web scraping and search</firecrawl>
    <context7>Documentation retrieval</context7>
    <convex>Backend operations</convex>
    <vercel>Deployment management</vercel>
    <linear>Project management</linear>
  </mcp_tools>
  
  <halo_commands>
    <prime>Deep project understanding</prime>
    <build>Feature implementation</build>
    <test>Test generation and execution</test>
    <docs>Documentation creation</docs>
    <web>Research and data gathering</web>
  </halo_commands>
  
  <orchestration_patterns>
    <research_first>Gather context before action</research_first>
    <parallel_tools>Execute multiple tools concurrently</parallel_tools>
    <iterative_refinement>Progressive improvement cycles</iterative_refinement>
  </orchestration_patterns>
</claude_orchestration>
```