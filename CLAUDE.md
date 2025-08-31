

<!-- Source: .ruler/01-halo-overview.md -->

# Halo Universal Prompt Framework

## Overview
Halo is a universal prompt framework that works across all AI CLI tools (Claude Code, Codex, Gemini, Cursor, etc.). It provides consistent commands, patterns, and delegation logic for seamless multi-agent collaboration.

## Core Philosophy
- **Universal** - Works in any AI CLI tool
- **Bidirectional** - Tools can delegate to each other
- **Consistent** - Same commands across all tools
- **Modular** - Components are reusable
- **Practical** - Focused on daily productivity

## Directory Structure
```
~/.halo/
├── commands/       # Executable commands
│   ├── core/      # Essential daily commands
│   ├── external/  # Delegation to other tools
│   ├── creative/  # Fun sandbox commands
│   ├── integrations/ # Service integrations
│   └── roles/     # Persona-based perspectives
├── components/    # Reusable patterns
└── .ruler/       # Configuration source
```

## Command Categories

### Core Commands
- `/prime` - Initialize project context
- `/build` - Implement features
- `/create` - Create new projects
- `/fix` - Fix bugs and errors
- `/test` - Write and run tests
- `/docs` - Generate documentation
- `/diagram` - Visual architecture
- `/web` - Web research and scraping

### External Orchestration
- `/external:claude` - Use Claude Code's MCP tools
- `/external:codex` - Use GPT-5 deep reasoning
- `/external:gemini` - Use 2M context analysis
- `/external:cursor` - Use implementation engine

### Integrations
- `/github` - GitHub operations
- `/linear` - Linear project management
- `/cloudflare` - Cloudflare deployment
- `/convex` - Convex backend operations

### Creative Sandbox
- `/3d` - 3D graphics and WebGL
- `/video` - Video creation with Remotion
- `/motion` - Motion graphics
- `/unreal/*` - Unreal Engine commands

### Personas
- `/jony` - Jony Ive's design thinking
- `/dieter` - Dieter Rams' principles
- `/bret` - Bret Victor's vision
- `/rick` - Rick Rubin's creativity
- `/tadao` - Tadao Ando's architecture
- `/kenya` - Kenya Hara's emptiness
- `/issey` - Issey Miyake's innovation
- `/teenage` - Teenage Engineering's playfulness



<!-- Source: .ruler/02-delegation-patterns.md -->

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



<!-- Source: .ruler/03-components.md -->

# Reusable Components

## Component System
Components are reusable patterns that commands can integrate. They ensure consistency across all commands and tools.

## Available Components

### thinking-blocks.md
Structured reasoning display for transparency:
- Understanding phase
- Analysis phase  
- Planning phase
- Execution phase

Usage: Shows AI reasoning process to build trust

### verification-patterns.md
Safety checks before dangerous operations:
- Impact assessment
- User confirmation
- Rollback planning
- Risk evaluation

Usage: Prevents accidental damage

### output-standards.md
Consistent formatting across all outputs:
- Markdown structure
- Emoji usage patterns
- Progress indicators
- Success/error formatting

Usage: Professional, readable outputs

### repomix-context.md
Smart context gathering with token management:
- Progressive refinement
- Token counting
- File filtering
- Project detection

Usage: Comprehensive codebase understanding

### next-command.md
Intelligent command suggestion:
- Analyzes current state
- Suggests logical next step
- Provides complete command
- Includes rationale

Usage: Guides users through workflows

### parallel-tasks.md
Concurrent execution patterns:
- Task batching
- Resource management
- Progress tracking
- Error handling

Usage: Efficient multi-task execution

### planning-phases.md
Structured planning approach:
- Requirement gathering
- Solution design
- Implementation planning
- Risk assessment

Usage: Complex task planning

### diagram-patterns.md
Visual representation patterns:
- ASCII diagrams
- Mermaid syntax
- Architecture visualization
- Flow charts

Usage: Visual communication

### interop-patterns.md
Command integration patterns:
- Command chaining
- State passing
- Context preservation
- Error propagation

Usage: Multi-command workflows

### xml-transformer.md
Input transformation to structured format:
- Natural language parsing
- Parameter extraction
- Intent detection
- Validation

Usage: Robust input handling

## Component Integration

### In Commands
```xml
<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>
```

### Component Principles
1. **Single Responsibility** - Each component does one thing well
2. **Composable** - Components work together seamlessly
3. **Reusable** - Used across multiple commands
4. **Consistent** - Same behavior everywhere
5. **Documented** - Clear usage instructions



<!-- Source: .ruler/04-coding-standards.md -->

# Coding Standards and Patterns

## Universal Principles
These standards apply regardless of which AI CLI tool you're using.

## Project Structure

### Modern Turborepo Pattern
```
[project]-xyz/
├── apps/
│   ├── app/        # Next.js client
│   ├── api/        # Hono API on Cloudflare
│   ├── ai/         # Mastra AI service
│   └── docs/       # Mintlify documentation
├── packages/
│   ├── database/   # Drizzle ORM
│   ├── design/     # Design system
│   ├── auth/       # Clerk authentication
│   └── services/   # Business logic
└── docs/          # Internal AI docs
```

## Technology Stack

### Frontend
- **Framework**: Next.js 15+, React 19+
- **Styling**: Tailwind CSS v4
- **State**: Jotai (UI), SWR (server state)
- **Components**: Radix UI, shadcn/ui

### Backend
- **API**: Hono on Cloudflare Workers
- **Database**: PostgreSQL with Drizzle
- **Auth**: Clerk
- **AI**: Mastra framework

### Infrastructure
- **Hosting**: Vercel (frontend), Cloudflare (API)
- **Analytics**: PostHog
- **Monitoring**: Sentry
- **Storage**: Cloudflare R2

## Code Quality Standards

### Before Any Commit
- [ ] TypeScript compiles without errors
- [ ] Biome/ESLint passes
- [ ] Tests pass
- [ ] No console.log statements
- [ ] Error boundaries implemented
- [ ] Loading states handled
- [ ] Mobile responsive
- [ ] Accessibility checked

### Documentation Requirements
- Every directory has CLAUDE.md
- All exports have TSDoc/JSDoc
- Component usage examples
- API endpoint documentation
- Environment variables documented

## AI-Specific Patterns

### Mastra AI Service
```typescript
// Agent definition
export const agent = new Agent({
  name: 'assistant',
  model: 'gpt-4',
  tools: [...],
  systemPrompt: '...'
})

// Workflow orchestration
export const workflow = new Workflow({
  steps: [...],
  errorHandling: {...}
})
```

### Error Handling
```typescript
// Always use error boundaries
export function ErrorBoundary({ error, reset }) {
  return <ErrorFallback error={error} reset={reset} />
}

// Consistent error types
export class AppError extends Error {
  constructor(message: string, public code: string) {
    super(message)
  }
}
```

### State Management
```typescript
// Jotai for UI state
export const userAtom = atom<User | null>(null)

// SWR for server state
export function useUser() {
  return useSWR('/api/user', fetcher)
}
```

## Security Best Practices
- Never commit secrets or API keys
- Use environment variables
- Validate all inputs
- Sanitize user content
- Implement rate limiting
- Use HTTPS everywhere
- Follow OWASP guidelines

## Performance Standards
- Lighthouse score > 90
- First Contentful Paint < 1s
- Time to Interactive < 3s
- Bundle size budgets enforced
- Images optimized and lazy loaded
- Code splitting implemented
- Caching strategies defined

## Testing Requirements
- Unit tests for utilities
- Integration tests for APIs
- Component tests with React Testing Library
- E2E tests for critical paths
- Minimum 80% coverage
- Tests run in CI/CD
