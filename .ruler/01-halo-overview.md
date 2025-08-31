# Halo Universal Prompt Framework

## Overview
Halo is a universal prompt framework that works across all AI CLI tools (Claude Code, Codex, Gemini, Cursor, etc.). It provides consistent commands, patterns, and delegation logic for seamless multi-agent collaboration.

## Core Philosophy
- **Universal** - Works in any AI CLI tool
- **Bidirectional** - Tools can delegate to each other
- **Consistent** - Same commands across all tools
- **Modular** - Components are reusable
- **Practical** - Focused on daily productivity

## Directory Structure
```
~/.halo/
├── commands/       # Executable commands
│   ├── core/      # Essential daily commands
│   ├── external/  # Delegation to other tools
│   ├── creative/  # Fun sandbox commands
│   ├── integrations/ # Service integrations
│   └── roles/     # Persona-based perspectives
├── components/    # Reusable patterns
└── .ruler/       # Configuration source
```

## Command Categories

### Core Commands
- `/prime` - Initialize project context
- `/build` - Implement features
- `/create` - Create new projects
- `/fix` - Fix bugs and errors
- `/test` - Write and run tests
- `/docs` - Generate documentation
- `/diagram` - Visual architecture
- `/web` - Web research and scraping

### External Orchestration
- `/external:claude` - Use Claude Code's MCP tools
- `/external:codex` - Use GPT-5 deep reasoning
- `/external:gemini` - Use 2M context analysis
- `/external:cursor` - Use implementation engine

### Integrations
- `/github` - GitHub operations
- `/linear` - Linear project management
- `/cloudflare` - Cloudflare deployment
- `/convex` - Convex backend operations

### Creative Sandbox
- `/3d` - 3D graphics and WebGL
- `/video` - Video creation with Remotion
- `/motion` - Motion graphics
- `/unreal/*` - Unreal Engine commands

### Personas
- `/jony` - Jony Ive's design thinking
- `/dieter` - Dieter Rams' principles
- `/bret` - Bret Victor's vision
- `/rick` - Rick Rubin's creativity
- `/tadao` - Tadao Ando's architecture
- `/kenya` - Kenya Hara's emptiness
- `/issey` - Issey Miyake's innovation
- `/teenage` - Teenage Engineering's playfulness