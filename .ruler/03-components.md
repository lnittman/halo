# Reusable Components

## Component System
Components are reusable patterns that commands can integrate. They ensure consistency across all commands and tools.

## Available Components

### thinking-blocks.md
Structured reasoning display for transparency:
- Understanding phase
- Analysis phase  
- Planning phase
- Execution phase

Usage: Shows AI reasoning process to build trust

### verification-patterns.md
Safety checks before dangerous operations:
- Impact assessment
- User confirmation
- Rollback planning
- Risk evaluation

Usage: Prevents accidental damage

### output-standards.md
Consistent formatting across all outputs:
- Markdown structure
- Emoji usage patterns
- Progress indicators
- Success/error formatting

Usage: Professional, readable outputs

### repomix-context.md
Smart context gathering with token management:
- Progressive refinement
- Token counting
- File filtering
- Project detection

Usage: Comprehensive codebase understanding

### next-command.md
Intelligent command suggestion:
- Analyzes current state
- Suggests logical next step
- Provides complete command
- Includes rationale

Usage: Guides users through workflows

### parallel-tasks.md
Concurrent execution patterns:
- Task batching
- Resource management
- Progress tracking
- Error handling

Usage: Efficient multi-task execution

### planning-phases.md
Structured planning approach:
- Requirement gathering
- Solution design
- Implementation planning
- Risk assessment

Usage: Complex task planning

### diagram-patterns.md
Visual representation patterns:
- ASCII diagrams
- Mermaid syntax
- Architecture visualization
- Flow charts

Usage: Visual communication

### interop-patterns.md
Command integration patterns:
- Command chaining
- State passing
- Context preservation
- Error propagation

Usage: Multi-command workflows

### xml-transformer.md
Input transformation to structured format:
- Natural language parsing
- Parameter extraction
- Intent detection
- Validation

Usage: Robust input handling

## Component Integration

### In Commands
```xml
<components>
  <use>@file:../../components/thinking-blocks.md</use>
  <use>@file:../../components/verification-patterns.md</use>
  <use>@file:../../components/output-standards.md</use>
</components>
```

### Component Principles
1. **Single Responsibility** - Each component does one thing well
2. **Composable** - Components work together seamlessly
3. **Reusable** - Used across multiple commands
4. **Consistent** - Same behavior everywhere
5. **Documented** - Clear usage instructions
