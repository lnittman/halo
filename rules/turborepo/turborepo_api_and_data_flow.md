# Rule: Turborepo API and Data Flow

The flow of data and execution must follow a clear, uni-directional pattern from the UI to the backend services, with a strict separation of concerns.

## 1. Primary API Pattern: Server Actions
-   **Use Case**: Server Actions are the default and required method for all data mutations (e.g., create, update, delete operations) initiated from the client.
-   **Location**: Server Actions must be defined in the `apps/app/src/actions/` directory and organized into domain-specific files (e.g., `chat.ts`, `project.ts`).
-   **Logic**: Server Actions must be lightweight and delegate all business logic to the appropriate services in the `packages/api` package. They must not contain business logic themselves.
-   **Validation and Authorization**: All Server Actions must validate their inputs using a Zod schema and perform an authentication and authorization check before calling any service.
-   **Cache Invalidation**: After a successful mutation, Server Actions must use `revalidatePath` or `revalidateTag` to invalidate the Next.js cache.

## 2. Secondary API Pattern: Route Handlers
-   **Use Case**: API Route Handlers (`app/api/**/route.ts`) must only be used for the following specific scenarios:
    1.  GET requests for data fetching by clients.
    2.  Serving as endpoints for third-party webhooks (e.g., Clerk).
    3.  Internal service-to-service communication (e.g., from the AI service to the web app's RAG API).
    4.  Health checks.
-   **Business Logic**: Route Handlers must not contain business logic directly. They must delegate all logic to services within the `packages/api` package.

## 3. Service Layer (`packages/api`)
-   **Responsibility**: The `packages/api` package is the single source of truth for all business logic. It is the only package that should directly interact with the database (`@repo/database`) and the AI client (`@repo/ai`).
-   **Structure**: Logic must be organized into domain-specific services (e.g., `chatService`, `projectService`).
-   **Service Layer Boundaries**: The service layers have a strict hierarchy:
    - `packages/api` IS ALLOWED to import from and use `packages/ai`.
    - `packages/ai` MUST NEVER import from `packages/api` or `packages/database`. It must remain a pure, dependency-free client for the external AI service.