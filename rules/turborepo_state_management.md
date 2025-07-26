# Rule: Turborepo State Management

State management in the web application must follow a clear hierarchy that leverages the strengths of the Next.js App Router and separates server state from client UI state.

## 1. React Server Components (RSC) First
-   **Default Pattern**: All page components and, where possible, components within the `apps/app/src/app/` directory must be React Server Components (RSCs) by default.
-   **Initial Data Fetching**: RSCs are responsible for fetching all initial data required for a page to render. This must be done by directly calling services from the `packages/api` package. Direct database access from RSCs is forbidden.

## 2. Client Component Hydration
-   **Data Passing**: Data fetched in RSCs must be passed as props to Client Components.
-   **SWR Hydration**: This server-fetched data must be used to hydrate the client-side SWR cache via the `fallbackData` option. This pattern is mandatory for preventing client-side fetch waterfalls on initial page load.

## 3. Client-Side State
-   **Server State Management**: `SWR` is the standard library for managing server state on the client. This includes all subsequent fetching, revalidation, and mutation of data after the initial load. React Query is an acceptable alternative when its specific features are needed.
-   **UI State Management**: `Jotai` is the recommended library for managing ephemeral, client-side UI state, such as the open/closed state of modals, menus, and sidebars. Atoms should be organized by feature in the `apps/app/src/atoms/` directory. Zustand and Valtio are acceptable alternatives.
-   **Global State**: React Context should be used judiciously. It's appropriate for truly global state like themes or user preferences, and required for integrating external libraries (e.g., Clerk's `ClerkProvider`).