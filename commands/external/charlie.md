# external:charlie - orchestrating autonomous TypeScript work via Linear

prime your understanding of how to collaborate with Charlie (CharlieHelps) - an autonomous TypeScript specialist who works through Linear tickets and GitHub PRs. this command teaches you orchestration patterns for effective Charlie collaboration.

<charlie_orchestration_guide>
you are learning how to orchestrate Charlie's work effectively. Charlie is powered by GPT-5 and operates autonomously through Linear and GitHub. after understanding these patterns, you'll apply them flexibly based on context.

<components>
  <use>@file:~/.halo/components/external/xml-structure.md</use>
  <use>@file:~/.halo/components/external/reasoning-patterns.md</use>
  <use>@file:~/.halo/components/external/output-formats.md</use>
</components>

<charlie_capabilities>
## understanding charlie's strengths
- **TypeScript mastery** - deep language, patterns, and ecosystem knowledge
- **autonomous execution** - self-directed from specs to deployed PRs
- **parallel processing** - self-clones for unlimited concurrent work
- **continuous availability** - 24/7 operation, never blocked or tired
- **integration native** - Linear, GitHub, Slack, Sentry, Vercel
- **quality focused** - comprehensive testing, type safety, best practices
</charlie_capabilities>

<collaboration_patterns>
## when to create new linear tickets for charlie

create tickets when:
- Starting new features or significant refactors
- Breaking down epics into manageable chunks
- Addressing bugs from Sentry or user reports
- Planning test coverage improvements
- Initiating dependency updates

ticket characteristics:
- Clean, descriptive titles (no [Charlie] prefix)
- Initially unassigned (you'll tag @charlie when ready)
- Clear project assignment (Core Features, UI/UX Polish, etc.)
- Explicit dependencies noted
- 1-3 days of scoped work

## when to comment on existing tickets

comment when:
- Providing additional context or clarification
- Nudging Charlie on stalled work (@charlie ping)
- Giving feedback on implementation approach
- Requesting changes or iterations
- Updating requirements mid-flight

## how to set charlie up for success

### 1. gather comprehensive context
```bash
# Understand current project state
git status
git log --oneline -10
npm test
npm run typecheck

# Check existing PRs and issues
gh pr list --author CharlieHelps
gh issue list --assignee CharlieHelps

# Review Linear tickets
mcp__linear__list_issues({ 
  filter: { labels: ["charlie"] },
  includeArchived: false 
})
```

### 2. provide rich ticket descriptions
include:
- Current implementation context
- Specific file paths and patterns to follow
- Dependencies and blockers
- Success criteria and testing approach
- Links to related tickets/PRs

### 3. stage the work properly
```typescript
// Check project dependencies
mcp__linear__get_issue({ id: "blocking_ticket_id" })

// Ensure no conflicts
gh pr list --state open --json files

// Verify build health
npm run build
```
</collaboration_patterns>

<verification_workflows>
## monitoring charlie's progress

### real-time progress tracking
```typescript
// Check Linear ticket updates
mcp__linear__list_comments({ issueId: "ticket_id" })

// Monitor PR creation
gh pr list --author CharlieHelps --state open --json number,title,url,createdAt
```

### local verification of charlie's work
```bash
# Fetch Charlie's PR branch
gh pr checkout <pr_number>

# Run comprehensive checks
npm install
npm run build
npm run typecheck
npm test
npm run lint

# Test the changes locally
npm run dev
# Manually verify functionality

# Check test coverage
npm run test:coverage
```

### deployment verification
```bash
# Check Vercel preview
gh pr view <pr_number> --json statusCheckRollup

# Get preview URL
gh pr view <pr_number> --json comments | \
  jq -r '.comments[] | select(.body | contains("vercel")) | .body'
```
</verification_workflows>

<linear_integration>
## effective linear usage with charlie

### creating optimal tickets
```typescript
mcp__linear__create_issue({
  team: "webs",
  title: "Implement user preference persistence", // Clean, no prefix
  description: `
    ## Context
    Users lose their settings on page refresh. We need to persist preferences.
    
    ## Current State
    - Preferences stored in React state only
    - See: src/hooks/usePreferences.ts
    
    ## Requirements
    - Persist to localStorage with fallback
    - Maintain TypeScript type safety
    - Add tests for persistence logic
    
    ## Success Criteria
    - Preferences survive page refresh
    - Graceful handling of corrupted data
    - 100% test coverage on new code
  `,
  project: "Core Features",
  priority: 2,
  labels: ["typescript", "frontend"],
  // Note: NOT assigning to charlie yet
})
```

### triggering charlie
```typescript
// After ticket creation, when ready:
mcp__linear__create_comment({
  issueId: "ticket_id",
  body: "@charlie please implement this. Focus on type safety and include comprehensive tests."
})
```

### providing feedback
```typescript
// Nudge if needed
mcp__linear__create_comment({
  issueId: "ticket_id",
  body: "@charlie any blockers on this? Need any clarification?"
})

// Request changes
mcp__linear__create_comment({
  issueId: "ticket_id",
  body: "@charlie the localStorage implementation needs error boundaries. Please add try-catch and fallback behavior."
})
```
</linear_integration>

<github_verification>
## comprehensive github checks

### pr quality assessment
```bash
# Review PR structure
gh pr view <pr_number> --json additions,deletions,files

# Check commit history
gh pr view <pr_number> --json commits | \
  jq '.commits[] | {message: .commit.message, author: .author.login}'

# Verify CI status
gh pr checks <pr_number>

# Review actual changes
gh pr diff <pr_number>
```

### code review workflow
```bash
# Check out locally for deep review
gh pr checkout <pr_number>

# Run security audit
npm audit

# Check bundle size impact
npm run build -- --analyze

# Verify no console.logs
grep -r "console.log" src/ --exclude-dir=node_modules

# Ensure proper error handling
grep -r "catch" src/ --include="*.ts" --include="*.tsx"
```
</github_verification>

<orchestration_strategies>
## strategic orchestration approaches

### parallel work distribution
when you have multiple independent tasks:
1. Create all Linear tickets upfront
2. Tag @charlie on each when ready
3. Monitor progress across all PRs
4. Merge in dependency order

### iterative refinement
for complex features:
1. Start with core functionality ticket
2. Wait for Charlie's PR
3. Review and test locally
4. Create follow-up tickets for polish
5. Maintain context thread in Linear

### dependency chain management
```typescript
// Map out the chain
const chain = [
  "WEB-123: Database schema migration",
  "WEB-124: API endpoints", 
  "WEB-125: Frontend integration",
  "WEB-126: Test suite"
]

// Create with explicit dependencies
chain.forEach((ticket, i) => {
  // Create ticket with "Depends on: previous"
  // Tag Charlie only when dependency completes
})
```
</orchestration_strategies>

<best_practices>
## orchestration best practices

### context is king
- Always provide file paths and examples
- Link to existing patterns in codebase
- Include recent git commits for context
- Reference related PRs and tickets

### scope appropriately
- 1-3 days per ticket maximum
- Single responsibility per ticket
- Clear definition of done
- Measurable success criteria

### maintain quality gates
- Always require tests
- Enforce TypeScript strict mode
- Check performance impacts
- Verify accessibility

### feedback loops
- Review PR within 24 hours
- Test locally before approving
- Provide specific, actionable feedback
- Use Linear for all communication

### trust but verify
- Charlie is excellent but verify critical paths
- Always test auth/payment flows manually
- Check error scenarios thoroughly
- Validate against requirements
</best_practices>

<communication_templates>
## effective communication patterns

### initial context setting
"@charlie reviewing the codebase for our preferences implementation. Current state is in src/hooks/usePreferences.ts. We need persistence that survives refresh. Follow the pattern in src/hooks/useAuth.ts for localStorage usage."

### mid-flight guidance
"@charlie good progress. The error handling looks solid. Can you add a migration strategy for users with old localStorage format? See how we handle this in src/utils/migrations.ts"

### quality nudges
"@charlie the implementation works but let's improve test coverage. Add edge cases for corrupted data and storage quota exceeded scenarios."

### completion acknowledgment
"@charlie excellent work! The implementation is solid and tests are comprehensive. PR approved and merging."
</communication_templates>

<session_initialization>
## how to start a charlie session

1. **assess current state**
   - Check active Charlie PRs
   - Review open Linear tickets
   - Verify build health

2. **plan the work**
   - Identify tasks suitable for Charlie
   - Map dependencies
   - Estimate scope

3. **prepare context**
   - Document current patterns
   - Gather relevant examples
   - Note any gotchas

4. **create and trigger**
   - Create Linear tickets with rich context
   - Tag @charlie when dependencies clear
   - Monitor and guide as needed

5. **verify and iterate**
   - Test PRs locally
   - Provide feedback via Linear
   - Merge when quality confirmed
</session_initialization>

<when_to_orchestrate>
## recognizing orchestration opportunities

semantic triggers that suggest charlie involvement:
- "implement this feature" → Create ticket, provide spec
- "fix this bug" → Create ticket with repro steps
- "add tests for" → Create ticket with coverage goals
- "refactor to" → Create ticket with target pattern
- "update dependencies" → Create ticket with constraints
- "improve performance" → Create ticket with metrics

semantic triggers for direct github:
- "review this PR" → Use gh CLI, comment findings
- "check Charlie's work" → Checkout branch, test locally
- "why is this failing" → Check CI logs, Linear comments
- "merge when ready" → Verify checks, approve PR
</when_to_orchestrate>

$ARGUMENTS
</charlie_orchestration_guide>