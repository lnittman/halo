# 🔨 external:codex:build - gpt-5 strategic build planning

leverage codex's gpt-5 reasoning for comprehensive build planning and implementation strategies.

<codex_build_directive>
you orchestrate codex cli for strategic build planning. codex uses gpt-5 to design optimal implementation approaches.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<build_capabilities>
## cursor-agent build strengths

- autonomous file creation and modification
- gpt-5 powered code generation
- intelligent refactoring
- automated testing
- dependency management
- real-time iteration
</build_capabilities>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **prepare build context**
```bash
# gather relevant files if needed
find . -name "*.ts" -o -name "*.tsx" | head -20 > relevant-files.txt

# create build requirements
cat > .cursor-build-prompt.txt << 'EOF'
# GPT-5 AUTONOMOUS BUILD TASK

Think deeply and implement the following feature with exceptional quality.

## Build Requirements
$ARGUMENTS

## Implementation Instructions

### Core Requirements
1. **Feature Specification**
   - Implement exactly as specified
   - Follow existing code patterns
   - Maintain consistency with codebase
   - Ensure type safety throughout

2. **Code Quality Standards**
   - Write clean, maintainable code
   - Follow SOLID principles
   - Implement proper error handling
   - Add comprehensive comments
   - Ensure accessibility compliance

3. **File Operations**
   - Create new files as needed
   - Modify existing files carefully
   - Maintain git-friendly changes
   - Preserve existing functionality

4. **Testing Requirements**
   - Write unit tests for new code
   - Update existing tests as needed
   - Ensure all tests pass
   - Add integration tests where appropriate

5. **Documentation**
   - Update relevant documentation
   - Add JSDoc/TSDoc comments
   - Create usage examples
   - Update README if needed

## Implementation Strategy

### Phase 1: Setup
- Analyze existing code structure
- Identify integration points
- Plan component hierarchy
- Design data flow

### Phase 2: Core Implementation
- Build main components
- Implement business logic
- Add state management
- Create API endpoints

### Phase 3: Integration
- Connect to existing systems
- Update routing/navigation
- Integrate with services
- Add error boundaries

### Phase 4: Polish
- Add loading states
- Implement error handling
- Optimize performance
- Ensure responsiveness

### Phase 5: Testing & Documentation
- Write comprehensive tests
- Document all changes
- Create examples
- Update changelogs

## Success Criteria
- [ ] Feature works as specified
- [ ] All tests pass
- [ ] Code follows patterns
- [ ] Documentation updated
- [ ] No regressions introduced
- [ ] Performance maintained
- [ ] Accessibility compliant

## Output Expectations
After implementation:
1. List all files created/modified
2. Provide usage instructions
3. Note any additional requirements
4. Suggest follow-up improvements
EOF
```

3. **execute cursor-agent build**
```bash
# GPT-5 strategic build planning
codex exec -m gpt-5 -s workspace-write "Think deeply: $(cat .codex-build-prompt.txt)" 2>&1 | tee codex-build.log
```

4. **verify implementation**
```bash
# check what was modified
git status

# run tests if available
npm test 2>/dev/null || echo "No tests configured"

# show summary of changes
git diff --stat
```
</execution_workflow>

<specialized_builds>
## build patterns

### component building
```bash
codex -m gpt-5 --auto-edit "Think deeply: Build a React component for $COMPONENT_NAME with TypeScript, tests, and Storybook stories"
```

### api endpoint creation
```bash
codex -m gpt-5 --auto-edit "Think deeply: Create a REST API endpoint for $ENDPOINT with validation, error handling, and tests"
```

### refactoring
```bash
codex -m gpt-5 --auto-edit "Think deeply: Refactor $FILE to improve performance and maintainability"
```

### implementation planning
```bash
codex -m gpt-5 "Think deeply: Plan implementation for feature $FEATURE_NAME"
```
</specialized_builds>

<integration_patterns>
## workflow integration

### build pipeline
```bash
# 1. Plan with gemini
/external:gemini:build plan feature

# 2. Implement with cursor-agent
/external:cursor-agent:build implement plan

# 3. Test with codex
/external:codex:test verify implementation

# 4. Polish with cursor-agent
/external:cursor-agent:polish refine ui
```

### iterative development
```bash
# rapid iteration
/external:cursor-agent:build create component
/test run tests
/external:cursor-agent:fix address issues
/external:cursor-agent:polish improve ux
```
</integration_patterns>

<best_practices>
## optimal usage

### when to use cursor-agent:build
- feature implementation
- component creation
- bug fixes
- refactoring tasks
- test writing
- documentation updates

### prompt optimization
- be specific about requirements
- reference existing patterns
- specify edge cases
- define success criteria
- request tests
</best_practices>

<output_format>
## 🔨 cursor-agent building

**task**: {{task_description}}  
**mode**: gpt-5 autonomous  
**operations**: file creation/modification  

### 📝 implementation progress

files created:
{{created_files}}

files modified:
{{modified_files}}

### ✅ completed tasks

{{completed_items}}

### 🎯 success criteria

{{success_checklist}}

### 🚀 next steps

{{follow_up_actions}}

---
✨ build complete. check `cursor-build.log` for details
</output_format>

$ARGUMENTS</cursor_build_directive>