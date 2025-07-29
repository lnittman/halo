# Claude Delegation Patterns

A guide for when Claude should automatically use agents without being explicitly asked.

## Core Principle

Claude should proactively use agents when the user's request clearly matches an agent's specialty. The goal is seamless assistance without making the user learn agent names.

## Automatic Delegation Triggers

### 1. Documentation Needs
**Trigger**: User mentions any technology, library, or documentation URL
**Agent**: `tech-docs`
**Examples**:
- "How do I use Mastra.ai?"
- "What's the API for Tanstack Query?"
- "Get me docs for https://mastra.ai/docs"
- "I need Cloudflare Workers documentation"

### 2. Code Quality Concerns
**Trigger**: User expresses dissatisfaction with code complexity
**Agent**: `simplify-design`
**Examples**:
- "This feels over-engineered"
- "Can we make this simpler?"
- "Too much boilerplate"
- "This component is doing too much"

### 3. Polish Requests
**Trigger**: User wants to improve aesthetics or feel
**Agent**: `polish-interface`
**Examples**:
- "Make it feel more premium"
- "Add some magic to this"
- "It needs more personality"
- "Polish the interactions"

### 4. Technical Deep Dives
**Trigger**: Complex implementation in the standard stack
**Agent**: `stack-expert-dev`
**Examples**:
- "Optimize Next.js performance"
- "Implement Cloudflare Workers"
- "Add real-time sync to iOS"
- "Debug this React 19 issue"

### 5. Quality Audits
**Trigger**: User wants comprehensive code review
**Agent**: `audit-codebase`
**Examples**:
- "Review this for best practices"
- "Find potential issues"
- "Is this production ready?"
- "Check for code smells"

### 6. Git/GitHub Operations
**Trigger**: Any git-related task or repository management
**Agent**: `github-whisperer`
**Examples**:
- "Commit these changes"
- "Create a PR for this feature"
- "What files have changed?"
- "Clean up my working directory"

### 7. Test Coverage
**Trigger**: Testing needs or coverage concerns
**Agent**: `test-coverage`
**Examples**:
- "Write tests for this component"
- "Check test coverage"
- "Fix failing tests"
- "Add e2e tests"

### 8. Cloudflare Services
**Trigger**: Cloudflare deployment or edge computing
**Agent**: `cloudflare-whisperer`
**Examples**:
- "Deploy to Cloudflare Workers"
- "Set up D1 database"
- "Configure R2 storage"
- "Optimize edge performance"

### 9. Dependency Management
**Trigger**: Package updates or dependency issues
**Agent**: `dependency-doctor`
**Examples**:
- "Update all packages"
- "Fix dependency conflicts"
- "Audit for vulnerabilities"
- "Reduce bundle size"

### 10. Linear Integration
**Trigger**: Project tracking or Linear sync
**Agent**: `linear-whisperer`
**Examples**:
- "Sync with Linear"
- "Update issue status"
- "Create issues from TODOs"
- "Check project progress"

## Multi-Agent Patterns

### Pattern 1: Code → Test
After implementing features:
1. Claude builds in main thread
2. `test-coverage` writes tests

### Pattern 2: Audit → Test → Commit
Before committing:
1. `audit-codebase` identifies issues
2. `test-coverage` ensures coverage
3. `github-whisperer` commits changes

### Pattern 3: Research → Document
When learning new tech:
1. `tech-docs` aggregates documentation
2. Claude implements based on docs

## Delegation Decision Tree

```
User Request
├─ Needs documentation?
│  └─ YES → tech-docs
├─ Git/GitHub task?
│  └─ YES → github-whisperer
├─ Cloudflare deployment?
│  └─ YES → cloudflare-whisperer
├─ Testing needed?
│  └─ YES → test-coverage
├─ Dependency issues?
│  └─ YES → dependency-doctor
├─ Linear sync?
│  └─ YES → linear-whisperer
├─ Code quality review?
│  └─ YES → audit-codebase
├─ Too complex?
│  └─ YES → simplify-design
├─ Needs polish?
│  └─ YES → polish-interface
└─ Building features?
   └─ YES → Handle in main thread
```

## When NOT to Delegate

### Keep in Main Context
- Simple questions
- Direct file edits
- Basic explanations
- Quick fixes
- General discussion

### Ask Before Delegating
- Ambiguous requests
- Personal preference matters
- Multiple valid approaches
- User seems unsure

## Communication Patterns

### Seamless Delegation
```
User: "I love how Linear does command palettes"
Claude: I'll analyze Linear's command palette design and show you how to recreate it.
[Uses recreate-design agent]
```

### Explicit Delegation
```
User: "This codebase needs help"
Claude: I'll use our audit specialist to comprehensively review your codebase for issues and improvements.
[Uses audit-codebase agent]
```

### Multi-Agent Coordination
```
User: "Build me a todo app like Things 3"
Claude: I'll analyze Things 3's design patterns and build you a beautiful todo app inspired by it.
[Claude handles directly, may use polish-interface for final touches]
```

## Implementation in CLAUDE.md

Add to main CLAUDE.md configuration:

```markdown
## Agent Delegation

Use specialized agents automatically when user requests match their expertise:
- Documentation needs → tech-docs
- Git/GitHub operations → github-whisperer
- Cloudflare deployment → cloudflare-whisperer
- Test writing/coverage → test-coverage
- Dependency management → dependency-doctor
- Linear sync/tracking → linear-whisperer
- Code quality review → audit-codebase
- Design simplification → simplify-design
- UI polish → polish-interface
- Technical depth → stack-expert-dev

For building features, handle directly in main thread rather than delegating.
```

## Evolution

This pattern list should grow as:
1. New agents are added
2. User patterns emerge
3. Delegation success is measured
4. Edge cases are discovered

The goal is invisible intelligence—users get expert help without thinking about delegation.