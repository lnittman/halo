# 🌟 external:gemini:prime - initialize session with 2m context

comprehensive project initialization using gemini's 2m token context window with repomix for deep codebase understanding.

<gemini_prime_directive>
you orchestrate gemini cli with repomix to establish comprehensive project context. leverage the 2m token window for exhaustive codebase analysis and strategic initialization.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
  <use>@file:~/.halo/components/repomix-context.md</use>
</components>

<initialization_protocol>
## comprehensive initialization with gemini

when executing prime:

1. **gather full codebase context with repomix**
2. **analyze project architecture and patterns**
3. **identify key systems and dependencies**
4. **establish development context**
5. **suggest strategic next steps**

gemini's 2m context allows us to:
- load entire codebases in one shot
- maintain complete architectural awareness
- identify cross-cutting concerns
- detect subtle patterns and anti-patterns
</initialization_protocol>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify gemini installation**
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

2. **run comprehensive repomix scan**
```bash
# comprehensive codebase gathering
npx repomix \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --ignore 'build/**' \
  --ignore '*.lock' \
  --output-file .gemini-prime-context.md
```

3. **create prime initialization prompt**
```bash
cat > .gemini-prime-prompt.md << 'EOF'
# PROJECT INITIALIZATION & DEEP ANALYSIS

You are performing a comprehensive project initialization. Think deeply and provide exhaustive analysis.

## Analysis Requirements

### 1. Project Architecture
- Identify core architectural patterns
- Map system boundaries and interfaces
- Detect design patterns and anti-patterns
- Evaluate technical debt indicators

### 2. Codebase Health
- Code quality metrics
- Consistency analysis
- Security vulnerabilities
- Performance bottlenecks
- Test coverage gaps

### 3. Development Context
- Technology stack assessment
- Dependency analysis
- Build and deployment patterns
- Development workflow evaluation

### 4. Strategic Insights
- Improvement opportunities
- Risk areas
- Optimization potential
- Modernization paths

### 5. Immediate Priorities
- Critical issues to address
- Quick wins available
- Technical debt to tackle
- Security concerns

## Output Format

Provide a structured analysis with:

### Executive Summary
- Project type and purpose
- Current state assessment
- Key strengths and weaknesses

### Detailed Analysis
1. **Architecture Overview**
   - System design
   - Component relationships
   - Data flow patterns

2. **Code Quality Report**
   - Health metrics
   - Problem areas
   - Best practices adherence

3. **Technology Assessment**
   - Stack evaluation
   - Dependency health
   - Upgrade opportunities

4. **Risk Register**
   - Security vulnerabilities
   - Performance issues
   - Maintenance concerns

5. **Recommendations**
   - Immediate actions
   - Short-term improvements
   - Long-term strategy

### Next Commands
Suggest the most appropriate halo commands:
- `/external:gemini:audit` - for security review
- `/external:cursor-agent:build` - for feature implementation
- `/external:codex:architect` - for system design
- `/fix` - for immediate issues
- `/build` - for new features

## Context

$(cat .gemini-prime-context.md)
EOF
```

4. **execute gemini with full context**
```bash
# pipe to gemini for analysis (avoids arg length limits)
cat .gemini-prime-prompt.md | gemini > gemini-prime-analysis.md 2>&1
```

5. **process and display results**
```bash
# show analysis
cat gemini-prime-analysis.md

# save key insights
grep -A 10 "Executive Summary" gemini-prime-analysis.md > .project-insights.md
grep -A 20 "Immediate Priorities" gemini-prime-analysis.md > .priorities.md
```
</execution_workflow>

<prompt_optimization>
## gemini-specific prompt patterns

### leverage 2m context
- include entire codebase in single analysis
- cross-reference all files simultaneously
- detect system-wide patterns
- identify architectural inconsistencies

### deep reasoning triggers
- "think step by step through the entire codebase"
- "analyze relationships between all components"
- "identify patterns across the full system"
- "consider the complete architectural context"

### comprehensive output
- request detailed, structured analysis
- ask for specific code examples
- demand actionable recommendations
- require risk assessments
</prompt_optimization>

<integration_patterns>
## halo system integration

### session initialization
```bash
# standard flow
/external:gemini:prime  # comprehensive init
/prime                  # claude's focused init
/build                  # start development
```

### context handoff
- gemini provides full analysis → claude focuses on specifics
- gemini identifies patterns → cursor-agent implements
- gemini finds issues → codex plans solutions

### continuous analysis
```bash
# periodic re-initialization
/external:gemini:prime  # weekly full analysis
/external:gemini:audit  # daily security check
/external:gemini:analyze # on-demand deep dives
```
</integration_patterns>

<best_practices>
## optimal usage patterns

### when to use gemini:prime
- project onboarding
- major refactoring planning
- architecture reviews
- comprehensive audits
- migration planning

### context management
- use repomix with smart ignores
- focus on source code, not artifacts
- include configuration files
- preserve directory structure in output

### result utilization
- save analysis for reference
- extract actionable items
- create todo lists from findings
- share insights with team
</best_practices>

<advanced_features>
## enhanced initialization

### multi-phase analysis
```bash
# phase 1: architecture
/external:gemini:prime focus on architecture

# phase 2: security
/external:gemini:audit based on prime analysis

# phase 3: performance
/external:gemini:analyze performance bottlenecks
```

### comparative analysis
```bash
# compare with standards
cat ~/Developer/STANDARDS.md >> .gemini-prime-prompt.md
echo "Compare this codebase against these standards" >> .gemini-prime-prompt.md
```

### ai-enhanced review
```bash
# include ai guidance
cat ~/.halo/rules/*.md >> .gemini-prime-prompt.md
echo "Evaluate against these architectural rules" >> .gemini-prime-prompt.md
```
</advanced_features>

<output_format>
## 🌟 gemini prime initialization

**mode**: comprehensive analysis  
**context**: full codebase ({{file_count}} files, {{loc}} lines)  
**model**: gemini with 2m context  

### 📊 initialization phases

1. ✓ codebase gathered with repomix
2. ✓ context prepared ({{context_size}} tokens)
3. ✓ gemini analysis in progress...
4. ⏳ processing insights...

### 🎯 analysis focus

examining:
- architecture patterns
- code quality metrics
- security vulnerabilities
- performance bottlenecks
- technical debt

### 💡 strategic insights

*gemini analyzing with full context awareness...*

### 🚀 next steps

based on analysis:
- critical issues: {{critical_count}}
- improvement opportunities: {{opportunity_count}}
- recommended commands: {{next_commands}}

---
✨ prime initialization complete. full analysis available in `gemini-prime-analysis.md`
</output_format>

$ARGUMENTS</gemini_prime_directive>