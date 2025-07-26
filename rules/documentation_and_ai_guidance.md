# Rule: Documentation and AI Guidance

All code must be documented in a way that is optimized for both human developers and Large Language Model (LLM) interpretation.

## 1. LLM-Specific Documentation
-   **`CLAUDE.md` / `AGENTS.md`**: Key directories (e.g., `apps/app`, `packages/api`, `src/mastra/agents`) must contain a `CLAUDE.md` or `AGENTS.md` file.
-   **Purpose**: These files must provide a high-level overview of the directory's architecture, key patterns, and operational guidelines. They serve as a "system prompt" for an LLM analyzing that part of the codebase.
-   **Content**: The content should be written in clear, concise language and use Markdown for structure. It should explain the "why" behind the code, not just the "what".

## 2. Code-Level Documentation
-   **TSDoc/JSDoc**: All exported functions, classes, and complex types must be documented using TSDoc/JSDoc comments.
-   **Required Tags**: Documentation must include `@param` for all parameters, `@returns` for the return value, and a brief summary of the item's purpose. `@example` is strongly encouraged.

## 3. Agent Instructions (`instructions.xml`)
-   **Format**: All Mastra agent instructions must be defined in structured `.xml` files.
-   **Structure**: The XML must be well-structured with clear tags for `<purpose>`, `<capabilities>`, `<methodology>`, `<guidelines>`, and `<response_examples>`. This structured format is required for optimal LLM interpretation.
-   **Includes**: The `<include>` tag must be used to import shared tool definitions, ensuring a modular and DRY instruction set.