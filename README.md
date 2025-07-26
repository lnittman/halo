# Halo - AI Assistant Configuration System

A modular, portable configuration system for AI coding assistants (Claude Code, GitHub Copilot, Cursor, etc.)

## Overview

Halo provides a unified way to configure AI assistants with:
- **Commands**: High-level workflows and task patterns
- **Agents**: Specialized AI personalities for different tasks
- **Roles**: Expert personas and functional specialists
- **Rules**: Universal coding standards and patterns

## Structure

```
halo/
├── commands/           # Universal command concepts
├── agents/            # Task-focused AI agents
├── roles/             # Expert personas & specialists
│   ├── personas/     # Character-based (Rick Rubin, Dieter Rams)
│   └── functions/    # Job-based (architect, engineer)
├── rules/            # Coding standards & patterns
└── docs/             # Documentation
```

## Installation

### For Claude Code

```bash
# Clone the repository
git clone https://github.com/yourusername/halo ~/.halo

# Symlink to Claude directory
ln -s ~/.halo ~/.claude
```

### For Other Tools

See adapters in `HALO_REPO_STRUCTURE.md` for tool-specific setup.

## Key Features

### Commands
- `/prime` - Initialize context
- `/build` - Execute implementations
- `/create` - Create new projects
- `/vision` - Explore possibilities
- `/design` - Design systems
- `/audit` - Code quality checks

### Agents
- `build-anything` - Rapid prototyping
- `recreate-design` - Copy UI/UX patterns
- `simplify-design` - Minimalist refactoring
- `polish-interface` - Final touches
- `orchestrate-work` - Meta coordination

### Roles
**Personas**: Rick Rubin, Dieter Rams, Jony Ive, Teenage Engineering
**Functions**: Full-Stack Architect, AI Integration Specialist, Product Manager

## Philosophy

Halo embodies the principle that AI assistants should:
1. Understand context deeply
2. Apply consistent patterns
3. Delegate to specialists
4. Maintain high standards
5. Enable creative exploration

## Contributing

Feel free to submit issues and enhancement requests!

## License

MIT