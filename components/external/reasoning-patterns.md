# Reasoning Patterns for External Tools

## Chain of Thought (CoT)
```xml
<reasoning_approach>
  <instruction>Think step-by-step through this problem</instruction>
  <breakdown>
    <step_1>Understand the requirements</step_1>
    <step_2>Analyze the current state</step_2>
    <step_3>Identify gaps and challenges</step_3>
    <step_4>Design the solution approach</step_4>
    <step_5>Consider edge cases</step_5>
    <step_6>Implement the solution</step_6>
    <step_7>Verify correctness</step_7>
  </breakdown>
</reasoning_approach>
```

## Guided CoT for Specific Domains
```xml
<guided_reasoning task="debugging">
  <symptom_analysis>What errors or unexpected behaviors are occurring?</symptom_analysis>
  <hypothesis_generation>What could be causing these symptoms?</hypothesis_generation>
  <evidence_gathering>What data supports or refutes each hypothesis?</evidence_gathering>
  <root_cause_identification>What is the most likely cause?</root_cause_identification>
  <solution_design>How can we fix the root cause?</solution_design>
  <impact_assessment>What are the implications of this fix?</impact_assessment>
  <implementation_plan>Step-by-step fix with rollback plan</implementation_plan>
</guided_reasoning>
```

## Self-Consistency Pattern
```xml
<multi_path_reasoning>
  <instruction>Generate 3 independent solutions, then synthesize</instruction>
  <path_1>First approach with reasoning</path_1>
  <path_2>Alternative approach with different assumptions</path_2>
  <path_3>Third perspective or methodology</path_3>
  <synthesis>Compare approaches and select best elements</synthesis>
  <consensus>Final solution incorporating strongest aspects</consensus>
</multi_path_reasoning>
```

## Chain of Verification (CoVe)
```xml
<verification_process>
  <draft>Initial solution or analysis</draft>
  <verification_questions>
    <q1>Is the problem correctly understood?</q1>
    <q2>Are all requirements addressed?</q2>
    <q3>Are there logical errors or gaps?</q3>
    <q4>Does this handle edge cases?</q4>
    <q5>Is this the optimal approach?</q5>
  </verification_questions>
  <independent_answers>Answer each question without bias</independent_answers>
  <revised_solution>Updated solution based on verification</revised_solution>
</verification_process>
```

## ReAct Pattern (Reasoning + Acting)
```xml
<react_loop>
  <thought>Current understanding and next step</thought>
  <action>Tool use or information retrieval</action>
  <observation>Result from action</observation>
  <reflection>What this tells us</reflection>
  <decision>Continue, pivot, or conclude</decision>
</react_loop>
```