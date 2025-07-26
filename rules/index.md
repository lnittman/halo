# Claude Code Rules Index

This directory contains architectural rules and standards that govern all development across the ecosystem. These rules are designed to be interpreted and enforced by Claude Code commands, especially `/user:ecosystem` and `/user:create`.

## Rule Categories

### 1. General & Architectural Rules
- `product_layout.md` - Overall product structure and repository organization
- `documentation_and_ai_guidance.md` - Documentation standards for humans and AI

### 2. Turborepo Rules (`*-xyz` projects)
- `turborepo_tooling.md` - Required tools, dependencies, and technology stack
- `turborepo_monorepo_structure.md` - Monorepo organization and package structure
- `turborepo_state_management.md` - State management patterns and hierarchy
- `turborepo_api_and_data_flow.md` - API patterns and data flow architecture
- `turborepo_ui_patterns.md` - Common UI patterns and libraries
- `version_guidelines.md` - Dependency version management

### 3. AI Service Rules (`*-ai` projects)
- `ai_service_architecture.md` - Mastra framework structure and patterns
- `ai_agent_instructions.md` - XML format for agent instructions

### 4. Apple Platform Rules (`*-apple` projects)
- `apple_project_structure.md` - Xcode project and Swift package organization
- `apple_architecture_patterns.md` - MVVM and architectural patterns
- `apple_ui_ux_patterns.md` - Design system and interaction patterns
- `apple_networking_layer.md` - Network layer implementation requirements

## Usage in Commands

### In `/user:ecosystem`
The ecosystem command uses these rules to:
- Audit projects for compliance
- Enforce standards across the ecosystem
- Generate compliance reports
- Suggest fixes for violations

### In `/user:create`
The create command uses these rules to:
- Generate compliant project structures
- Initialize with correct dependencies
- Set up proper architectural patterns
- Ensure zero manual configuration needed

## Rule Enforcement

All rules are:
1. **Mandatory** - Not optional guidelines
2. **Specific** - Clear, actionable requirements
3. **Testable** - Can be verified programmatically
4. **Complete** - Cover all aspects of development

## Integration with STANDARDS.md

These rules complement and detail the high-level standards defined in `~/Developer/STANDARDS.md`. While STANDARDS.md provides the overview, these rules provide the implementation specifics.