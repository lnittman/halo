# 🌟 external:cursor:prime - read-only initialization with sonnet 1m context

comprehensive project analysis using cursor's sonnet 4 model with 1m token context window for deep understanding without modifications.

<cursor_prime_directive>
you orchestrate cursor-agent with sonnet 4 to establish comprehensive project context. leverage the 1m token window for deep codebase understanding in READ-ONLY mode. after analysis, provide the ideal next halo command with a mini PRD spec.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
  <use>@file:~/.halo/components/next-command.md</use>
</components>

<model_selection>
## intelligent model choice

**use sonnet 4 for prime** - 1m context window enables full codebase loading
**never use opus** - explicitly avoided
**fallback to gpt-5** - if context is smaller or reasoning depth needed
</model_selection>

<initialization_protocol>
## comprehensive initialization with cursor

when executing prime:

1. **analyze entire codebase with sonnet**
2. **identify immediate improvements**
3. **create initial fixes/enhancements**
4. **establish development context**
5. **prepare for subsequent tasks**

cursor's sonnet advantages:
- 1m context window for large codebases
- gpt-5 fallback for complex reasoning
- generates actionable insights
- prepares specs for next commands
</initialization_protocol>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify cursor installation**
```bash
which cursor-agent || curl https://cursor.com/install -fsSL | bash
```

2. **gather codebase with repomix (optimized for 1M tokens)**
```bash
# use repomix to gather comprehensive context
npx repomix \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --ignore 'build/**' \
  --ignore '*.lock' \
  --ignore 'coverage/**' \
  --ignore '.next/**' \
  --output-file .repomix-context.md

# check context size and trim if needed
CONTEXT_SIZE=$(wc -c < .repomix-context.md)
MAX_SIZE=$((1000000 * 3))  # ~1M tokens ≈ 3M chars

if [ $CONTEXT_SIZE -gt $MAX_SIZE ]; then
  echo "Context too large ($CONTEXT_SIZE bytes), trimming to fit 1M tokens..."
  
  # smart trimming: keep structure, remove large files
  head -c $((MAX_SIZE / 2)) .repomix-context.md > .context-start.md
  tail -c $((MAX_SIZE / 2)) .repomix-context.md > .context-end.md
  
  cat > .repomix-context-trimmed.md << 'EOF'
# TRIMMED CONTEXT (Optimized for Sonnet 1M tokens)
[First half of codebase]
EOF
  cat .context-start.md >> .repomix-context-trimmed.md
  echo "\n\n[... middle section trimmed to fit 1M token limit ...]\n\n" >> .repomix-context-trimmed.md
  echo "[Second half of codebase]" >> .repomix-context-trimmed.md
  cat .context-end.md >> .repomix-context-trimmed.md
  
  mv .repomix-context-trimmed.md .repomix-context.md
  rm .context-start.md .context-end.md
  echo "Context trimmed to fit within 1M tokens"
else
  echo "Context size OK: $CONTEXT_SIZE bytes (~$(($CONTEXT_SIZE / 3000)) tokens)"
fi

# create initialization prompt with repomix context
cat > .cursor-prime-prompt.txt << 'EOF'
# PROJECT INITIALIZATION WITH SONNET 1M CONTEXT

[IMPORTANT: Use Sonnet 4 model for maximum context window]
[Context gathered with repomix - comprehensive codebase included below]

You are performing a comprehensive READ-ONLY project analysis. With Sonnet's 1M context and repomix data, analyze the entire codebase without making modifications.

## Initialization Requirements

### 1. Comprehensive Analysis
- Map entire project architecture
- Identify all major systems and components
- Detect patterns and anti-patterns
- Find security vulnerabilities
- Locate performance bottlenecks
- Assess technical debt

### 2. Analysis Without Modifications
Based on your analysis, document:
- Critical security issues to fix
- Missing type definitions needed
- Essential configuration files absent
- Obvious bugs discovered
- Error handling gaps
- Test coverage missing

### 3. Project Understanding
Document your findings:
- Project type and purpose
- Technology stack
- Architecture patterns
- Key dependencies
- Development workflow
- Build and deployment process

### 4. Code Quality Assessment
- Code consistency analysis
- Test coverage evaluation
- Documentation completeness
- Performance metrics
- Security posture
- Scalability assessment

### 5. Readiness Assessment
Assess development readiness:
- Dependency installation status
- Build process health
- Test suite status
- Linting configuration
- TypeScript setup
- Development server state

## Execution Instructions

1. **Analyze First**
   - Load all relevant files
   - Build mental model of architecture
   - Identify critical issues

2. **Document Issues (NO FIXES)**
   - List security vulnerabilities
   - Note build/compilation errors
   - Identify missing critical files
   - Catalog type errors
   - Record obvious bugs

3. **Prepare Recommendations**
   - Suggest configuration additions
   - Propose test strategies
   - Recommend error handling
   - Plan type safety improvements
   - Identify documentation needs

4. **Prepare for Next Steps**
   - List remaining improvements
   - Prioritize technical debt
   - Suggest architecture enhancements
   - Identify optimization opportunities

## Model Selection
- USE: Sonnet 4 (for 1M context capability)
- AVOID: Opus (never use)
- FALLBACK: GPT-5 (only if context fits)

## Success Criteria
- [ ] Full codebase analyzed
- [ ] Critical issues identified
- [ ] Build status assessed
- [ ] Test coverage evaluated
- [ ] Development readiness documented
- [ ] Next command with spec prepared

## Output Format

### Executive Summary
- Project overview
- Health score
- Critical fixes applied
- Remaining issues

### Detailed Analysis
1. Architecture Map
2. Technology Assessment
3. Security Report
4. Performance Analysis
5. Code Quality Metrics

### Recommended Actions
- Files to create
- Files to modify
- Issues to fix
- Tests to add
- Configurations to update

### Next Steps
- Immediate priorities
- Short-term improvements
- Long-term recommendations

## Repomix Context (Full Codebase)
$(cat .repomix-context.md)
EOF
```

3. **execute cursor with sonnet (read-only)**
```bash
# use sonnet for maximum context with repomix data
if [ -f ".repomix-context.md" ]; then
  echo "Executing with repomix context ($(wc -c < .repomix-context.md) bytes)..."
  
  # cursor-agent with sonnet 4 handles large context well (1M tokens)
  cursor-agent chat --model sonnet-4 "$(cat .cursor-prime-prompt.txt)" 2>&1 | tee cursor-prime-results.log
else
  echo "ERROR: Repomix context not found. Run repomix first."
  exit 1
fi

# note: sonnet-4 in cursor has 1M token context, perfect for repomix output
```

4. **prepare next command spec**
```bash
# extract key findings
grep -A 20 "Critical Issues" cursor-prime-results.log > issues.md
grep -A 20 "Recommended Actions" cursor-prime-results.log > actions.md

# create mini PRD for next command
cat > next-command-spec.md << 'EOF'
# NEXT COMMAND SPECIFICATION

## Recommended Command
[Based on analysis, the ideal next command]

## Mini PRD
[Concise requirements for the next action]

## Success Criteria
[Clear success metrics]

## Context
[Key findings from prime analysis]
EOF

echo "=== ANALYSIS COMPLETE ==="
cat next-command-spec.md
```
</execution_workflow>

<orchestration_integration>
## halo orchestration pattern

### receiving specs from claude
when claude provides detailed specifications:
```bash
# claude writes spec
cat > .implementation-spec.md << 'EOF'
[Claude's detailed PRDA with requirements]
EOF

# cursor executes with full context
cursor-agent chat --model sonnet-4 "$(cat .implementation-spec.md)"
```

### handoff workflow
```bash
# 1. Claude gathers context
/prime  # claude's initialization

# 2. Claude writes spec
/build detailed specification

# 3. Cursor prime with spec
/external:cursor:prime with claude's analysis

# 4. Cursor implements
/external:cursor:build execute specification
```
</orchestration_integration>

<best_practices>
## optimal usage

### when to use cursor:prime
- project onboarding
- codebase health check
- pre-refactoring analysis
- security audit with fixes
- development environment setup

### model selection strategy
- sonnet for large context (>100k tokens)
- gpt-5 for complex reasoning
- never use opus
- let cursor auto-select when uncertain

### context optimization
- include all source files
- include configurations
- include documentation
- exclude build artifacts
- exclude node_modules
</best_practices>

<output_format>
## 🌟 cursor prime initialization

**model**: sonnet 4 (1m context)  
**scope**: full codebase analysis  
**mode**: analyze + immediate fixes  

### 📊 initialization phases

1. ✓ codebase analyzed ({{file_count}} files)
2. ✓ critical issues identified
3. ⚡ fixes being applied...
4. ✓ development environment prepared

### 📋 findings

critical issues:
{{critical_issues}}

missing components:
{{missing_components}}

improvement areas:
{{improvement_areas}}

### 💡 key insights

architecture:
{{architecture_summary}}

health score:
{{health_metrics}}

---
✨ analysis complete.

<!-- generate next command with comprehensive PRD -->
<use>@file:~/.halo/components/next-command.md</use>
</output_format>

$ARGUMENTS</cursor_prime_directive>