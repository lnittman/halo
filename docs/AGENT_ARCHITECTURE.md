# Claude Agent Architecture

A powerful system combining commands, roles, and agents for maximum flexibility and capability.

## Three-Layer Architecture

### 1. Commands (`/commands/`)
**Purpose**: Direct actions and workflows
- Remain in conversation context
- Execute specific tasks
- Can be chained together
- Examples: `/user:build`, `/user:create`, `/user:prime`

### 2. Roles (`/roles/`)
**Purpose**: Reusable expertise definitions
- Define specialized knowledge domains
- Can be referenced by agents
- Provide consistent personas
- Example: `design-system-engineer.md`

### 3. Agents (`/agents/`)
**Purpose**: Isolated specialized assistants
- Have their own context window
- Can use specific tools
- Embody roles or combine them
- Can invoke commands explicitly

## Key Design Decisions

### Commands Stay Simple
- Remove session management overhead
- Focus on direct action
- Leverage conversation context
- Quick and responsive

### Agents Provide Specialization
- **design-inspiration**: Browse and recreate designs with MCP tools
- **build-anything**: Rapid prototyping with taste
- **dieter-rams**: Minimalist design philosophy
- **jony-ive**: Obsessive attention to detail
- **teenage-engineering**: Playful, innovative design
- **product-visionary**: Meta-agent combining perspectives

### Roles Enable Consistency
- Shared expertise across agents
- Reusable personas
- Consistent voice and approach

## Usage Patterns

### Stream-of-Consciousness Design
```
User: "go to linear.app I want that sidebar"
Assistant: *uses design-inspiration agent*
→ Browses Linear with MCP tools
→ Extracts design patterns
→ Builds matching component
```

### Philosophical Guidance
```
User: "is this good design?"
Assistant: *uses dieter-rams agent*
→ Evaluates against 10 principles
→ Suggests simplifications
→ Questions everything
```

### Rapid Building
```
User: "build me a todo app like Things 3"  
Assistant: *uses build-anything agent*
→ Analyzes Things 3 design
→ Creates beautiful prototype
→ Adds delightful details
```

### Combined Perspectives
```
User: "help me envision this product"
Assistant: *uses product-visionary agent*
→ Channels multiple perspectives
→ Integrates with /user:vision command
→ Creates cohesive vision
```

## Benefits

1. **Flexibility**: Use commands for workflow, agents for expertise
2. **Isolation**: Agents don't pollute main context
3. **Personality**: Each agent has distinct voice and approach
4. **Integration**: Agents can use commands and MCP tools
5. **Extensibility**: Easy to add new agents/roles

## Future Possibilities

- Agents that embody specific users/customers
- Time-period specific agents (60s designer, 80s hacker)
- Domain experts (security-auditor, performance-optimizer)
- Collaborative agents that work together
- Agents that learn from your preferences

## Quick Start

1. **For design work**: Use `design-inspiration` or specific designer agents
2. **For building**: Use `build-anything` for rapid prototypes
3. **For vision**: Use `product-visionary` for big-picture thinking
4. **For expertise**: Use specific agents like `dieter-rams` for guidance

The system is designed to be fluid - use whatever combination helps you create great products.