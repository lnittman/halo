# Rule: Turborepo Monorepo Structure

All `*-xyz` monorepos must follow a standardized package structure to enforce a clear separation of concerns and promote code reuse.

## 1. Root Directories
The monorepo must contain:
- `apps/`: Deployable applications
- `packages/`: Shared code and libraries
- `docs/`: Internal AI-optimized development documentation (CLAUDE.md files, architecture guides, etc.)

## 2. `apps` Directory
This directory contains deployable applications.

-   `apps/app`: The main Next.js user-facing application. It should contain all pages, layouts, and app-specific components.
-   `apps/api`: Hono API on Cloudflare Workers for backend services and webhooks.
-   `apps/ai`: Mastra AI service application for agents, workflows, and LLM interactions.
-   `apps/docs`: (Optional) User-facing Mintlify documentation site.
-   `apps/email`: (Optional) Resend dev preview server for email template development.
-   `apps/daemon`: (Optional) Background services and scheduled tasks.
-   `apps/ws`: (Optional) WebSocket server for real-time features.

## 3. `packages` Directory
This directory contains shared code, libraries, and configurations used across the applications in the monorepo.

-   `packages/services`: Contains all shared business logic and domain services. This package acts as the intermediary between the frontend and backend services.
-   `packages/auth`: Centralizes all authentication and authorization logic. It provides a consistent interface for Clerk across the monorepo, including middleware and server-side utilities.
-   `packages/database`: Manages all database interactions. It is the single source of truth for the database schema (Drizzle schema files) and the Drizzle ORM client.
-   `packages/design`: The shared design system. It contains reusable UI components, hooks, constants, and the shared Tailwind CSS v4 styles (using `@import "tailwindcss"` without config files). All `shadcn/ui` components must be installed into this package.
-   `packages/ai`: A generalized AI client SDK and utilities. This package must be structured as follows:
    - `src/client.ts`: Initializes and exports the Mastra client.
    - `src/agents/`: Contains AI agent definitions and instructions.
    - `src/tools/`: Contains tool definitions for agents.
    - `src/schemas/`: Contains Zod schemas defining the data contracts for AI inputs and outputs.
    - `src/hooks/`: Contains client-side React hooks (e.g., `use-ai-chat`) that wrap the Vercel AI SDK.
    - `src/components/`: (Optional) Contains generic, reusable UI components for AI interactions.
-   `packages/orpc`: Shared tRPC/oRPC routers, procedures, and type definitions for type-safe API communication.
-   `packages/storage`: File storage abstractions for S3, R2, or local storage.
-   `packages/analytics`: PostHog analytics integration and event tracking.
-   `packages/email`: Email templates and utilities for transactional emails.
-   `packages/notifications`: In-app notification system components and logic.
-   `packages/collaboration`: Real-time collaboration features (if applicable).
-   `packages/seo`: SEO utilities and metadata management.
-   `packages/logger`: Centralized logging utilities.
-   `packages/next-config`: Shared Next.js configuration.
-   `packages/typescript-config`: Provides the base `tsconfig.json` files that all other packages in the monorepo must extend.
-   `packages/testing`: Shared testing utilities and fixtures.