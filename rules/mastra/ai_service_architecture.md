# Rule: AI Service Architecture

The AI service (`apps/ai`) is integrated within the turborepo as a standalone application. It is responsible for defining and running all core AI logic using the Mastra framework.

## 1. Core Framework
-   **Mastra**: The `@mastra/core` library is the mandatory framework for defining all agents, tools, and workflows.

## 2. Directory Structure
The AI service follows this structure:
-   `apps/ai/src/mastra/`: Core AI logic directory
    -   `agents/`: Contains a subdirectory for each distinct AI agent (e.g., `chat/`, `code/`). Each agent directory must include its own `index.ts` for definition, `instructions.xml`, and `memory.ts`.
    -   `tools/`: Contains definitions for tools that agents can use, organized by function.
    -   `workflows/`: Defines multi-step processes that combine agents and tools.
    -   `lib/`: Contains shared utilities, such as the RAG implementation for attachments.
-   `packages/ai/`: Shared AI utilities and client SDK used by other apps in the monorepo

## 3. Model Initialization
-   **Pattern**: A lazy-initialization "model factory" pattern must be used for all language models. This involves creating a `getModel()` function that initializes the model on its first call and returns the cached instance on subsequent calls. This is required to prevent multiple "Creating model factory" logs during startup and to optimize resource usage.

## 4. Storage and Memory
-   **Database**: The AI service must connect to the same shared PostgreSQL database as the web application.
-   **Storage Layer**: `@mastra/pg` is the required library for interacting with the database for memory (`PostgresStore`) and vector search (`PgVector`). Shared instances of these stores must be created to avoid multiple database connections.