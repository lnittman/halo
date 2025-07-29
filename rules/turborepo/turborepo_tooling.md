# Rule: Turborepo Tooling and Dependencies

All `*-xyz` projects must adhere to a standardized set of tools to ensure consistency, performance, and a smooth developer experience.

## 1. Core Stack
-   **Package Manager**: `pnpm` is mandatory for managing dependencies and workspaces.
-   **Language**: `TypeScript` (latest stable version) is required for all web and AI projects. `strict` mode must be enabled in the root `tsconfig.json`.
-   **Framework**: `Next.js` (latest stable version) with the App Router is the required framework for the primary web application (`apps/app`).

## 2. Formatting and Linting
-   **Primary Tool**: `Biome` is the required, unified tool for formatting and linting. A `biome.json` file must exist at the root of the monorepo.

## 3. Authentication
-   **Provider**: `Clerk` is the mandatory authentication provider.
-   **UI**: `Clerk Elements` must be used to build custom, unstyled login and sign-up forms in all unauthenticated page routes within `apps/app`.

## 4. UI and Styling
-   **Styling**: `Tailwind CSS` (version 4 or later) is the required CSS framework.
-   **Component Primitives**: `Radix UI` must be used for all accessible, unstyled component primitives.
-   **Component Patterns**: The `shadcn/ui` methodology, including the use of `cva` (class-variance-authority) and `tailwind-merge`, is the standard for building the design system. A `components.json` file must be present in the `packages/design` directory to configure this.

## 5. State Management
-   **Client UI State**: `Jotai` is the standard library for managing local and shared UI state that is ephemeral and client-side only.
-   **Server State (Client)**: `SWR` is the standard library for fetching, caching, and mutating all data that originates from the server.

## 6. Database
-   **ORM**: `Drizzle ORM` is the mandatory ORM for all database interactions.
-   **Database**: PostgreSQL is the standard database.
-   **Migrations**: Drizzle Kit for schema migrations.