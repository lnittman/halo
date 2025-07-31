# Claude Code Configuration

This configuration helps Claude Code understand your development environment, standards, and preferences.

## Development Standards

### Primary References
1. **STANDARDS.md** - Located at `~/Developer/STANDARDS.md`
   - Overall architectural guidelines
   - Technology stack specifications
   - Development workflow standards
   - Quality requirements

2. **Rules Directory** - Located at `~/.claude/rules/`
   - Detailed implementation rules
   - Platform-specific requirements
   - Architectural patterns
   - Tool configurations

### Quick Access to Rules
- **General**: product_layout, documentation_and_ai_guidance
- **Turborepo**: tooling, monorepo_structure, state_management, api_and_data_flow
- **AI Service**: ai_service_architecture, ai_agent_instructions
- **Apple**: project_structure, architecture_patterns, ui_ux_patterns, networking_layer

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
Every project consists of:
- `[projectName]-xyz` - Web platform (Turborepo)
- `[projectName]-ai` - AI service (Mastra)
- `[projectName]-apple` - iOS/macOS app (Swift)
- `[projectName]-docs` - Documentation (AI-optimized)

### Technology Stack
- **Web**: Next.js 15+, React 19+, TypeScript, Tailwind CSS v4
- **State**: Jotai (UI), SWR (server state)
- **Auth**: Clerk
- **Database**: PostgreSQL with Prisma
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
- Apps: `~/Developer/apps`
- Docs: `~/Developer/docs`
- Personal: `~/.claude`

### Key Locations
- Standards: `~/Developer/STANDARDS.md`
- Rules: `~/.claude/rules/`
- Commands: `~/.halo/commands/`
- Roles: `~/.halo/roles/`

---

*This configuration ensures Claude Code operates with full awareness of your development ecosystem and standards.*
