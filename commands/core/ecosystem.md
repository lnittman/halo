# Ecosystem Command

Analyze, standardize, and evolve your entire developer ecosystem from a meta perspective.

<components>
  <use>@thinking-blocks</use>
  
  <use>@xml-transformer</use>
  <use>@verification-patterns</use>
  <use>@output-standards</use>
  <use>@task-execution</use>
</components>

<references>
@file:~/Developer/STANDARDS.md
@file:~/Developer/docs/apps/patterns.md
@file:~/Developer/docs/tools/claude-code-power-user.md
@file:~/Developer/docs/apps/docs.md
@file:~/.claude/rules/index.md
@file:~/.claude/rules/product_layout.md
@file:~/.claude/rules/documentation_and_ai_guidance.md
@file:~/.claude/rules/turborepo_tooling.md
@file:~/.claude/rules/turborepo_monorepo_structure.md
@file:~/.claude/rules/turborepo_state_management.md
@file:~/.claude/rules/turborepo_api_and_data_flow.md
@file:~/.claude/rules/ai_service_architecture.md
@file:~/.claude/rules/ai_agent_instructions.md
@file:~/.claude/rules/apple_project_structure.md
@file:~/.claude/rules/apple_architecture_patterns.md
@file:~/.claude/rules/apple_ui_ux_patterns.md
@file:~/.claude/rules/apple_networking_layer.md
</references>

<ecosystem_directive>
You are tasked with providing meta-level intelligence across the entire ~/Developer ecosystem. This command operates above individual projects to analyze patterns, enforce standards, propagate improvements, and extract collective wisdom.
<universal_input_handler>
Process $ARGUMENTS to detect operation type and scope:

**Operation Types:**
- `audit` - Analyze projects for patterns and compliance
- `standards` - Check and enforce architectural standards
- `evolve` - Propagate changes across projects
- `wisdom` - Extract learnings and patterns

**Scope Options:**
- `all` - All projects in ecosystem
- `apps/*` - All turborepo projects
- `*-ai` - All AI services
- `*-apple` - All Apple projects
- `*-docs` - All documentation
- Specific project names

**Mixed Content:**
- URLs → Fetch standards/patterns to apply
- Code blocks → Patterns to propagate
- File paths → Reference implementations
</universal_input_handler>

<thinking_process>
<extended_thinking>
  <understanding_phase>
    <operation_analysis>
    Let me understand what ecosystem operation is needed:
    - Operation type: [audit|standards|evolve|wisdom]
    - Scope: [all|specific pattern]
    - Intent: [analyze|enforce|propagate|extract]
    </operation_analysis>
    
    <ecosystem_context>
    Current ecosystem state:
    - Number of projects
    - Common patterns identified
    - Known divergences
    - Recent changes
    </ecosystem_context>
  </understanding_phase>
  
  <analysis_phase>
    <pattern_detection>
    Looking for patterns across:
    - Directory structures
    - Dependencies and versions
    - Code organization
    - Architectural decisions
    - Common utilities
    </pattern_detection>
    
    <standards_comparison>
    Comparing against STANDARDS.md:
    - Compliance check
    - Drift detection
    - Best practice identification
    - Anti-pattern detection
    </standards_comparison>
  </analysis_phase>
  
  <execution_phase>
    <sequential_analysis>
    Analyzing projects systematically:
    - Structure analysis
    - Dependency audit
    - Pattern extraction
    - Performance metrics
    </sequential_analysis>
    
    <synthesis>
    Combining findings:
    - Common patterns
    - Divergences
    - Opportunities
    - Recommendations
    </synthesis>
  </execution_phase>
</extended_thinking>
</thinking_process>

<operation_handlers>

## Audit Operation

When `audit` is specified:

**Task 1: Structure Analysis**
- Map all project structures
- Identify naming patterns
- Check directory organization
- Validate monorepo setup

**Task 2: Dependency Analysis**
- Extract all package.json files
- Compare dependency versions
- Identify outdated packages
- Check for security issues

**Task 3: Pattern Analysis**
- Analyze code organization
- Extract common utilities
- Identify shared patterns
- Detect anti-patterns

**Task 4: Standards Compliance**
- Compare against STANDARDS.md
- Identify deviations
- Calculate compliance score
- Generate fix recommendations

## Standards Operation

When `standards check` is specified:

**Rule-Based Verification:**
Check each project against all applicable rules from ~/.claude/rules/:

1. **Product Layout Rules**
   - Repository naming ([product]-xyz, -ai, -apple, -docs)
   - Monorepo vs standalone service structure
   - Required directories presence

2. **Documentation Rules**
   - CLAUDE.md/AGENTS.md presence in key directories
   - TSDoc/JSDoc on exported items
   - Agent instructions in XML format

3. **Turborepo Rules**
   - pnpm as package manager
   - TypeScript strict mode
   - Biome configuration
   - Required packages structure
   - State management patterns (RSC → SWR → Jotai)
   - API patterns (Server Actions primary)

4. **AI Service Rules**
   - Mastra framework usage
   - Agent/tool/workflow structure
   - Lazy model initialization
   - Storage patterns

5. **Apple Platform Rules**
   - Swift package structure
   - MVVM architecture
   - Technical UI patterns
   - Actor-based networking

**Enforcement Tasks:**
1. Generate detailed compliance reports per rule
2. Create automated fix scripts where possible
3. Update configurations to match rules
4. Standardize dependencies across projects

## Evolve Operation

When `evolve` is specified with a change:

**Planning Phase:**
1. Identify affected projects
2. Create change plan
3. Generate migration scripts
4. Estimate impact

**Execution Phase:**
1. Create branches
2. Apply changes
3. Run tests
4. Generate PRs

## Wisdom Operation

When `wisdom` is specified:

**Pattern Extraction:**
1. Common code patterns
2. Repeated solutions
3. Architectural decisions
4. Performance optimizations

**Learning Synthesis:**
1. Success patterns
2. Failure patterns
3. Evolution trends
4. Best practices

</operation_handlers>

<output_format>
## 🌍 Ecosystem Analysis: $OPERATION

### 📊 Overview
- **Projects Analyzed**: [count]
- **Operation**: [audit|standards|evolve|wisdom]
- **Scope**: [what was analyzed]
- **Timestamp**: [ISO timestamp]

### 🔍 Key Findings

#### Compliance Status
| Standard | Compliance | Projects | Issues |
|----------|------------|----------|--------|
| Structure | [%] | [list] | [count] |
| Dependencies | [%] | [list] | [count] |
| Documentation | [%] | [list] | [count] |
| Testing | [%] | [list] | [count] |

#### Pattern Analysis
$PATTERN_FINDINGS

#### Recommendations
$RECOMMENDATIONS

### 📈 Metrics

#### Dependency Health
- Outdated packages: [count]
- Security issues: [count]
- Version mismatches: [count]

#### Code Quality
- TypeScript coverage: [%]
- Test coverage: [avg %]
- Documentation coverage: [%]

### 🎯 Action Items

**Immediate** (Address within 24h):
- [ ] [Critical issue 1]
- [ ] [Critical issue 2]

**Short-term** (This week):
- [ ] [Important improvement 1]
- [ ] [Important improvement 2]

**Long-term** (This month):
- [ ] [Strategic enhancement 1]
- [ ] [Strategic enhancement 2]

### 🔄 Evolution Opportunities

$EVOLUTION_SUGGESTIONS

### 💡 Extracted Wisdom

$WISDOM_INSIGHTS

<context_output>
## 🔗 Command Context
**Command**: /user:ecosystem $OPERATION
**Timestamp**: [ISO timestamp]
**Projects**: [count analyzed]

**Key Insights**:
- operation: $OPERATION
- compliance_score: [percentage]
- patterns_found: [count]
- improvements_available: [count]
- next_steps:
  - specific recommendation 1
  - specific recommendation 2

**Suggested Commands**:
- `/user:ecosystem evolve [pattern]` - Propagate improvements
- `/user:create [project]` - Create compliant project
- `/user:prime [project]` - Deep dive on specific project
</context_output>
</output_format>

<operation_examples>

## Example: Full Audit
**Command**: /user:ecosystem audit all
**Result**: Analyzes entire ecosystem for patterns, compliance, and opportunities.

## Example: Standards Check
**Command**: /user:ecosystem standards check apps/*
**Result**: Verifies all turborepo projects against STANDARDS.md.

## Example: Dependency Evolution
**Command**: /user:ecosystem evolve "next@15 tailwind@4"
**Result**: Updates all projects to latest framework versions.

## Example: Pattern Wisdom
**Command**: /user:ecosystem wisdom patterns auth
**Result**: Extracts all authentication patterns across projects.

## Example: Targeted Analysis
**Command**: /user:ecosystem audit arbor-* kumori-*
**Result**: Analyzes specific project families.

</operation_examples>

<best_practices>
1. Run audit before major changes
2. Check standards weekly
3. Evolve dependencies monthly
4. Extract wisdom quarterly
5. Document findings in STANDARDS.md
6. Create snapshot before evolution
7. Test changes in one project first
8. Execute systematically for clarity
</best_practices>

<error_handling>
- Missing projects → Skip with warning
- Access errors → Report and continue
- Malformed files → Log and skip
- Network issues → Retry with backoff
</error_handling>
</ecosystem_directive>

$ARGUMENTS
