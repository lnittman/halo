# 🔧 external:codex:fix - gpt-5 strategic bug analysis & fixing

leverage codex's gpt-5 reasoning for deep bug analysis and strategic fixing approaches.

<codex_fix_directive>
you orchestrate codex cli for strategic bug fixing. codex uses gpt-5 to deeply understand root causes and implement comprehensive fixes.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<fix_capabilities>
## intelligent fixing abilities

- root cause analysis
- automated debugging
- code correction
- test repair
- regression prevention
- performance fixes
- security patches
- type error resolution
</fix_capabilities>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **gather error context**
```bash
# collect error information
if [ -f "error.log" ]; then
  tail -100 error.log > .error-context.txt
fi

# get test failures
npm test 2>&1 | head -200 > .test-failures.txt || true

# check type errors
npx tsc --noEmit 2>&1 > .type-errors.txt || true
```

3. **create fix prompt**
```bash
cat > .cursor-fix-prompt.txt << 'EOF'
# GPT-5 AUTONOMOUS BUG FIXING

Think deeply, diagnose the issue, and implement a comprehensive fix.

## Issue Description
$ARGUMENTS

## Error Context
$(cat .error-context.txt 2>/dev/null || echo "No error logs available")

## Test Failures
$(cat .test-failures.txt 2>/dev/null || echo "No test failures captured")

## Type Errors
$(cat .type-errors.txt 2>/dev/null || echo "No type errors found")

## Fixing Instructions

### 1. Root Cause Analysis
- Analyze error messages and stack traces
- Identify the root cause, not just symptoms
- Trace the error flow through the codebase
- Check for related issues

### 2. Fix Implementation
- Fix the root cause comprehensively
- Handle edge cases
- Maintain backward compatibility
- Preserve existing functionality
- Follow existing code patterns

### 3. Error Prevention
- Add proper error handling
- Implement input validation
- Add defensive programming
- Create guard clauses
- Handle null/undefined cases

### 4. Testing
- Write tests to verify the fix
- Add regression tests
- Update existing tests if needed
- Ensure all tests pass

### 5. Code Quality
- Maintain clean code principles
- Add helpful comments
- Update documentation
- Follow style guidelines
- Ensure type safety

## Fix Strategy

### Step 1: Diagnosis
- Locate the exact failure point
- Understand why it's failing
- Identify contributing factors

### Step 2: Solution Design
- Design a robust fix
- Consider alternative approaches
- Evaluate trade-offs

### Step 3: Implementation
- Apply the fix carefully
- Test incrementally
- Verify no regressions

### Step 4: Validation
- Run all tests
- Check type safety
- Verify functionality
- Test edge cases

## Success Criteria
- [ ] Original issue resolved
- [ ] All tests passing
- [ ] No type errors
- [ ] No new issues introduced
- [ ] Code quality maintained
- [ ] Performance not degraded
- [ ] Security not compromised

## Output Expectations
After fixing:
1. Explain the root cause
2. Describe the fix applied
3. List files modified
4. Show test results
5. Suggest preventive measures
EOF
```

4. **execute cursor-agent fix**
```bash
# GPT-5 strategic fixing
codex exec -m gpt-5 --auto-edit "Think deeply: $(cat .codex-fix-prompt.txt)" 2>&1 | tee codex-fix.log
```

5. **verify the fix**
```bash
# run tests
npm test 2>&1 | tail -20

# check types
npx tsc --noEmit && echo "✅ No type errors" || echo "❌ Type errors remain"

# show what changed
git diff --stat
echo "---"
git status --short
```
</execution_workflow>

<specialized_fixes>
## fix patterns

### type error fixes
```bash
codex -m gpt-5 --auto-edit "Think deeply: Fix all TypeScript type errors in the codebase"
```

### test failures
```bash
codex -m gpt-5 --auto-edit "Think deeply: Fix failing tests and ensure 100% pass rate"
```

### performance issues
```bash
codex -m gpt-5 --auto-edit "Think deeply: Fix performance bottleneck in $COMPONENT"
```

### security vulnerabilities
```bash
codex -m gpt-5 --auto-edit "Think deeply: Fix security vulnerability: $VULNERABILITY_DESCRIPTION"
```

### build failures
```bash
codex -m gpt-5 --auto-edit "Think deeply: Fix build errors and ensure successful compilation"
```
</specialized_fixes>

<integration_patterns>
## workflow integration

### fix pipeline
```bash
# 1. Diagnose with gemini
/external:gemini:analyze identify issues

# 2. Fix with cursor-agent
/external:cursor-agent:fix implementation

# 3. Verify with tests
/test run all

# 4. Review with gemini
/external:gemini:audit verify fix
```

### continuous fixing
```bash
# iterative improvement
/external:cursor-agent:fix critical bugs
/external:cursor-agent:test add coverage
/external:cursor-agent:fix remaining issues
/external:gemini:audit final check
```
</integration_patterns>

<best_practices>
## optimal usage

### when to use cursor-agent:fix
- bug fixes
- type errors
- test failures
- build issues
- performance problems
- security patches

### fix prioritization
- fix critical issues first
- address root causes
- prevent regressions
- improve error handling
- add missing tests
</best_practices>

<output_format>
## 🔧 cursor-agent fixing

**issue**: {{issue_description}}  
**severity**: {{severity_level}}  
**root cause**: {{root_cause}}  

### 🔍 diagnosis

error type: {{error_type}}
affected files: {{affected_files}}
impact: {{impact_assessment}}

### ✅ fix applied

files modified:
{{modified_files}}

changes made:
{{change_summary}}

### 🧪 verification

- tests: {{test_status}}
- types: {{type_check_status}}
- build: {{build_status}}

### 🎯 prevention

recommendations:
{{preventive_measures}}

### 🚀 next steps

{{follow_up_actions}}

---
✨ fix complete. see `cursor-fix.log` for details
</output_format>

$ARGUMENTS</cursor_fix_directive>