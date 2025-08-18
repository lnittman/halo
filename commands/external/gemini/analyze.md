# 🔬 external:gemini:analyze - deep pattern & architecture analysis

leverage gemini's 2m context for comprehensive pattern extraction and architectural analysis.

<gemini_analyze_directive>
you orchestrate gemini cli with repomix for deep codebase analysis, pattern extraction, and architectural insights.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
  <use>@file:~/.halo/components/repomix-context.md</use>
</components>

<analysis_capabilities>
## comprehensive analysis scope

### pattern detection
- design patterns in use
- architectural patterns
- anti-patterns present
- code smells
- duplication patterns
- naming conventions

### architecture mapping
- component relationships
- dependency graphs
- data flow patterns
- control flow analysis
- boundary definitions
- layer violations
</analysis_capabilities>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify gemini installation**
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

2. **gather complete codebase**
```bash
npx repomix \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --ignore 'build/**' \
  --output-file .analysis-context.md
```

3. **create analysis prompt**
```bash
cat > .gemini-analyze-prompt.md << 'EOF'
# DEEP PATTERN & ARCHITECTURE ANALYSIS

Think deeply and perform exhaustive analysis of patterns, architecture, and code quality.

## Analysis Requirements
$ARGUMENTS

## Analysis Dimensions

### 1. Pattern Analysis
- **Design Patterns**
  - Identify all patterns in use
  - Evaluate pattern implementation quality
  - Suggest missing beneficial patterns
  - Flag pattern misuse

- **Anti-Patterns**
  - Detect anti-patterns
  - Assess impact severity
  - Provide refactoring suggestions
  - Prioritize fixes

### 2. Architecture Analysis
- **Structure**
  - Map component hierarchy
  - Identify architectural layers
  - Detect boundary violations
  - Assess coupling/cohesion

- **Dependencies**
  - Create dependency graph
  - Identify circular dependencies
  - Find unused dependencies
  - Detect version conflicts

### 3. Code Quality Metrics
- **Complexity**
  - Cyclomatic complexity hotspots
  - Cognitive complexity issues
  - Nested depth problems
  - Method/file size violations

- **Maintainability**
  - Code duplication analysis
  - Dead code detection
  - Documentation coverage
  - Test coverage gaps

### 4. Performance Analysis
- **Bottlenecks**
  - Algorithm efficiency issues
  - Database query problems
  - Memory leak potential
  - CPU-intensive operations

- **Optimization Opportunities**
  - Caching candidates
  - Parallelization potential
  - Lazy loading opportunities
  - Bundle size reductions

### 5. Best Practices Compliance
- **Standards Adherence**
  - Coding standards violations
  - Framework best practices
  - Security best practices
  - Accessibility compliance

## Output Format

### Executive Summary
- Overall health score
- Critical issues count
- Improvement opportunities
- Quick wins available

### Detailed Findings

#### Patterns Report
- Patterns in use: [list with examples]
- Anti-patterns found: [list with locations]
- Recommended patterns: [suggestions with rationale]

#### Architecture Report
- System architecture diagram (text)
- Component relationships
- Layer violations
- Dependency issues

#### Quality Metrics
- Complexity scores
- Maintainability index
- Technical debt estimate
- Coverage statistics

#### Action Items
[Prioritized list with effort estimates]

### Visualization Data
[Data for generating diagrams]

### Refactoring Roadmap
[Step-by-step improvement plan]

## Context
$(cat .analysis-context.md)
EOF
```

4. **execute gemini analysis**
```bash
cat .gemini-analyze-prompt.md | gemini > analysis-report.md 2>&1
```

5. **process results**
```bash
# extract patterns
grep -A 30 "Patterns Report" analysis-report.md > patterns.md

# extract architecture insights
grep -A 50 "Architecture Report" analysis-report.md > architecture.md

# extract action items
grep -A 40 "Action Items" analysis-report.md > action-items.md

# display summary
echo "=== ANALYSIS SUMMARY ==="
head -75 analysis-report.md
```
</execution_workflow>

<specialized_analysis>
## focused analysis modes

### pattern extraction
```bash
/external:gemini:analyze extract all design patterns

/external:gemini:analyze find anti-patterns and code smells
```

### architecture review
```bash
/external:gemini:analyze map component architecture

/external:gemini:analyze analyze dependency graph
```

### performance analysis
```bash
/external:gemini:analyze identify performance bottlenecks

/external:gemini:analyze suggest optimizations
```
</specialized_analysis>

<integration_patterns>
## workflow integration

### analysis pipeline
```bash
# 1. Analyze patterns
/external:gemini:analyze patterns

# 2. Plan refactoring
/external:codex:architect refactoring strategy

# 3. Implement improvements
/external:cursor-agent:refactor patterns.md

# 4. Verify improvements
/external:gemini:analyze verify changes
```

### continuous analysis
```bash
# regular health checks
/external:gemini:analyze weekly health check
/external:gemini:audit security focus
/external:gemini:analyze performance focus
```
</integration_patterns>

<output_format>
## 🔬 pattern & architecture analysis

**scope**: full codebase analysis  
**patterns found**: {{pattern_count}}  
**anti-patterns**: {{antipattern_count}}  
**architecture score**: {{arch_score}}/100  

### 📊 key findings

patterns in use:
{{pattern_list}}

critical issues:
{{critical_issues}}

### 🎯 improvement opportunities

quick wins:
{{quick_wins}}

strategic improvements:
{{strategic_improvements}}

### 💡 recommendations

1. {{recommendation_1}}
2. {{recommendation_2}}
3. {{recommendation_3}}

### 🚀 next actions

{{next_commands}}

---
✨ full analysis: `analysis-report.md`
</output_format>

$ARGUMENTS</gemini_analyze_directive>