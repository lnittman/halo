# next command component

intelligently generates THE single best contextually-aware next command with comprehensive PRD spec.

## usage

```xml
<generate_next_command>
  <use>@next-command</use>
</generate_next_command>
```

## implementation

```xml
<next_command_algorithm>
<!-- CRITICAL: always output exactly ONE command with rich PRD -->

<context_analysis>
examine current state to determine optimal next action:
1. what was just completed?
2. what gaps or issues exist?
3. what would provide maximum value?
4. what follows logically in the workflow?
5. what would the user want to do next?

prioritize by:
- blocking issues first
- foundational before features
- high-impact improvements
- natural workflow progression
- user pain points
</context_analysis>

<command_selection>
based on context, select THE command that:
- addresses the most pressing need
- provides maximum immediate value
- follows naturally from current state
- moves the project forward significantly
- feels inevitable and obvious

common progressions:
- /prime → /build (implement core feature)
- /create → /build (add first component)
- /build → /test-coverage (ensure quality)
- /build → /docs (document changes)
- major feature → /audit-codebase (verify quality)
- complexity added → /simplify-design (refine)
- ui complete → /polish-interface (perfect)
- all done → /vision (what's next?)
</command_selection>

<prd_generation>
create a focused PRD (400 words) that:

1. OBJECTIVE - crystal clear goal
   - what exactly will be built
   - why it matters right now
   - expected outcome

2. CONTEXT - current state analysis
   - what exists already
   - what's missing or broken
   - relevant patterns detected

3. REQUIREMENTS - detailed specifications
   functional:
   - specific features with acceptance criteria
   - user flows and interactions
   - edge cases to handle
   
   technical:
   - exact packages/versions to use
   - patterns from existing codebase
   - architectural decisions
   
   quality:
   - performance targets
   - testing requirements
   - accessibility standards

4. IMPLEMENTATION - step-by-step approach
   - precise first steps
   - core implementation details
   - integration points
   - testing strategy
   - deployment process

5. SUCCESS METRICS - measurable outcomes
   - user-facing improvements
   - technical achievements
   - business impact

6. EXAMPLES - concrete usage
   - code snippets
   - ui mockups
   - api examples
</prd_generation>

<quality_checks>
ensure the command:
✓ addresses most pressing current need
✓ includes specific, contextual arguments
✓ has comprehensive PRD (not generic)
✓ removes all implementation ambiguity
✓ follows detected patterns exactly
✓ respects existing architecture
✓ is immediately actionable
✓ provides clear value
✓ feels like the obvious next step
</quality_checks>
</next_command_algorithm>
```

## output format

```markdown
### 🎯 next command

```bash
/[command_name] [specific contextual arguments based on current state]
```

**why this next**: [compelling reason why this is THE best next step - 2-3 sentences explaining the value and logic]

<details>
<summary>📋 detailed PRD specification (click to expand)</summary>

# [Feature/Task Name] Specification

## 🎯 Objective

[Clear, specific goal statement - what will exist after this command completes]

## 📊 Context

**Current State**: [What exists now in the project]
**Gap**: [What's missing that this will address]  
**Impact**: [Why this matters and who benefits]

## 📐 Requirements

### Functional Requirements
1. **[Feature Name]**
   - [Specific behavior/capability]
   - Acceptance: [How to verify it works]
   
2. **[Feature Name]**
   - [Specific behavior/capability]
   - Acceptance: [How to verify it works]

### Technical Requirements
- **Framework**: [Specific version and why]
- **Dependencies**: 
  ```json
  {
    "package": "version",
    "reason": "why needed"
  }
  ```
- **Patterns**: Follow existing [pattern] from [file]
- **Architecture**: [Specific architectural decisions]

### Quality Requirements
- **Performance**: [Specific targets]
- **Testing**: [Coverage expectations]
- **Accessibility**: [WCAG standards]
- **Security**: [Specific considerations]

## 🏗️ Implementation Approach

### Phase 1: Setup (30 min)
1. [Specific first step with command/code]
2. [Next step with details]

### Phase 2: Core Implementation (2-3 hrs)
1. [Main implementation task]
   ```typescript
   // example code structure
   ```
2. [Integration task]

### Phase 3: Testing & Polish (1 hr)
1. [Testing approach]
2. [Edge cases to verify]

### Phase 4: Documentation (30 min)
1. [What to document]
2. [Where to document]

## 📊 Success Criteria

### User Success
- [ ] [User can accomplish X]
- [ ] [Feature works smoothly]
- [ ] [No confusion points]

### Technical Success
- [ ] [Tests pass]
- [ ] [Performance met]
- [ ] [Code quality standards]

### Business Success
- [ ] [Metric improved]
- [ ] [Goal achieved]

## 💡 Example Usage

```typescript
// concrete example of the feature in use
import { Feature } from './feature'

const result = await Feature.use({
  // realistic example
})
```

## 🚀 Future Considerations

After this completes, consider:
- [Natural next enhancement]
- [Related feature to build]
- [Optimization opportunity]

</details>
```

## contextual intelligence

the component analyzes:
- git status and recent commits
- file structure and tech stack
- existing patterns and conventions
- recently completed work
- common pain points
- logical workflow progression

## example outputs

after `/prime` on fresh Next.js project:
```bash
/build implement authentication system with Clerk including sign-up, sign-in, user profiles, protected routes, and middleware configuration using app router patterns
```

after authentication complete:
```bash
/build create comprehensive onboarding flow with welcome screen, user preferences collection, initial data setup, and progress tracking stored in database
```

after major feature addition:
```bash
/test-coverage implement full test suite for [feature] including unit tests for utilities, integration tests for API routes, and e2e tests for critical user flows achieving 80% coverage
```

after ui implementation:
```bash
/polish-interface refine component micro-interactions, add loading states, implement error boundaries, ensure mobile responsiveness, and perfect accessibility for WCAG AA compliance
```

## integration guidelines

- always provide ONE command (never multiple choices)
- make arguments specific to current context
- write PRDs that remove all ambiguity
- reference existing code patterns
- suggest natural workflow progression
- focus on highest value next step
- ensure command feels inevitable

## quality assurance

every suggested command must:
1. solve a real current need
2. include rich contextual detail
3. have focused PRD (400 words)
4. follow existing patterns exactly
5. be immediately actionable
6. provide clear value
7. advance the project meaningfully
8. feel like the obvious choice
9. require no clarification

remember: this component shapes development flow. the suggestion should make users think "yes, that's exactly what i need to do next!" every single time.