# Halo Repository Structure v2

A modular AI assistant configuration system that works across Claude Code, GitHub Copilot, Cursor, and other AI coding tools.

## Core Repository Structure

```
halo/
├── README.md                      # Overview and quick start
├── halo.json                      # Repository metadata
│
├── commands/                      # Universal command concepts
│   ├── index.json                # Command registry
│   ├── prime.md                  # Context initialization
│   ├── build.md                  # Implementation execution
│   ├── create.md                 # Project creation
│   ├── vision.md                 # Creative exploration
│   ├── design.md                 # Design system work
│   ├── audit.md                  # Code quality checks
│   ├── docs.md                   # Documentation
│   ├── diagram.md                # Visual architecture
│   ├── ecosystem.md              # Meta-level analysis
│   └── components/               # Reusable command components
│       ├── thinking-blocks.md
│       ├── xml-transformer.md
│       └── ...
│
├── agents/                        # All agent types (unified)
│   ├── index.json                # Agent registry with metadata
│   ├── capabilities/             # Task-focused agents
│   │   ├── build-anything.md
│   │   ├── recreate-design.md
│   │   ├── simplify-design.md
│   │   ├── polish-interface.md
│   │   ├── audit-codebase.md
│   │   ├── envision-product.md
│   │   └── orchestrate-work.md
│   │
│   ├── specialists/              # Functional role agents
│   │   ├── design-system-engineer.md
│   │   ├── full-stack-architect.md
│   │   ├── ai-integration-specialist.md
│   │   ├── product-manager.md
│   │   └── performance-engineer.md
│   │
│   └── personas/                 # Character-based agents
│       ├── rick-rubin.md
│       ├── dieter-rams.md
│       ├── jony-ive.md
│       └── teenage-engineering.md
│
├── rules/                        # Universal standards
│   ├── index.md
│   ├── documentation.md
│   ├── code-quality.md
│   ├── architecture/
│   │   ├── patterns.md
│   │   ├── monorepo-structure.md
│   │   └── state-management.md
│   └── platform/
│       ├── turborepo.md
│       ├── nextjs.md
│       ├── swift.md
│       └── ai-services.md
│
├── patterns/                     # Reusable patterns & templates
│   ├── delegation.md            # When to use which agent
│   ├── architecture.md          # System design patterns
│   └── workflows.md             # Common task flows
│
└── adapters/                    # Tool-specific configurations
    ├── claude-code/
    │   ├── setup.sh            # Installation script
    │   ├── CLAUDE.md           # Main config file
    │   ├── command-syntax.md   # /user:command mappings
    │   └── sub-agents.md       # Task tool integration
    │
    ├── github-copilot/
    │   ├── setup.sh
    │   ├── commands.json       # @command mappings
    │   └── workspace/          # Workspace settings
    │
    ├── cursor/
    │   ├── setup.sh
    │   ├── .cursorrules        # Rules format
    │   └── commands.md         # Command adaptations
    │
    └── aider/
        ├── setup.sh
        └── .aider.conf.yml     # Configuration
```

## Key Concepts

### 1. Commands as Universal Concepts
Commands represent high-level workflows that adapt to each tool:

```markdown
# commands/build.md
# Build Execution Command

Execute on plans, implement features, and build anything based on context.

## Core Concept
Transform plans into reality by understanding context and executing with precision.

## Workflow
1. Assess context from conversation
2. Understand build requirements  
3. Implement systematically
4. Verify results

## Tool Adaptations
- Claude Code: `/user:build` or `/build`
- Copilot: `@workspace /build` or custom command
- Cursor: Referenced in chat or via command palette
- Aider: `/build` in chat
```

### 2. Agent Metadata System
Each agent includes metadata for tool compatibility:

```json
// agents/index.json
{
  "agents": {
    "build-anything": {
      "type": "capability",
      "category": "implementation",
      "path": "capabilities/build-anything.md",
      "tools_required": ["file_ops", "code_gen"],
      "invoke_patterns": {
        "claude-code": "Task tool with subagent_type",
        "copilot": "@workspace mention",
        "cursor": "Agent reference in chat",
        "aider": "Direct prompt inclusion"
      }
    }
  }
}
```

### 3. Tool Adapters
Each tool gets an adapter that translates halo concepts:

#### Claude Code Adapter
```bash
# adapters/claude-code/setup.sh
#!/bin/bash

# Link commands
ln -s $HALO_ROOT/commands ~/.claude/commands

# Link agents  
ln -s $HALO_ROOT/agents ~/.claude/agents

# Generate CLAUDE.md with proper mappings
cat > ~/.claude/CLAUDE.md << EOF
# Claude Configuration (via Halo)

## Commands
$(generate_command_mappings)

## Agent Delegation
$(generate_agent_patterns)
EOF
```

#### GitHub Copilot Adapter
```json
// adapters/github-copilot/commands.json
{
  "commands": [
    {
      "name": "build",
      "description": "Execute on plans and build features",
      "command": "@workspace /build",
      "source": "halo/commands/build.md"
    }
  ]
}
```

### 4. Unified Agent Structure
All roles become agents with type metadata:

```markdown
---
type: persona
name: rick-rubin
description: Zen master of creative production
---

# Rick Rubin

[Content remains the same]
```

```markdown
---
type: specialist  
name: design-system-engineer
description: Technical design system expert
---

# Design System Engineer

[Content remains the same]
```

## Benefits of This Structure

1. **Universal Commands**: Core workflows work everywhere
2. **Flexible Agents**: All agent types in one place with metadata
3. **Tool Adaptability**: Each tool interprets halo concepts its own way
4. **Single Source**: One repo, multiple tools
5. **Clear Separation**: Core concepts vs tool-specific syntax
6. **Easy Extension**: Add new tools by adding adapters

## Installation Example

```bash
# Clone halo
git clone https://github.com/yourusername/halo ~/.halo

# Install for Claude Code
~/.halo/adapters/claude-code/setup.sh

# Install for Copilot
~/.halo/adapters/github-copilot/setup.sh

# Or selective install
halo install --tool=claude-code --components=commands,agents
```

This structure maintains the conceptual power of commands while adapting to each tool's specific implementation!