# next commands component

provides THE single best contextually-aware next command with comprehensive spec.

## usage

```xml
<use>@next-commands</use>
```

## implementation

```xml
<next_command_generation>
analyze the current context and determine THE SINGLE BEST next command.
the command should:
1. be the most logical and valuable next step
2. include full command with detailed, specific arguments
3. have a comprehensive PRD/spec that removes all ambiguity

<command_analysis>
determine the single most valuable next action by analyzing:
- what was just completed
- current project state
- detected gaps or issues
- logical workflow progression
- highest impact opportunity

the command should:
- solve the most pressing need
- provide maximum value
- be immediately actionable
- move the project forward significantly
- feel like the obvious next step
</command_analysis>

<command_template>
structure the single best command as:

best_next_command:
  name: the command name (build, vision, create, etc)
  args: highly specific arguments based on current context
  rationale: why this is THE best next step right now
  prd: |
    # comprehensive specification
    
    ## objective
    clear goal statement based on current context
    
    ## context
    - current state: what exists now
    - gap: what's missing or needed
    - value: why this matters
    
    ## requirements
    ### functional
    - specific features/capabilities needed
    - based on detected patterns and stack
    - aligned with existing architecture
    
    ### technical 
    - frameworks/tools to use (from detected stack)
    - patterns to follow (from codebase analysis)
    - constraints to respect
    
    ### quality
    - performance targets
    - testing requirements
    - documentation needs
    
    ## implementation approach
    1. specific first step
    2. core implementation 
    3. integration points
    4. testing strategy
    5. deployment considerations
    
    ## success criteria
    - measurable outcomes
    - user-facing improvements
    - technical achievements
    
    ## example usage
    ```
    specific code examples or workflows
    ```
</command_template>

<contextual_examples>
after /prime on a new Next.js project with no auth:
→ /build "implement complete authentication system with Clerk including user profiles, protected routes, and role-based access control"
   - because auth is foundational and blocks other features

after /build completing authentication:
→ /build "create comprehensive test suite for authentication flows including unit tests, integration tests, and e2e tests with Playwright"
   - because testing auth is critical before moving forward

after /create scaffolding a new turborepo:
→ /build "implement shared UI component library in packages/ui with Button, Card, Input, and Modal components following the design system"
   - because shared components enable consistent development

after major refactoring:
→ /docs "generate comprehensive documentation for the new architecture including diagrams, API references, and migration guide"
   - because documentation prevents knowledge loss

after performance issues discovered:
→ /build "optimize application performance: implement code splitting, lazy loading, image optimization, and caching strategies to achieve <3s load time"
   - because performance directly impacts users
</contextual_examples>
</next_commands_generation>
```

## output format

```markdown
### 🦌 next command

```bash
/{{command_name}} {{command_args}}
```

**why this**: {{command_rationale}}

<details>
<summary>📋 comprehensive spec (click to expand)</summary>

{{command_prd}}

</details>
```

## integration notes

- analyze command history if available
- detect project type and stack
- understand current workflow phase
- suggest logical progressions
- ensure specs are actionable
- make args specific and contextual
- include enough detail to execute without questions

## quality checklist

the single command must:
- [ ] be THE most logical next step
- [ ] include highly specific, contextual arguments
- [ ] have comprehensive PRD (750+ words minimum)
- [ ] remove all ambiguity about implementation
- [ ] follow detected patterns and conventions
- [ ] respect existing architecture
- [ ] be immediately actionable without questions
- [ ] provide maximum value for effort
- [ ] feel inevitable - "of course this is next"

remember: this single suggestion shapes the entire development flow. make it perfect. users should think "yes, that's exactly what i need to do next" when they see it.