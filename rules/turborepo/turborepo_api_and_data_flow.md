# Rule: Turborepo API and Data Flow

The flow of data and execution must follow a clear, uni-directional pattern from the UI to the backend services, with a strict separation of concerns.

## 1. Primary API Pattern: Hono API on Cloudflare Workers
-   **Use Case**: The Hono API (`apps/api`) is the primary backend service handling all API requests, deployed on Cloudflare Workers for edge performance.
-   **Structure**: Routes are organized using Hono's router pattern with type-safe oRPC/tRPC procedures.
-   **Authentication**: Uses Clerk for authentication with JWT verification at the edge.
-   **Logic**: API routes must be lightweight and delegate business logic to the `packages/services` package.
-   **Type Safety**: Shared types and procedures are defined in `packages/orpc` for end-to-end type safety.

## 2. Secondary API Pattern: Next.js Server Actions
-   **Use Case**: Server Actions in `apps/app/src/actions/` can be used for:
    1.  Form submissions and simple mutations when edge deployment isn't required
    2.  Real-time updates using `revalidatePath` or `revalidateTag`
    3.  File uploads that need Next.js middleware processing
-   **Business Logic**: Server Actions must delegate to `packages/services` for business logic.

## 3. Service Layer (`packages/services`)
-   **Responsibility**: The `packages/services` package is the single source of truth for all business logic. It is the only package that should directly interact with the database (`packages/database`) and coordinate with AI services.
-   **Structure**: Logic must be organized into domain-specific services (e.g., `chatService`, `projectService`).
-   **Service Layer Boundaries**: The service layers have a strict hierarchy:
    - `packages/services` IS ALLOWED to import from `packages/database`, `packages/ai`, and other utility packages.
    - `packages/ai` MUST NEVER import from `packages/services` or `packages/database`. It must remain a pure utilities package.
    - `apps/api` and `apps/app` both delegate to `packages/services` for business logic.