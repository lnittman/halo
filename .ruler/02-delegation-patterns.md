# External Tool Delegation Patterns

## Automatic Delegation Logic

### Claude Code (MCP Power)
**When to delegate to Claude:**
- Tasks requiring MCP tools (firecrawl, context7, convex, vercel, playwright)
- Project initialization with comprehensive understanding
- Complex implementation with established patterns
- Documentation generation with context
- Web research and data extraction

**Keywords that trigger delegation:**
- "use claude"
- "mcp tools"
- "web research"
- "scrape"
- "project context"

**Example delegation:**
```bash
# From any tool
"use claude to scrape competitor websites and analyze features"
→ /external:claude
```

### Codex (GPT-5 Deep Reasoning)
**When to delegate to Codex:**
- Strategic planning and architecture design
- Complex debugging and root cause analysis
- Technical research and evaluation
- Performance optimization strategies
- System design decisions

**Keywords that trigger delegation:**
- "think deeply"
- "complex reasoning"
- "architecture"
- "root cause"
- "strategic"

**Example delegation:**
```bash
# From any tool
"think deeply about the architecture for this real-time system"
→ /external:codex
```

### Gemini (2M Context Window)
**When to delegate to Gemini:**
- Full codebase audits and analysis
- Pattern extraction across many files
- Security vulnerability scanning
- Comprehensive code reviews
- Large-scale refactoring planning

**Keywords that trigger delegation:**
- "entire codebase"
- "audit"
- "analyze all"
- "use repomix"
- "comprehensive"

**Example delegation:**
```bash
# From any tool
"audit the entire codebase for security vulnerabilities"
→ /external:gemini
```

### Cursor (Implementation Engine)
**When to delegate to Cursor:**
- Feature implementation from specs
- Bug fixes with immediate execution
- Code scaffolding and boilerplate
- Refactoring with auto-edit
- Test generation

**Keywords that trigger delegation:**
- "implement"
- "build feature"
- "fix bug"
- "scaffold"
- "refactor"

**Example delegation:**
```bash
# From any tool
"implement the authentication flow based on the spec"
→ /external:cursor
```

## Bidirectional Orchestration

### Chain Patterns
```bash
# Analysis → Planning → Implementation
gemini "analyze codebase" → 
codex "plan refactoring" → 
cursor "implement changes"

# Research → Design → Build
claude "/web research" →
codex "design architecture" →
cursor "build components"

# Debug → Fix → Test
codex "debug issue" →
cursor "fix bug" →
claude "/test generate tests"
```

### Parallel Patterns
```bash
# Multiple tools for different aspects
claude "/web research competitors" &
gemini "analyze our codebase" &
codex "plan differentiation strategy"
```

## Smart Model Selection

### Automatic Model Routing
Each tool should intelligently select models:

**Codex:**
- Always GPT-5 for deep reasoning
- Prefix with "Think deeply and reason step-by-step"

**Cursor:**
- Sonnet 4 for large context (>100k tokens)
- GPT-5 for complex logic
- Never Opus

**Gemini:**
- Always use with repomix for full context
- Optimize token usage progressively

**Claude:**
- Leverage all available MCP tools
- Use appropriate halo commands