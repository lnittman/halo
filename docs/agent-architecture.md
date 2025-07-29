# Claude Agent Architecture

A powerful system combining commands, roles, and agents for maximum flexibility and capability.

## Two-Layer Architecture

### 1. Commands (`/commands/`)
**Purpose**: Direct actions and workflows
- Remain in conversation context
- Execute specific tasks
- Can be chained together
- Examples: `/build`, `/create`, `/prime`

### 2. Agents (`/agents/`)
**Purpose**: Isolated single-purpose specialists
- Have their own context window
- Use specific, restricted tools
- Focus on one domain deeply
- Triggered by PROACTIVE descriptions

## Key Design Decisions

### Commands Stay Simple
- Remove session management overhead
- Focus on direct action
- Leverage conversation context
- Quick and responsive

### Agents Provide Specialization
- **tech-docs**: Aggregate documentation from multiple sources
- **github-whisperer**: Git operations and repository management
- **cloudflare-whisperer**: Edge deployment and services
- **test-coverage**: Write and maintain comprehensive tests
- **dependency-doctor**: Package management and updates
- **linear-whisperer**: Project tracking synchronization
- **audit-codebase**: Code quality analysis
- **simplify-design**: Radical reduction and minimalism
- **polish-interface**: Final UI touches and refinement

### Roles Enable Consistency
- Shared expertise across agents
- Reusable personas
- Consistent voice and approach

## Usage Patterns

### Documentation Aggregation
```
User: "how do I use Mastra.ai?"
Assistant: *uses tech-docs agent*
→ Fetches from context7 and official docs
→ Aggregates all relevant information
→ Creates comprehensive reference
```

### Git Operations
```
User: "commit these changes"
Assistant: *uses github-whisperer agent*
→ Analyzes diffs comprehensively
→ Creates meaningful commit messages
→ Manages branches and PRs
```

### Test Coverage
```
User: "add tests for this component"  
Assistant: *uses test-coverage agent*
→ Analyzes code paths
→ Writes comprehensive tests
→ Ensures high coverage
```

### Deployment
```
User: "deploy to cloudflare"
Assistant: *uses cloudflare-whisperer agent*
→ Configures workers/pages
→ Sets up edge functions
→ Optimizes performance
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

1. **For documentation**: Use `tech-docs` to aggregate references
2. **For git/github**: Use `github-whisperer` for repository tasks
3. **For testing**: Use `test-coverage` to ensure quality
4. **For deployment**: Use `cloudflare-whisperer` for edge services
5. **For building**: Handle directly in main thread with Claude

The system is designed to be fluid - use whatever combination helps you create great products.