# 🎯 prime context command

quickly understand the current project state, structure, and development patterns.

<prime_directive>
you are tasked with efficiently understanding the current project context by analyzing the codebase structure, recent changes, documentation, and established patterns. this provides a foundation for effective assistance.

<components>
  <use>@xml-transformer</use>
  <use>@thinking-blocks</use>
  <use>@output-standards</use>
  <use>@next-commands</use>
</components>

<references>
@file:~/Developer/STANDARDS.md
@file:~/.claude/rules/
@file:~/.claude/CLAUDE.md
</references>

<universal_input_handler>
process $ARGUMENTS to detect and handle:

**project paths:**
- analyze specific directories mentioned
- focus on particular areas of interest

**questions about state:**
- current implementation status
- recent changes and progress
- technical debt areas

**context requests:**
- architecture overview needed
- pattern identification
- convention understanding
</universal_input_handler>

<prompt_transformation>
<!-- transform input to structured format -->
<input_analysis>
  <raw_input>$ARGUMENTS</raw_input>
  <detect_focus>
    - specific project or directory
    - technology stack questions
    - architecture understanding
    - recent changes analysis
    - general orientation
  </detect_focus>
</input_analysis>

<context_requirements>
  <project_scope>
    - current directory analysis
    - git repository status
    - project type detection
    - tech stack identification
  </project_scope>
  
  <depth_level>
    - quick overview requested
    - deep analysis needed
    - specific area focus
  </depth_level>
</context_requirements>
</prompt_transformation>

<thinking_process>
<!-- clear reasoning about project context -->
<analysis_thinking>
  <understanding_phase>
    let me understand what context is needed:
    - current project structure and setup
    - technology stack in use
    - recent changes and git status
    - key patterns and conventions
  </understanding_phase>
  
  <analysis_approach>
    my approach:
    1. scan project structure
    2. identify tech stack
    3. check recent activity
    4. extract patterns
    5. synthesize insights
  </analysis_approach>
  
  <key_questions>
    what to discover:
    - what type of project is this?
    - what's been recently changed?
    - what patterns are established?
    - what needs attention?
  </key_questions>
</analysis_thinking>
</thinking_process>

<project_analysis_execution>
# core analysis tasks

## 1. project structure analysis
- identify project type (Next.js, React, Node, etc.)
- scan directory structure
- locate key configuration files
- understand workspace/monorepo setup

## 2. technology stack discovery
check for:
- package.json dependencies
- framework versions
- build tools and configs
- development scripts

## 3. recent activity check
git analysis:
- recent commits (last 10-20)
- changed files
- current branch
- uncommitted changes

## 4. pattern recognition
identify:
- code organization patterns
- component structure
- state management approach
- API patterns
- testing approach

## 5. documentation scan
review:
- README files
- CLAUDE.md files
- architecture docs
- API documentation
</project_analysis_execution>

<verification_phase>
<!-- quick checks before analysis -->
<environment_check>
  <git_repo>check if in git repository</git_repo>
  <project_files>verify project files exist</project_files>
  <permissions>ensure read access</permissions>
</environment_check>
</verification_phase>

<output_format>
## 🎯 project context

**type**: [project_type]  
**stack**: [tech_stack]  
**health**: [pct]% 🟢🟢🟢🟢🔴

### 📡 recent activity
- **branch**: [branch] - [last_commit_msg]
- **modified**: [n] files
- **focus**: [active_area]

### 🏗️ architecture
- **pattern**: [main_pattern]
- **structure**: [org_type]
- **style**: [code_style]

### 📁 key directories
- 📁 `/src` → [purpose]
- 📦 `/packages` → [purpose]
- 🔧 `/config` → [purpose]

### ⚡ available scripts
- `dev` → start development
- `build` → production build
- `test` → run test suite

{{#if insights}}
### 💡 insights
- [insight_1]
- [insight_2]
{{/if}}

{{#if needs_attention}}
### ⚠️ attention needed
- [issue_1]
- [issue_2]
{{/if}}

<!-- next command generation using component -->
<generate_next_command>
  <use>@next-commands</use>
  <!-- component will generate THE best next command -->
</generate_next_command>

---
✨ ready. run the command above or tell me what you need.
</output_format>

<advanced_features>
## smart context detection

### monorepo awareness
if turborepo/nx detected:
- map workspace structure
- identify apps vs packages
- understand shared dependencies
- track cross-project imports

### framework-specific analysis
**Next.js projects**:
- app router vs pages router
- API route structure
- middleware setup
- ISR/SSG configuration

**React Native/Expo**:
- platform-specific code
- native module usage
- navigation setup

**Node.js APIs**:
- route organization
- middleware stack
- database connections
- authentication setup

### AI/ML project detection
look for:
- AI service directories
- model configurations
- training scripts
- inference endpoints

### quick insights
provide immediate value:
- "noticed you're using [pattern] ✨"
- "recent work focuses on [area] 🎯"
- "following [convention] consistently ✓"
</advanced_features>

$ARGUMENTS</prime_directive>