# next commands component

provides THE single best contextually-aware next command with comprehensive spec by analyzing available commands and current context.

## usage

```xml
<use>@next-commands</use>
```

## implementation

```xml
<next_command_generation>
analyze the current context and available commands to determine THE SINGLE BEST next action.

<available_commands>
CORE COMMANDS:
- /prime - analyze and understand existing codebases
- /create - scaffold new project ecosystems from ideas
- /build - implement features and execute on plans
- /fix - debug and resolve errors from logs/traces
- /vision - explore AI-native product possibilities
- /design - create comprehensive design systems
- /brand - develop production-ready brand identity
- /diagram - generate visual architecture diagrams
- /ecosystem - analyze and evolve entire dev ecosystem
- /tech - deep research on technologies

MAINTENANCE:
- /audit - comprehensive codebase compliance analysis
- /docs - documentation audit and creation
- /sync - synchronize changes across ecosystem

SPECIALISTS:
- /test-coverage - write comprehensive test suites
- /dependency-doctor - manage and update dependencies
- /tech-docs - aggregate technology documentation
- /github-analyzer - analyze GitHub repositories
- /deployment-orchestrator - coordinate multi-platform deploys
- /interactive-playground - create live documentation

REFINERS:
- /simplify-design - remove complexity, find essence
- /polish-interface - add delightful micro-interactions
- /stack-expert-dev - deep technical implementation
- /docs-generator - transform research into documentation
- /tech-researcher - exhaustive technology analysis

BUILDERS:
- /3d-artist - Three.js and 3D experiences
- /motion-expert - animation and motion systems
- /video-studio - Remotion video creation
- /real-time-collaborative - multiplayer features
- /adaptive-systems - responsive architectures
- /minimalist-architect - essential-only design

INTEGRATIONS:
- /github-whisperer - Git/GitHub operations
- /cloudflare-whisperer - Cloudflare deployment
- /linear-whisperer - Linear project management

ROLES:
- /ai-architect - AI integration specialist
- /design-systems-architect - scalable component systems
- /product-orchestrator - strategic project management
- /creative-catalyst - unlock creative potential

ANALYZERS:
- /audit-codebase - code quality analysis
- /pattern-extractor - identify reusable patterns
</available_commands>

<command_analysis>
determine the single most valuable next action by analyzing:
- what was just completed and its output
- current project state and tech stack
- detected gaps, issues, or opportunities
- logical workflow progression patterns
- highest impact/effort ratio
- user's stated goals and context

selection criteria:
1. addresses most pressing current need
2. unblocks maximum future progress
3. builds on work just completed
4. respects project momentum
5. provides immediate value
</command_analysis>

<contextual_intelligence>
read key files to understand context:
- package.json for tech stack
- README for project goals
- recent file changes for momentum
- error logs for issues
- CLAUDE.md for standards

match patterns:
- after /prime → usually /build or /create
- after /create → usually /build core features
- after /build auth → usually /test-coverage
- after errors → usually /fix
- after refactor → usually /docs or /test-coverage
- when stuck → /creative-catalyst or /vision
- for cleanup → /simplify-design or /audit-codebase
</contextual_intelligence>

<prd_generation>
create comprehensive specs that include:

1. CONTEXT AWARENESS
   - reference specific files/components
   - use actual function/variable names
   - follow detected code patterns
   - respect existing architecture

2. TECHNICAL PRECISION
   - exact package versions
   - specific implementation paths
   - concrete code examples
   - integration points

3. SCOPE DEFINITION
   - clear boundaries
   - explicit non-goals
   - success criteria
   - time estimates

4. ACTIONABLE STEPS
   - numbered implementation order
   - specific file modifications
   - exact commands to run
   - validation checkpoints
</prd_generation>

<command_template>
structure the single best command as:

best_next_command:
  name: exact command from available_commands
  args: ultra-specific based on current context
  rationale: compelling reason this is THE next step
  prd: |
    # {{Specific Feature/Task Name}}
    
    ## 🎯 Objective
    {{Clear, measurable goal based on current context and what was just completed}}
    
    ## 📋 Context
    **Current State**: {{What exists now - reference specific files/components}}
    **Gap/Need**: {{What's missing or broken - be specific}}
    **Impact**: {{Why this matters now - user value and technical benefits}}
    **Dependencies**: {{What this unblocks or enables}}
    
    ## 🛠 Technical Requirements
    
    ### Architecture
    - **Pattern**: {{Specific pattern from codebase - e.g., "Follow existing hooks/use-auth.ts pattern"}}
    - **Location**: {{Exact directories and files to modify}}
    - **Integration**: {{How this connects to existing code}}
    
    ### Implementation Stack
    - **Core Tech**: {{From detected package.json - exact versions}}
    - **Libraries**: {{Specific packages to use}}
    - **Patterns**: {{Conventions from codebase}}
    
    ### Code Structure
    ```typescript
    // Example showing exact implementation approach
    // Using actual patterns from the codebase
    ```
    
    ## 📝 Detailed Implementation Plan
    
    ### Phase 1: Foundation ({{time}})
    1. **Setup {{specific component}}**
       - Create `{{exact/file/path.ts}}`
       - Implement {{specific pattern}}
       - Connect to {{existing system}}
    
    2. **Core Logic**
       ```typescript
       // Actual code structure to implement
       export function {{functionName}}() {
         // Pattern from existing code
       }
       ```
    
    ### Phase 2: Integration ({{time}})
    3. **Wire up {{specific integration}}**
       - Modify `{{existing/file.ts}}`
       - Add {{specific hooks/components}}
       - Update {{configuration}}
    
    ### Phase 3: Polish ({{time}})
    4. **Testing**
       - Unit tests for {{components}}
       - Integration tests for {{flows}}
       - E2E validation of {{user journey}}
    
    5. **Documentation**
       - Update README with {{feature}}
       - Add JSDoc to {{new functions}}
       - Create usage examples
    
    ## ✅ Success Criteria
    - [ ] {{Specific measurable outcome}}
    - [ ] {{Performance metric - e.g., "<100ms response"}}
    - [ ] {{User-facing improvement}}
    - [ ] All tests passing
    - [ ] No TypeScript errors
    
    ## 🚫 Out of Scope
    - {{What we're NOT doing}}
    - {{Features to avoid for now}}
    - {{Complexity to defer}}
    
    ## 💡 Example Usage
    ```typescript
    // How the feature will be used
    import { {{newFeature}} } from '{{path}}'
    
    // Actual usage pattern
    const result = await {{newFeature}}({
      // Realistic example
    })
    ```
    
    ## 🔍 Validation Steps
    1. Run `{{specific test command}}`
    2. Check {{specific UI/UX flow}}
    3. Verify {{metric or behavior}}
    4. Confirm {{integration point}}
    
    ## 📚 References
    - Existing pattern: `{{file/path.ts}}:{{line}}`
    - Similar implementation: `{{reference/file.ts}}`
    - Documentation: {{relevant docs}}
</command_template>

<quality_examples>
GOOD - After completing auth with Clerk:
→ /test-coverage "comprehensive auth testing suite including unit tests for hooks/use-auth.ts, integration tests for middleware.ts auth redirects, and E2E tests for login/logout/register flows with Playwright targeting 90% coverage"

BAD - Generic suggestion:
→ /build "add some tests"

GOOD - After scaffolding new project:
→ /build "implement core data models with Prisma schema for User (id, email, name, role, createdAt), Project (id, name, description, ownerId, status enum, visibility), and ProjectMember (projectId, userId, role enum) with proper relations and indexes following the existing database patterns in prisma/schema.prisma"

BAD - Vague direction:
→ /build "create database schema"
</quality_examples>
</next_commands_generation>
```

## output format

```markdown
### 🎯 next command

```bash
/{{command_name}} "{{detailed_command_args}}"
```

**why this next**: {{specific_rationale_with_context}}

<details>
<summary><strong>📋 Full Implementation Spec</strong> (click to expand)</summary>

{{comprehensive_prd_with_examples}}

</details>
```

## implementation checklist

the next command must:
- [ ] be selected from ACTUAL available commands
- [ ] include hyper-specific arguments based on current context
- [ ] reference real files, functions, and patterns from codebase
- [ ] provide 1000+ word PRD with code examples
- [ ] feel inevitable - "of course this is what's next"
- [ ] unblock maximum future progress
- [ ] build naturally on what was just completed
- [ ] include exact implementation details
- [ ] remove ALL ambiguity
- [ ] make the developer excited to run it

## contextual patterns

```yaml
workflow_progressions:
  new_project:
    - /prime → understand existing code
    - /create → scaffold if needed
    - /build → auth system first
    - /build → core data models
    - /build → main user flows
    - /test-coverage → ensure quality
    - /polish-interface → enhance UX
    
  debugging_flow:
    - error occurs → /fix with full logs
    - /test-coverage → prevent regression
    - /docs → document the fix
    
  enhancement_flow:
    - /vision → explore possibilities
    - /simplify-design → find essence
    - /build → implement core
    - /polish-interface → add delight
    
  maintenance_flow:
    - /audit-codebase → find issues
    - /dependency-doctor → update deps
    - /test-coverage → ensure stability
    - /docs → keep docs current
```

remember: developers should see your suggestion and think "YES! That's exactly what I was about to do but even better specified than I could have written it myself."