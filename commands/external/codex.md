# external:codex - deep reasoning orchestrator

intelligently leverage codex cli's GPT-5 for tasks requiring strategic thinking, complex problem solving, and architectural reasoning.

<codex_directive>
you orchestrate codex cli based on the user's prompt. analyze intent and configure codex with GPT-5 for deep reasoning. codex excels at strategic planning, debugging, and complex technical analysis.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<intent_detection>
analyze $ARGUMENTS to determine task type:
- **architect** → system design and architecture planning
- **debug** → root cause analysis and deep debugging
- **plan** → strategic technical planning
- **research** → technical research and evaluation
- **optimize** → performance analysis and optimization
</intent_detection>

<execution_workflow>
## actual execution with bash tool

1. **verify codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **prepare strategic prompt**
```bash
cat > .codex-prompt.txt << 'EOF'
Think deeply and reason step-by-step:

$ARGUMENTS

## Analysis Requirements
1. Break down the problem systematically
2. Consider multiple approaches and trade-offs
3. Provide detailed reasoning for recommendations
4. Include implementation strategy if applicable
5. Identify potential risks and mitigations
EOF
```

3. **execute with GPT-5 reasoning**
```bash
# ALWAYS use GPT-5 for deep reasoning
codex -m gpt-5 --auto-edit "$(cat .codex-prompt.txt)"

# cleanup
rm -f .codex-prompt.txt
```
</execution_workflow>

<task_templates>
## architecture design
```markdown
Design system architecture:
- Analyze requirements and constraints
- Evaluate architectural patterns
- Design component interactions
- Plan data flow and state management
- Create implementation roadmap
```

## debugging investigation
```markdown
Debug complex issue:
- Analyze symptoms and error patterns
- Trace execution flow
- Identify root causes
- Design minimal fix
- Plan regression prevention
```

## strategic planning
```markdown
Strategic technical planning:
- Assess current state
- Define target architecture
- Map migration path
- Identify risks and dependencies
- Create phased implementation plan
```
</task_templates>

<best_practices>
## codex optimization
- ALWAYS use GPT-5 model
- prefix prompts with "Think deeply"
- focus on reasoning and analysis
- use for planning, not implementation
- leverage for complex problem solving
</best_practices>

$ARGUMENTS</codex_directive>
