# Claude Delegation Patterns

A guide for when Claude should automatically use agents without being explicitly asked.

## Core Principle

Claude should proactively use agents when the user's request clearly matches an agent's specialty. The goal is seamless assistance without making the user learn agent names.

## Automatic Delegation Triggers

### 1. Design References
**Trigger**: User mentions any website, app, or UI they want to recreate
**Agent**: `recreate-design`
**Examples**:
- "I want a sidebar like Linear's"
- "Make it look like stripe.com"
- "Build me something like Notion"
- "Check out this cool UI: [URL]"

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

### 6. Product Ideation
**Trigger**: User wants to explore possibilities
**Agent**: `envision-product`
**Examples**:
- "What AI features could we add?"
- "How could this be better?"
- "I need innovative ideas"
- "Transform this experience"

### 7. Rapid Prototyping
**Trigger**: User wants something built quickly with taste
**Agent**: `build-anything`
**Examples**:
- "Build me a quick prototype"
- "I need a demo fast"
- "Create a proof of concept"
- "Make something beautiful"

## Multi-Agent Patterns

### Pattern 1: Reference → Build
When user says "build X like Y":
1. `recreate-design` analyzes Y
2. `build-anything` implements X

### Pattern 2: Build → Polish
When creating new features:
1. `build-anything` creates base
2. `polish-interface` adds refinement

### Pattern 3: Audit → Simplify
When improving existing code:
1. `audit-codebase` identifies issues
2. `simplify-design` refactors

## Delegation Decision Tree

```
User Request
├─ Contains URL/design reference?
│  └─ YES → recreate-design
├─ About code complexity?
│  └─ YES → simplify-design
├─ About polish/feel?
│  └─ YES → polish-interface
├─ Deep technical (Next.js/Swift/etc)?
│  └─ YES → stack-expert-dev
├─ Comprehensive review?
│  └─ YES → audit-codebase
├─ Product ideas/vision?
│  └─ YES → envision-product
├─ Quick prototype?
│  └─ YES → build-anything
└─ Multiple aspects?
   └─ YES → orchestrate-work
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
Claude: I'll first analyze Things 3's design patterns, then build you a beautiful todo app inspired by it.
[Uses recreate-design then build-anything]
```

## Implementation in CLAUDE.md

Add to main CLAUDE.md configuration:

```markdown
## Agent Delegation

Use specialized agents automatically when user requests match their expertise:
- Design references → recreate-design
- Simplification → simplify-design  
- Polish → polish-interface
- Technical depth → stack-expert-dev
- Code review → audit-codebase
- Product vision → envision-product
- Quick builds → build-anything

For complex requests spanning multiple domains, use orchestrate-work.
```

## Evolution

This pattern list should grow as:
1. New agents are added
2. User patterns emerge
3. Delegation success is measured
4. Edge cases are discovered

The goal is invisible intelligence—users get expert help without thinking about delegation.