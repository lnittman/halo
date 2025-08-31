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