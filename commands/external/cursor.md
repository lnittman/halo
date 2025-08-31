# external:cursor - implementation orchestrator

intelligently leverage cursor-agent for building features and fixing bugs. auto-selects between GPT-5 and Sonnet based on task complexity and context size.

<cursor_directive>
you orchestrate cursor-agent based on the user's prompt. analyze intent and select the optimal model: Sonnet for large context (>100k tokens) or GPT-5 for complex reasoning. NEVER use Opus.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<intent_detection>
analyze $ARGUMENTS to determine task type:
- **build** → implement features from specifications
- **fix** → fix bugs and resolve errors
- **refactor** → improve code structure
- **implement** → execute detailed plans
- **scaffold** → create project structure
</intent_detection>

<model_selection>
## automatic model selection
- **Sonnet 4**: Large context tasks (>100k tokens), full codebase operations
- **GPT-5**: Complex reasoning, architecture, strategic implementation
- **NEVER Opus**: Explicitly avoided in all scenarios
</model_selection>

<execution_workflow>
## actual execution with bash tool

1. **verify cursor-agent installation**
```bash
which cursor-agent || curl https://cursor.com/install -fsSL | bash
```

2. **analyze context size for model selection**
```bash
# estimate context needed
if [[ "$ARGUMENTS" == *"entire"* ]] || [[ "$ARGUMENTS" == *"full codebase"* ]]; then
  MODEL="sonnet-4"
  echo "Using Sonnet for large context"
else
  MODEL="gpt-5"
  echo "Using GPT-5 for complex reasoning"
fi
```

3. **prepare implementation spec**
```bash
cat > .cursor-spec.txt << 'EOF'
# IMPLEMENTATION TASK

$ARGUMENTS

## Requirements
1. Follow existing code patterns
2. Maintain type safety
3. Implement error handling
4. Write clean, maintainable code
5. Update tests as needed

## Success Criteria
- Feature works as specified
- Code follows conventions
- Tests pass
- No type errors
EOF
```

4. **execute with cursor-agent**
```bash
# auto-edit mode for implementation
cursor-agent -m $MODEL --auto-edit "$(cat .cursor-spec.txt)"

# verify results
npm test 2>/dev/null || echo "Remember to run tests"
npm run typecheck 2>/dev/null || echo "Remember to check types"

# cleanup
rm -f .cursor-spec.txt
```
</execution_workflow>

<task_templates>
## feature building
```markdown
Build feature:
- Implement according to specification
- Follow existing patterns
- Add proper error handling
- Include loading states
- Ensure accessibility
```

## bug fixing
```markdown
Fix bug:
- Identify root cause
- Implement minimal fix
- Preserve existing functionality
- Add regression test
- Update documentation
```

## refactoring
```markdown
Refactor code:
- Improve structure
- Enhance readability
- Reduce complexity
- Maintain functionality
- Update tests
```
</task_templates>

<best_practices>
## cursor optimization
- let model auto-selection handle complexity
- use Sonnet for large context
- use GPT-5 for complex logic
- NEVER use Opus
- focus on implementation excellence
</best_practices>

$ARGUMENTS</cursor_directive>
