# Rule: AI Service Architecture

The AI service (`*-ai`) must be a standalone Node.js/TypeScript project, completely separate from any web monorepo. It is responsible for defining and running all core AI logic.

## 1. Core Framework
-   **Mastra**: The `@mastra/core` library is the mandatory framework for defining all agents, tools, and workflows.

## 2. Directory Structure
All AI logic must be contained within the `src/mastra/` directory.
-   `agents/`: Contains a subdirectory for each distinct AI agent (e.g., `chat/`, `code/`). Each agent directory must include its own `index.ts` for definition, `instructions.xml`, and `memory.ts`.
-   `tools/`: Contains definitions for tools that agents can use, organized by function.
-   `workflows/`: Defines multi-step processes that combine agents and tools.
-   `lib/`: Contains shared utilities, such as the RAG implementation for attachments.

## 3. Model Initialization
-   **Pattern**: A lazy-initialization "model factory" pattern must be used for all language models. This involves creating a `getModel()` function that initializes the model on its first call and returns the cached instance on subsequent calls. This is required to prevent multiple "Creating model factory" logs during startup and to optimize resource usage.

## 4. Storage and Memory
-   **Database**: The AI service must connect to the same shared PostgreSQL database as the web application.
-   **Storage Layer**: `@mastra/pg` is the required library for interacting with the database for memory (`PostgresStore`) and vector search (`PgVector`). Shared instances of these stores must be created to avoid multiple database connections.