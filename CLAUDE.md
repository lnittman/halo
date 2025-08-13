# Claude Code Configuration

This configuration helps Claude Code understand your development environment, standards, and preferences.

## Development Standards

### Primary References
1. **Halo System** - Located at `~/.halo/`
   - Commands, rules, components, and roles
   - All development standards and patterns
   - Self-contained system (no external dependencies)

2. **Rules Directory** - Located at `~/.halo/rules/`
   - `general/`: product_layout.md, documentation_and_ai_guidance.md, version_guidelines.md
   - `turborepo/`: tooling.md, monorepo_structure.md, state_management.md, api_and_data_flow.md, ui_patterns.md
   - `mastra/`: ai_service_architecture.md, ai_agent_instructions.md
   - `apple/`: project_structure.md, architecture_patterns.md, ui_ux_patterns.md, networking_layer.md

### Architecture Notes
- Documentation lives in turborepo: `apps/docs/` (user-facing Mintlify) and `./docs/` (internal AI guidance)
- No separate `-ai` or `-docs` repos - everything in the turborepo
- Standards documentation: `~/Developer/docs/content/architecture/standards.mdx`

## Command System

### Available Commands
- `/prime` - Initialize session context
- `/create` - Create new project ecosystem
- `/build` - Implement features
- `/vision` - Explore creative possibilities
- `/design` - Design system development
- `/brand` - Production readiness
- `/docs` - Documentation audit
- `/diagram` - Visual architecture
- `/ecosystem` - Meta-level ecosystem management

### Command Integration
All commands:
1. Accept universal inputs (URLs, code, files, images)
2. Follow standardized output formats
3. Suggest logical next commands
4. Enforce architectural rules

## Project Patterns

### Repository Structure
Modern turborepo structure:
- `[projectName]-xyz/` - Main turborepo containing:
  - **Apps:**
    - `apps/app/` - Client-facing Next.js web application
    - `apps/api/` - Hono API on Cloudflare Workers
    - `apps/ai/` - Mastra AI service
    - `apps/docs/` - User-facing Mintlify documentation (optional)
    - `apps/email/` - Resend dev preview server (optional)
    - `apps/daemon/` - Background services (optional)
    - `apps/ws/` - WebSocket server (optional)
  - **Packages:**
    - `packages/ai/` - AI utilities and agents
    - `packages/auth/` - Authentication logic (Clerk)
    - `packages/database/` - Drizzle schema and client
    - `packages/design/` - Design system components
    - `packages/orpc/` - tRPC/oRPC shared types
    - `packages/storage/` - File storage abstractions
    - `packages/analytics/` - PostHog integration
    - `packages/email/` - Email templates
    - `packages/services/` - Business logic
    - `packages/typescript-config/` - Shared TS configs
  - `docs/` - Internal AI-optimized development docs
- `[projectName]-apple/` - Native iOS/macOS app (Swift)

### Technology Stack
- **Web**: Next.js 15+, React 19+, TypeScript, Tailwind CSS v4
- **State**: Jotai (UI), SWR (server state)
- **Auth**: Clerk
- **Database**: PostgreSQL with Drizzle ORM
- **AI**: Mastra framework
- **Analytics**: PostHog
- **Monitoring**: Sentry

### Development Workflow
1. Always run `/prime` at session start
2. Use `/ecosystem audit` to check standards
3. Create projects with `/create` (zero config)
4. Implement with `/build`
5. Document continuously

## AI Development Principles

### Documentation First
- Every major directory needs CLAUDE.md
- All exports need TSDoc/JSDoc
- Agent instructions in XML format
- Machine-readable indexes for navigation

### Pattern Recognition
- Learn from existing projects
- Apply consistent patterns
- Enforce standards automatically
- Extract wisdom from collective work

### Extended Thinking
- Use extended thinking for complex tasks
- Show reasoning transparently
- Consider alternatives
- Include potential issues

## Quality Standards

### Before Committing
- [ ] TypeScript compiles without errors
- [ ] Biome formatting applied
- [ ] No console.log statements
- [ ] Error boundaries implemented
- [ ] Loading states handled
- [ ] Mobile responsive
- [ ] Accessibility checked
- [ ] Documentation updated

## Slash Command System

Use specialized slash commands when user requests match their expertise:
- Documentation needs → `/tech-docs`
- Git/GitHub operations → `/github-whisperer`  
- Cloudflare deployment → `/cloudflare-whisperer`
- Test writing/coverage → `/test-coverage`
- Dependency management → `/dependency-doctor`
- Linear sync/tracking → `/linear-whisperer`
- Code quality review → `/audit-codebase`
- Design simplification → `/simplify-design`
- UI polish → `/polish-interface`
- Technical depth → `/stack-expert-dev`

For building features, handle directly in main thread rather than delegating.

## Environment Specifics

### Working Directories
- Primary: `~/Developer`
- Personal: `~/.claude`

### Key Locations
- Halo System: `~/.halo/`
- Rules: `~/.halo/rules/`
- Commands: `~/.halo/commands/`
- Components: `~/.halo/components/`
- Roles: `~/.halo/roles/`
- Developer Docs: `~/Developer/docs/` (Mintlify app)

---

*This configuration ensures Claude Code operates with full awareness of your development ecosystem and standards.*
