# Rule: Turborepo Monorepo Structure

All `*-xyz` monorepos must follow a standardized package structure to enforce a clear separation of concerns and promote code reuse.

## 1. Root Directories
The monorepo must contain two primary directories at its root: `apps` and `packages`.

## 2. `apps` Directory
This directory contains deployable applications.

-   `apps/app`: The main Next.js user-facing application. It should contain all pages, layouts, and app-specific components.
-   `apps/api`: An optional, separate Next.js application for hosting services like webhooks or cron jobs that need to be deployed independently from the main app.

## 3. `packages` Directory
This directory contains shared code, libraries, and configurations used across the applications in the monorepo.

-   `packages/api`: Contains all shared business logic and domain services. This package acts as the intermediary between the frontend and backend services (database, AI). It is the only package, besides the database package itself, that should interact directly with the database.
-   `packages/auth`: Centralizes all authentication and authorization logic. It provides a consistent interface for Clerk across the monorepo, including middleware and server-side utilities.
-   `packages/database`: Manages all database interactions. It is the single source of truth for the database schema (Drizzle schema files) and the Drizzle ORM client.
-   `packages/design`: The shared design system. It contains reusable UI components, hooks, constants, and the shared Tailwind CSS v4 styles (using `@import "tailwindcss"` without config files). All `shadcn/ui` components must be installed into this package.
-   `packages/ai`: A generalized AI client SDK for the web application to interact with the external AI service. This package must be structured as follows:
    - `src/client.ts`: Initializes and exports the Mastra client.
    - `src/services/`: Contains service classes that abstract the Mastra client's APIs (e.g., `agentService`, `workflowService`).
    - `src/schemas/`: Contains Zod schemas defining the data contracts for AI inputs and outputs.
    - `src/hooks/`: Contains client-side React hooks (e.g., `use-ai-chat`) that wrap the Vercel AI SDK and call the application's backend API routes.
    - `src/components/`: (Optional) Contains generic, reusable UI components for AI interactions.
-   `packages/typescript-config`: Provides the base `tsconfig.json` files that all other packages in the monorepo must extend.