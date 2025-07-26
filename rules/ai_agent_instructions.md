# Rule: AI Agent Instructions

All agent instructions must be defined in a structured, consistent format to ensure optimal performance and maintainability.

## 1. Format
-   **XML**: Agent instructions are typically defined in `.xml` files for complex agents. This structured format provides reliable LLM interpretation. Simple agents may define instructions inline in TypeScript.

## 2. Structure
The XML file for each agent must follow a standard structure with clear, descriptive tags. The following top-level tags are required:
-   `<purpose>`: A concise statement of the agent's primary role and goal.
-   `<capabilities>`: A list of specific actions the agent can perform, wrapped in `<capability>` tags.
-   `<methodology>`: A series of `<step>` tags that outline the agent's standard operational procedure (e.g., Analyze, Plan, Execute, Summarize).
-   `<guidelines>`: A list of behavioral rules and principles, wrapped in `<guideline>` tags.
-   `<response_examples>`: A set of `<example>` blocks demonstrating desired query-response patterns.

## 3. Tool and Output Definitions
-   **Tool Inclusion**: The `<include>` tag must be used to import shared tool definitions from the `tools/mcp/` directory. This keeps the main instruction file clean and promotes tool reuse.
-   **Output Creation**: For agents that generate structured content, instructions must specify the use of `<OUTPUT_START>` and `<OUTPUT_END>` tags. The rule must clearly define the required attributes (`type`, `title`) and the available content types (e.g., `code`, `markdown`).