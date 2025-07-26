# Rule: Version Guidelines

Guidelines for dependency versions across all project types.

## 1. Core Framework Versions

### Turborepo Projects
- **Next.js**: 15.0.0 or higher (App Router required)
- **React**: 19.0.0 or higher (RSC support required)
- **TypeScript**: 5.0.0 or higher (strict mode required)
- **Tailwind CSS**: 3.x stable (v4 when officially released)
- **Node.js**: 20.9.0 or higher

### AI Services
- **Node.js**: 20.9.0 or higher
- **TypeScript**: 5.0.0 or higher
- **Mastra**: Latest stable version

### Apple Projects
- **Swift**: 5.9 or higher
- **iOS Deployment Target**: 17.0 or higher
- **macOS Deployment Target**: 14.0 or higher
- **Xcode**: Latest stable version

## 2. Update Strategy

### Regular Updates (Monthly)
- Patch versions of all dependencies
- Minor versions after testing in one project
- Security updates immediately

### Major Updates
- Coordinate across all projects in ecosystem
- Test in development project first
- Update create command templates after validation
- Document breaking changes in STANDARDS.md

### Dependency Pinning
- Exact versions for critical infrastructure (Next.js, React)
- Range versions for utilities and dev dependencies
- Lock files committed to repository

## 3. Version Alignment

### Within Monorepo
- All packages in a monorepo must use the same version of:
  - React and React DOM
  - TypeScript
  - Next.js (if multiple apps)
  - Shared internal packages

### Across Ecosystem
- Projects should align on major versions of:
  - Authentication providers (Clerk)
  - Database clients (Prisma)
  - UI libraries (shadcn/ui)
  - Monitoring tools (Sentry, PostHog)

## 4. Breaking Change Management

### Pre-update Checklist
1. Review changelog for breaking changes
2. Check compatibility with other dependencies
3. Test in isolated branch
4. Update types and interfaces
5. Run full test suite

### Post-update Verification
1. Build all projects in monorepo
2. Test critical user flows
3. Verify production build optimization
4. Check bundle size impact
5. Monitor error rates after deployment

## 5. Tool-Specific Guidelines

### pnpm
- Use workspace protocol for internal packages: `workspace:*`
- Deduplicate dependencies regularly: `pnpm dedupe`
- Clean install after major updates: `pnpm clean && pnpm install`

### Turbo
- Keep turbo.json synchronized with actual scripts
- Update Turborepo CLI quarterly
- Use remote caching for CI/CD

### Biome/Ultracite
- Update formatter/linter rules cautiously
- Run format after updates to catch changes
- Document any rule customizations