# Rule: Product Layout

## 1. Monorepo Structure
A product is organized as a single Turborepo monorepo with platform-specific apps. The standard layout is:

-   `[product-name]-xyz/`: The main monorepo containing all web, AI, and documentation
-   `[product-name]-apple/`: The native Apple platform project (separate repository)

## 2. Web Monorepo (`-xyz`) Structure
The web monorepo must contain two primary directories: `apps` and `packages`.

-   `apps/`: Contains deployable applications.
    -   `app/`: The main Next.js user-facing application.
    -   `ai/`: The AI service application (Mastra-based).
    -   `api/`: Optional, for services like webhooks or cron jobs.
-   `packages/`: Contains shared code and libraries.
    -   `api/`: Shared business logic, domain services, and Zod schemas.
    -   `auth/`: Authentication logic, primarily as a wrapper for Clerk.
    -   `database/`: Drizzle ORM schemas, client, and migrations.
    -   `design/`: The shared UI component library, hooks, and constants.
    -   `ai/`: The generalized AI client SDK for the web application.
    -   `typescript-config/`: Shared `tsconfig.json` files.

## 3. AI Service (`apps/ai`) Structure
The AI service is an application within the monorepo dedicated to all AI logic.

-   `src/`: The root for the AI service.
    -   `mastra/`: All Mastra AI definitions.
        -   `agents/`: Contains definitions for each AI agent (Mastra runtime; not halo prompts).
        -   `tools/`: Contains tool definitions.
        -   `workflows/`: Multi-step AI processes.
    -   `lib/`: Shared utilities and helpers.
    -   `routes/`: API endpoints for the AI service.

## 4. Documentation (`docs/`) Structure
Documentation lives within the monorepo at the root level:

-   `docs/`: Comprehensive documentation
    -   `architecture/`: System design and architecture
    -   `api/`: API documentation
    -   `guides/`: User and developer guides
    -   `ai/`: AI agent documentation and CLAUDE.md files