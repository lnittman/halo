# 🔨 external:cursor:main - intelligent model-agnostic implementation

leverage cursor's autonomous capabilities with intelligent model selection between gpt-5 and sonnet. orchestrate execution based on detailed specifications from claude.

<cursor_main_directive>
you orchestrate cursor-agent cli intelligently, selecting the optimal model:
- **gpt-5**: complex reasoning, architecture, strategic tasks
- **sonnet 4**: large context (1m tokens), full codebase operations
- **never opus**: explicitly avoid
cursor excels at receiving detailed specs from claude and executing with precision.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<cli_documentation>
## cursor-agent cli usage

### installation
```bash
# check if installed
which cursor-agent || {
  # install via official script
  curl https://cursor.com/install -fsSL | bash
}
```

### model-aware invocation
```bash
# explicit model selection
cursor-agent chat --model gpt-5 "complex reasoning task"
cursor-agent chat --model sonnet-4 "analyze entire codebase"  # 1M context

# let cursor auto-select (recommended)
cursor-agent chat "your task here"  # intelligently picks gpt-5 or sonnet

# NEVER use opus
# cursor-agent chat --model opus  # ❌ EXPLICITLY AVOID
```

### key features
- **multi-model access**: gpt-5 (reasoning) and sonnet 4 (1m context)
- **autonomous file operations**: can read, write, modify files
- **terminal command execution**: runs commands with approval
- **spec-driven execution**: optimized for detailed requirements from claude
- **orchestration-ready**: part of claude's delegation workflow
- **headless operation**: works in CI/CD environments

### security notes
- beta software with evolving safeguards
- can modify and delete files
- executes shell commands (with approval)
- use only in trusted environments
</cli_documentation>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **check cursor-agent installation**
```bash
which cursor-agent || curl https://cursor.com/install -fsSL | bash
```

2. **prepare focused prompt**
```bash
cat > .cursor-prompt.txt << 'EOF'
[Your implementation requirements here]
EOF
```

3. **execute cursor-agent with intelligent model selection**
```bash
# analyze prompt to determine model
if grep -q "entire codebase\|comprehensive\|all files\|full analysis" .cursor-prompt.txt; then
  # large context - use sonnet
  MODEL="sonnet-4"
  echo "Using Sonnet 4 for large context..."
elif grep -q "reason\|architect\|strategic\|complex\|debug" .cursor-prompt.txt; then
  # complex reasoning - use gpt-5
  MODEL="gpt-5"
  echo "Using GPT-5 for deep reasoning..."
else
  # let cursor auto-select
  MODEL=""
  echo "Letting cursor auto-select model..."
fi

# execute with selected model
if [ -n "$MODEL" ]; then
  cursor-agent chat --model $MODEL "$(cat .cursor-prompt.txt)"
else
  cursor-agent chat "$(cat .cursor-prompt.txt)"
fi
```

4. **alternative: direct execution for simple tasks**
```bash
cursor-agent chat "fix the TypeScript errors in src/"
```
</execution_workflow>

<prompt_templates>
## orchestration-ready prompts

### receiving specs from claude
```markdown
# SPECIFICATION-DRIVEN EXECUTION

[This prompt is optimized to receive detailed specifications from Claude]

## Received Requirements
$ARGUMENTS

## Execution Instructions
1. Parse the provided specification
2. Identify all success criteria
3. Execute with precision
4. Return structured results

## Model Selection
- If context >100k tokens: Use Sonnet 4
- If complex reasoning needed: Use GPT-5
- Never use: Opus
```

### feature implementation
```markdown
# FEATURE IMPLEMENTATION TASK

## Objective
[Specific feature to build]

## Requirements
1. **Functional Requirements**
   - [User-facing features]
   - [API endpoints needed]
   - [Data models required]

2. **Technical Requirements**
   - Follow existing patterns in the codebase
   - Include comprehensive error handling
   - Add appropriate logging
   - Write unit tests for new functions

3. **Code Quality Standards**
   - Use semantic variable names
   - Keep functions small and focused
   - Apply SOLID principles
   - Consider edge cases

## Implementation Steps
1. Analyze existing codebase structure
2. Plan the implementation approach
3. Implement incrementally with verification
4. Run tests after each major change
5. Ensure the build passes

## Success Criteria
- [ ] Feature works as specified
- [ ] All tests pass
- [ ] Code follows project conventions
- [ ] Documentation updated
```

### bug fixing
```markdown
# BUG FIX TASK

## Issue Description
[Describe the bug and symptoms]

## Error Details
```
[Include error messages, stack traces]
```

## Investigation Approach
1. Reproduce the issue
2. Identify root cause
3. Develop minimal fix
4. Test the solution
5. Prevent regression

## Fix Requirements
- Minimal code changes
- Preserve existing functionality
- Add test to prevent regression
- Update relevant documentation
```

### refactoring
```markdown
# REFACTORING TASK

## Target Code
[Files/modules to refactor]

## Refactoring Goals
1. **Code Quality**
   - Improve readability
   - Reduce complexity
   - Eliminate duplication

2. **Performance**
   - Optimize algorithms
   - Reduce memory usage
   - Improve response times

3. **Maintainability**
   - Better separation of concerns
   - Clearer abstractions
   - Improved testability

## Constraints
- Maintain backward compatibility
- Preserve all existing functionality
- Keep changes incremental
- Ensure all tests pass

## Verification
- Run full test suite
- Performance benchmarks
- Code review checklist
```
</prompt_templates>

<best_practices>
## cursor-agent best practices

### prompt engineering
- be specific about requirements
- include success criteria
- reference existing patterns
- specify test requirements

### safety considerations
- review file operations before approval
- verify shell commands before execution
- work in version-controlled directories
- maintain backups of critical files

### optimal use cases
- implementing new features
- fixing well-defined bugs
- refactoring existing code
- adding test coverage
- updating documentation

### performance tips
- provide focused, clear requirements
- reference specific files when possible
- break large tasks into steps
- let agent handle file navigation
</best_practices>

<execution_patterns>
## common execution patterns

### focused implementation
```bash
# single file fix
cursor-agent chat "fix the TypeScript error in src/auth/login.ts"

# specific feature
cursor-agent chat "add password reset functionality to the auth module"

# test writing
cursor-agent chat "write comprehensive tests for the payment service"
```

### comprehensive tasks
```bash
# full feature implementation
PROMPT="Implement a complete user dashboard with:
- Profile management
- Activity history
- Settings panel
- Responsive design
Follow the existing component patterns in src/components/"

cursor-agent chat "$PROMPT"
```

### debugging workflow
```bash
# investigate and fix
cursor-agent chat "Debug why the login flow fails after 5 minutes of inactivity"

# with error context
ERROR_LOG=$(cat error.log | tail -50)
cursor-agent chat "Fix this error: $ERROR_LOG"
```
</execution_patterns>

<integration_notes>
## integration with halo system

### context awareness
- cursor-agent auto-discovers project structure
- reads package.json, tsconfig, etc.
- understands existing patterns
- follows project conventions

### orchestration workflow
```bash
# claude gathers context and writes spec
cat specification.md | cursor-agent chat --model sonnet-4 -

# receive detailed PRDA from claude
cursor-agent chat "Execute the following specification: $(cat prda.md)"

# after gemini analysis
cursor-agent chat --model gpt-5 "Fix issues from audit.md with strategic thinking"

# continuous orchestration
while read -r task < tasks.txt; do
  cursor-agent chat "$task"
done
```

### output handling
- cursor-agent shows file modifications
- requests approval for changes
- provides execution summaries
- maintains conversation context
</integration_notes>

<usage_examples>
## example invocations

### implement feature
```
/external:cursor-agent build user authentication with JWT
```

### fix bugs
```
/external:cursor-agent fix the memory leak in the WebSocket handler
```

### refactor code
```
/external:cursor-agent refactor the payment service for better testability
```

### add tests
```
/external:cursor-agent write integration tests for the API endpoints
```

### update documentation
```
/external:cursor-agent update the README with current API documentation
```
</usage_examples>

$ARGUMENTS</cursor_agent_directive>