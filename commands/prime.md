# Prime Context Command

Quickly understand the current project state, structure, and development patterns.

<prime_directive>
You are tasked with efficiently understanding the current project context by analyzing the codebase structure, recent changes, documentation, and established patterns. This provides a foundation for effective assistance.

<components>
  <use>@xml-transformer</use>
  <use>@thinking-blocks</use>
  <use>@output-standards</use>
</components>

<references>
@file:~/Developer/STANDARDS.md
@file:~/.claude/rules/
@file:~/.claude/CLAUDE.md
</references>

<universal_input_handler>
Process $ARGUMENTS to detect and handle:

**Project Paths:**
- Analyze specific directories mentioned
- Focus on particular areas of interest

**Questions About State:**
- Current implementation status
- Recent changes and progress
- Technical debt areas

**Context Requests:**
- Architecture overview needed
- Pattern identification
- Convention understanding
</universal_input_handler>

<prompt_transformation>
<!-- Transform input to structured format -->
<input_analysis>
  <raw_input>$ARGUMENTS</raw_input>
  <detect_focus>
    - Specific project or directory
    - Technology stack questions
    - Architecture understanding
    - Recent changes analysis
    - General orientation
  </detect_focus>
</input_analysis>

<context_requirements>
  <project_scope>
    - Current directory analysis
    - Git repository status
    - Project type detection
    - Tech stack identification
  </project_scope>
  
  <depth_level>
    - Quick overview requested
    - Deep analysis needed
    - Specific area focus
  </depth_level>
</context_requirements>
</prompt_transformation>

<thinking_process>
<!-- Clear reasoning about project context -->
<analysis_thinking>
  <understanding_phase>
    Let me understand what context is needed:
    - Current project structure and setup
    - Technology stack in use
    - Recent changes and git status
    - Key patterns and conventions
  </understanding_phase>
  
  <analysis_approach>
    My approach:
    1. Scan project structure
    2. Identify tech stack
    3. Check recent activity
    4. Extract patterns
    5. Synthesize insights
  </analysis_approach>
  
  <key_questions>
    What to discover:
    - What type of project is this?
    - What's been recently changed?
    - What patterns are established?
    - What needs attention?
  </key_questions>
</analysis_thinking>
</thinking_process>

<project_analysis_execution>
# Core Analysis Tasks

## 1. Project Structure Analysis
- Identify project type (Next.js, React, Node, etc.)
- Scan directory structure
- Locate key configuration files
- Understand workspace/monorepo setup

## 2. Technology Stack Discovery
Check for:
- package.json dependencies
- Framework versions
- Build tools and configs
- Development scripts

## 3. Recent Activity Check
Git analysis:
- Recent commits (last 10-20)
- Changed files
- Current branch
- Uncommitted changes

## 4. Pattern Recognition
Identify:
- Code organization patterns
- Component structure
- State management approach
- API patterns
- Testing approach

## 5. Documentation Scan
Review:
- README files
- CLAUDE.md files
- Architecture docs
- API documentation
</project_analysis_execution>

<verification_phase>
<!-- Quick checks before analysis -->
<environment_check>
  <git_repo>Check if in git repository</git_repo>
  <project_files>Verify project files exist</project_files>
  <permissions>Ensure read access</permissions>
</environment_check>
</verification_phase>

<output_format>
## 🎯 Project Context

### 📁 Project Overview
**Type**: [Project type identified]
**Stack**: [Technology stack]
**Structure**: [Monorepo/Single/etc]

### 🔄 Recent Activity
**Current Branch**: `branch-name`
**Recent Changes**:
- Last commit: [message]
- Modified files: [count]
- Active areas: [list]

### 🏗️ Architecture Insights
**Patterns Detected**:
- [Pattern 1]: [Description]
- [Pattern 2]: [Description]

**Key Directories**:
- `/src`: [Purpose]
- `/components`: [Organization]
- `/api`: [Structure]

### 🛠️ Development Setup
**Scripts Available**:
- `npm run dev`: Development server
- `npm run build`: Production build
- `npm test`: Run tests

**Key Dependencies**:
- Framework: [Version]
- Major libs: [List]

### 📋 Recommendations
Based on analysis:
1. **Immediate**: [What needs attention]
2. **Next Steps**: [Logical next actions]
3. **Patterns to Follow**: [Conventions detected]

### 🚀 Ready to Assist
I now understand:
- ✓ Project structure and conventions
- ✓ Recent development activity
- ✓ Technology stack and patterns
- ✓ Current state and needs

**Suggested Next Commands**:
- `/user:build [feature]` - Implement features
- `/user:create [component]` - Create new elements
- `/user:audit` - Check code quality
- `/user:docs` - Update documentation

---
*Context loaded. How can I help you today?*
</output_format>

<advanced_features>
## Smart Context Detection

### Monorepo Awareness
If Turborepo/Nx detected:
- Map workspace structure
- Identify apps vs packages
- Understand shared dependencies
- Track cross-project imports

### Framework-Specific Analysis
**Next.js Projects**:
- App Router vs Pages Router
- API route structure
- Middleware setup
- ISR/SSG configuration

**React Native/Expo**:
- Platform-specific code
- Native module usage
- Navigation setup

**Node.js APIs**:
- Route organization
- Middleware stack
- Database connections
- Authentication setup

### AI/ML Project Detection
Look for:
- AI service directories
- Model configurations
- Training scripts
- Inference endpoints

### Quick Insights
Provide immediate value:
- "I notice you're using [pattern], which is great for [benefit]"
- "Recent commits focus on [area], shall we continue there?"
- "Your [feature] follows [pattern], I'll maintain consistency"
</advanced_features>

$ARGUMENTS</build_execution_directive>