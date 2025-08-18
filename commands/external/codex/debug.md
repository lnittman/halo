# 🐛 external:codex:debug - gpt-5 strategic debugging & root cause analysis

leverage codex's gpt-5 deep reasoning for complex debugging and root cause analysis.

<codex_debug_directive>
you orchestrate codex cli for strategic debugging of complex issues. use gpt-5's reasoning to understand intricate bugs and system failures.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<debug_capabilities>
## strategic debugging focus

- complex race conditions
- memory leaks
- performance degradation
- distributed system issues
- concurrency problems
- architectural bugs
- integration failures
- intermittent errors
</debug_capabilities>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **gather comprehensive debug context**
```bash
# collect all relevant logs
find . -name "*.log" -mtime -1 -exec tail -100 {} \; > .debug-logs.txt 2>/dev/null || true

# get system metrics if available
ps aux | head -20 > .system-state.txt
df -h >> .system-state.txt
free -h >> .system-state.txt 2>/dev/null || true

# capture recent git changes
git log --oneline -20 > .recent-changes.txt
git diff HEAD~5 --stat >> .recent-changes.txt
```

3. **create strategic debug prompt**
```bash
cat > .codex-debug-prompt.txt << 'EOF'
# GPT-5 STRATEGIC DEBUGGING & ROOT CAUSE ANALYSIS

Think deeply and systematically analyze this complex issue using first principles reasoning.

## Issue Description
$ARGUMENTS

## Debug Context
### Error Logs
$(cat .debug-logs.txt 2>/dev/null || echo "No logs available")

### System State
$(cat .system-state.txt 2>/dev/null || echo "No system metrics")

### Recent Changes
$(cat .recent-changes.txt 2>/dev/null || echo "No recent changes")

## Strategic Debugging Approach

### 1. Problem Characterization
- **Symptoms Analysis**
  - What exactly is failing?
  - When did it start failing?
  - Under what conditions does it fail?
  - Is it deterministic or intermittent?
  - What is the failure frequency?

- **Impact Assessment**
  - Which components are affected?
  - What is the blast radius?
  - Are there cascading failures?
  - What is the business impact?

### 2. Hypothesis Generation
- **Potential Root Causes**
  - List all possible causes
  - Rank by probability
  - Consider recent changes
  - Check for environmental factors
  - Evaluate external dependencies

- **Failure Scenarios**
  - Race conditions
  - Resource exhaustion
  - Configuration issues
  - Network problems
  - Data corruption
  - Timing issues

### 3. Systematic Investigation
- **Diagnostic Strategy**
  - What data do we need?
  - Which logs to examine?
  - What metrics to monitor?
  - Which components to isolate?
  - What experiments to run?

- **Root Cause Isolation**
  - Binary search approach
  - Component isolation
  - Time-based analysis
  - Correlation analysis
  - Causation verification

### 4. Solution Design
- **Fix Strategies**
  - Immediate mitigation
  - Short-term fix
  - Long-term solution
  - Preventive measures
  - Monitoring additions

- **Risk Assessment**
  - Fix complexity
  - Testing requirements
  - Rollback plan
  - Performance impact
  - Side effects

### 5. Prevention Planning
- **Systemic Improvements**
  - Architecture changes
  - Process improvements
  - Monitoring enhancements
  - Testing additions
  - Documentation updates

## Output Format

### Executive Summary
- Problem statement
- Root cause identified
- Recommended solution
- Risk assessment

### Detailed Analysis

#### Problem Diagnosis
[Systematic breakdown of the issue]

#### Root Cause Analysis
[Evidence-based root cause identification]

#### Investigation Steps
[Ordered list of diagnostic steps taken]

#### Solution Proposal
[Comprehensive fix strategy]

#### Implementation Plan
1. Immediate actions
2. Short-term fixes
3. Long-term improvements

#### Prevention Strategy
[How to prevent recurrence]

### Debugging Artifacts

#### Key Findings
[Critical discoveries during investigation]

#### Evidence Chain
[How we traced from symptom to cause]

#### Test Cases
[Tests to verify the fix]

### Monitoring Requirements
[What to monitor going forward]

### Documentation Needs
[What to document for future reference]

## Success Metrics
- Issue resolved
- No regressions
- Performance maintained
- Monitoring in place
- Documentation updated
- Team knowledge transferred
EOF
```

4. **execute codex debug analysis**
```bash
# use gpt-5 for deep debugging reasoning
codex exec -m gpt-5 -s read-only "$(cat .codex-debug-prompt.txt)" 2>&1 | tee debug-analysis.md
```

5. **process debug outputs**
```bash
# extract root cause
grep -A 15 "Root Cause Analysis" debug-analysis.md > root-cause.md

# extract solution
grep -A 30 "Solution Proposal" debug-analysis.md > solution.md

# extract immediate actions
grep -A 20 "Immediate actions" debug-analysis.md > immediate-actions.md

# display summary
echo "=== DEBUG ANALYSIS SUMMARY ==="
head -75 debug-analysis.md
```
</execution_workflow>

<specialized_debugging>
## debug patterns

### race condition analysis
```bash
codex -m gpt-5 "Think deeply: Debug race condition in concurrent system"
```

### memory leak investigation
```bash
codex -m gpt-5 "Think deeply: Trace and fix memory leak in $APPLICATION"
```

### performance degradation
```bash
codex -m gpt-5 "Think deeply: Debug performance regression since $VERSION"
```

### intermittent failures
```bash
codex -m gpt-5 "Think deeply: Debug intermittent failure occurring 30% of the time"
```

### distributed system issues
```bash
codex -m gpt-5 "Think deeply: Debug distributed consensus failure"
```
</specialized_debugging>

<integration_patterns>
## workflow integration

### debug pipeline
```bash
# 1. Gather context with gemini
/external:gemini:analyze full system

# 2. Debug with codex
/external:codex:debug strategic analysis

# 3. Implement fix with cursor
/external:cursor-agent:fix root cause

# 4. Verify with gemini
/external:gemini:audit verify resolution
```

### continuous debugging
```bash
# progressive debugging
/external:codex:debug initial analysis
/external:cursor-agent:fix immediate issues
/external:codex:debug deeper investigation
/external:cursor-agent:fix root causes
```
</integration_patterns>

<best_practices>
## optimal usage

### when to use codex:debug
- complex multi-component issues
- race conditions
- performance problems
- intermittent failures
- architectural bugs
- integration issues

### debugging methodology
- gather comprehensive context
- form multiple hypotheses
- test systematically
- verify root cause
- implement comprehensive fix
- add prevention measures
</best_practices>

<output_format>
## 🐛 strategic debugging

**issue**: {{issue_description}}  
**complexity**: {{complexity_level}}  
**impact**: {{impact_severity}}  

### 🔍 root cause analysis

symptoms:
{{symptom_list}}

root cause:
{{root_cause_description}}

evidence:
{{evidence_chain}}

### 🎯 solution strategy

immediate fix:
{{immediate_fix}}

long-term solution:
{{long_term_solution}}

### 📊 investigation findings

key discoveries:
{{key_findings}}

correlation factors:
{{correlation_factors}}

### 🛡️ prevention plan

monitoring:
{{monitoring_additions}}

improvements:
{{systemic_improvements}}

### 🚀 next steps

1. {{action_1}}
2. {{action_2}}
3. {{action_3}}

---
✨ full debug analysis: `debug-analysis.md`
</output_format>

$ARGUMENTS</codex_debug_directive>