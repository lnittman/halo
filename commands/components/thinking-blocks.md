# Enhanced Thinking Blocks Component

Provides structured, multi-phase thinking patterns for all Claude Code commands to ensure transparency, build trust, and improve decision quality through extended reasoning and critical evaluation.

## Extended Thinking Requirements

```xml
<thinking_requirements>
# Use extended thinking liberally - default to MORE thinking, not less
- Simple requests: "think about implementation approach"
- Complex requests: "think deeply about edge cases, constraints, and alternatives"
- Creative tasks: "think extensively about possibilities and their implications"
- Always: "think critically about potential flaws in this approach"
</thinking_requirements>

<ultrathink_triggers>
# Automatically engage deep thinking for:
- Architecture decisions
- API design
- Security implications  
- Performance optimization
- User experience trade-offs
- Integration complexity
- When user says "think about", "consider", "explore"
- When dealing with system design or refactoring
- When multiple valid approaches exist
</ultrathink_triggers>
```

## Core Thinking Pattern

```xml
<thinking_process>
<!-- Phase 1: Understanding -->
<understanding_phase>
  <user_intent>
  Let me understand what you're asking for:
  - Primary goal: {{extracted_goal}}
  - Context: {{relevant_context}}
  - Constraints: {{identified_constraints}}
  - Success looks like: {{success_criteria}}
  </user_intent>
  
  <assumptions>
  I'm making these assumptions:
  - {{assumption_1}}
  - {{assumption_2}}
  - {{assumption_3}}
  </assumptions>
</understanding_phase>

<!-- Phase 2: Analysis -->
<analysis_phase>
  <current_state>
  Current situation:
  - {{state_assessment}}
  - {{existing_resources}}
  - {{identified_gaps}}
  </current_state>
  
  <options_considered>
  Possible approaches:
  1. {{option_1}}: {{pros_cons}}
  2. {{option_2}}: {{pros_cons}}
  3. {{option_3}}: {{pros_cons}}
  </options_considered>
  
  <decision_rationale>
  Choosing approach {{selected}} because:
  - {{reason_1}}
  - {{reason_2}}
  - {{reason_3}}
  </decision_rationale>
</analysis_phase>

<!-- Phase 3: Planning -->
<planning_phase>
  <execution_plan>
  Here's my plan:
  1. {{step_1}}: {{expected_outcome}}
  2. {{step_2}}: {{expected_outcome}}
  3. {{step_3}}: {{expected_outcome}}
  </execution_plan>
  
  <risk_mitigation>
  Potential issues and mitigations:
  - Risk: {{risk_1}} → Mitigation: {{mitigation_1}}
  - Risk: {{risk_2}} → Mitigation: {{mitigation_2}}
  </risk_mitigation>
  
  <success_metrics>
  How we'll know it worked:
  - [ ] {{metric_1}}
  - [ ] {{metric_2}}
  - [ ] {{metric_3}}
  </success_metrics>
</planning_phase>

<!-- Phase 4: Critical Evaluation -->
<critical_evaluation>
  <potential_issues>
  What could go wrong:
  - {{issue_1}}: {{impact_and_likelihood}}
  - {{issue_2}}: {{impact_and_likelihood}}
  - {{issue_3}}: {{impact_and_likelihood}}
  </potential_issues>
  
  <oversimplifications>
  What I might be oversimplifying:
  - {{oversimplification_1}}: {{reality_check}}
  - {{oversimplification_2}}: {{reality_check}}
  </oversimplifications>
  
  <skeptical_review>
  A skeptical reviewer would point out:
  - {{criticism_1}}: {{validity_assessment}}
  - {{criticism_2}}: {{validity_assessment}}
  - {{alternative_view}}: {{consideration}}
  </skeptical_review>
  
  <confidence_assessment>
  My confidence level: {{high|medium|low}}
  Because: {{reasoning}}
  Areas of uncertainty: {{specific_unknowns}}
  </confidence_assessment>
</critical_evaluation>

<!-- User-Visible Summary -->
<thinking_summary>
## 🧠 My Thinking Process

**Understanding**: {{one_line_interpretation}}

**Analysis**: {{key_insight}}

**Approach**: {{selected_approach_summary}}

**Next Steps**: {{immediate_action}}
</thinking_summary>
</thinking_process>
```

## Command-Specific Variants

### For Planning Commands (create, multitask, vision)
```xml
<extended_thinking>
  <creative_exploration>
  Exploring possibilities:
  - What if: {{creative_idea_1}}
  - What if: {{creative_idea_2}}
  - What if: {{creative_idea_3}}
  </creative_exploration>
  
  <pattern_recognition>
  Relevant patterns from your codebase:
  - {{pattern_1}}: {{application}}
  - {{pattern_2}}: {{application}}
  </pattern_recognition>
</extended_thinking>
```

### For Execution Commands (build, prime)
```xml
<execution_thinking>
  <pre_flight_check>
  Before proceeding:
  - [ ] {{check_1}}: {{status}}
  - [ ] {{check_2}}: {{status}}
  - [ ] {{check_3}}: {{status}}
  </pre_flight_check>
  
  <parallel_opportunities>
  Can execute simultaneously:
  - Task Group A: {{tasks}}
  - Task Group B: {{tasks}}
  - Task Group C: {{tasks}}
  </parallel_opportunities>
</execution_thinking>
```

### For Analysis Commands (docaudit, diagram)
```xml
<analytical_thinking>
  <data_synthesis>
  Patterns discovered:
  - {{pattern_1}}: {{implication}}
  - {{pattern_2}}: {{implication}}
  </data_synthesis>
  
  <gap_analysis>
  Missing elements:
  - {{gap_1}}: {{impact}}
  - {{gap_2}}: {{impact}}
  </gap_analysis>
</analytical_thinking>
```

## Integration Instructions

### Placement in Commands
1. Add immediately after `<prompt_transformation>`
2. Before any execution or main processing
3. Update throughout execution as thinking evolves

### Example Integration
```xml
</prompt_transformation>

<thinking_process>
  <!-- Thinking blocks here -->
</thinking_process>

<main_execution>
  <!-- Command logic here -->
</main_execution>
```

## Thinking Persistence

### Save to Session
```json
{
  "thinking_history": [
    {
      "command": "create",
      "timestamp": "ISO_8601",
      "understanding": "User wants to build a task management app",
      "decision": "Using Next.js with Prisma and Clerk",
      "rationale": "Matches existing patterns, provides auth",
      "outcome": "Success - project scaffolded"
    }
  ]
}
```

## User Communication Principles

1. **Transparency**: Show enough thinking to build trust, not overwhelm
2. **Relevance**: Only show thinking that impacts user decisions
3. **Clarity**: Use plain language, avoid jargon
4. **Actionability**: Connect thinking to concrete next steps
5. **Iteration**: Update thinking as new information emerges

## Anti-Sycophancy Mechanisms

```xml
<anti_sycophancy>
Before accepting any approach as "good":
1. Ask: "What are three ways this could fail?"
2. Consider: "What would a critic say about this?"
3. Check: "Am I being overly optimistic?"
4. Verify: "Have I considered simpler alternatives?"
5. Question: "Am I agreeing too readily with implied preferences?"
</anti_sycophancy>
```

### Reality Check Output Format
```markdown
### 🚨 Reality Check
**What could fail**: [Honest assessment of failure modes]
**Technical debt risks**: [Specific technical concerns]
**User adoption barriers**: [Real obstacles users might face]
**Simpler alternative**: [A less complex approach that might work]
**Confidence level**: [High/Medium/Low] - [Why]
```

## Anti-Patterns to Avoid

- ❌ Showing every micro-decision
- ❌ Using thinking as filler content
- ❌ Repeating obvious information
- ❌ Making thinking feel robotic
- ❌ Hiding important decisions
- ❌ Being overly agreeable or optimistic
- ❌ Ignoring obvious problems
- ❌ Assuming everything will work perfectly
- ❌ Using superlatives like "amazing", "revolutionary", "game-changing"

## Best Practices

1. **Progressive Disclosure**: Start with summary, expand if needed
2. **Context Awareness**: Reference previous thinking from session
3. **Confidence Levels**: Be honest about uncertainty
4. **Learning Display**: Show how past outcomes inform current thinking
5. **User Alignment**: Regularly check if thinking matches user intent
6. **Critical First**: Lead with potential issues, not just benefits
7. **Alternatives Always**: Present at least one simpler alternative
8. **Concrete Examples**: Support claims with specific evidence
9. **Failure Modes**: Explicitly consider how things could go wrong
10. **Continuous Verification**: Re-evaluate assumptions during execution