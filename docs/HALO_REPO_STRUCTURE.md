# Halo Repository Structure

A modular Claude configuration system that can be partially cloned into different environments.

## Repository Structure

```
halo/
├── commands/               # Command definitions (can be git submodule)
│   ├── *.md               # Individual commands
│   ├── components/        # Reusable components
│   └── rules/            # Project standards
│
├── agents/                # Verb-based AI agents (can be git submodule)
│   ├── *.md              # Individual agents
│   └── README.md         # Agent overview
│
├── roles/                 # Character-based advisors (can be git submodule)
│   ├── personas/         # Philosophy-driven roles
│   │   ├── rick-rubin.md
│   │   ├── dieter-rams.md
│   │   ├── jony-ive.md
│   │   └── teenage-engineering.md
│   │
│   └── functions/        # Job-based roles
│       ├── design-system-engineer.md
│       ├── full-stack-architect.md
│       ├── ai-integration-specialist.md
│       ├── product-manager.md
│       └── performance-engineer.md
│
├── CLAUDE.md              # Main configuration
├── DELEGATION_PATTERNS.md # When to use which agent
├── AGENT_ARCHITECTURE.md  # System design docs
├── CLAUDE_SYSTEM_DESIGN.md
├── README.md              # Setup instructions
└── setup.sh              # Installation script
```

## Setup Options

### Option 1: Git Sparse Checkout (Recommended)
This allows cloning only specific directories from the main repo.

```bash
# Clone with sparse checkout
git clone --filter=blob:none --sparse https://github.com/yourusername/halo.git
cd halo

# Enable only what you need
git sparse-checkout add commands
git sparse-checkout add agents
# or
git sparse-checkout add roles/personas
```

### Option 2: Git Submodules
Make each major directory its own repository, referenced as submodules.

```bash
# Main repo structure
halo/
├── .gitmodules
├── commands (submodule) → github.com/yourusername/halo-commands
├── agents (submodule)   → github.com/yourusername/halo-agents  
├── roles (submodule)    → github.com/yourusername/halo-roles
└── README.md
```

### Option 3: Symlink Strategy
Keep halo as a single repo but symlink needed parts.

```bash
# Clone full repo to a shared location
git clone https://github.com/yourusername/halo.git ~/shared/halo

# In your project
ln -s ~/shared/halo/commands ~/.claude/commands
ln -s ~/shared/halo/agents ~/.claude/agents
# etc.
```

## Recommended Approach: Sparse Checkout

### Why Sparse Checkout?
- Single source of truth
- Easy to update everything
- Flexible partial cloning
- No submodule complexity
- Works with private repos

### Setup Script
```bash
#!/bin/bash
# setup-halo.sh

# Clone halo with sparse checkout
git clone --filter=blob:none --sparse https://github.com/yourusername/halo.git ~/.halo

cd ~/.halo

# Function to install components
install_component() {
    echo "Installing $1..."
    git sparse-checkout add $1
    
    # Create symlinks in .claude
    if [ -d ~/.claude ]; then
        ln -sf ~/.halo/$1 ~/.claude/$1
    fi
}

# Interactive setup
echo "Which components do you want?"
echo "1) Commands only"
echo "2) Commands + Agents"  
echo "3) Everything"
echo "4) Custom selection"

read -p "Choice: " choice

case $choice in
    1) install_component "commands" ;;
    2) 
        install_component "commands"
        install_component "agents"
        ;;
    3)
        install_component "commands"
        install_component "agents"
        install_component "roles"
        ln -sf ~/.halo/CLAUDE.md ~/.claude/
        ln -sf ~/.halo/DELEGATION_PATTERNS.md ~/.claude/
        ;;
    4)
        echo "Available components:"
        echo "- commands"
        echo "- agents"
        echo "- roles/personas"
        echo "- roles/functions"
        read -p "Enter components (space-separated): " components
        for comp in $components; do
            install_component "$comp"
        done
        ;;
esac

echo "Halo setup complete!"
```

## Migration Plan

### 1. Create Halo Repository
```bash
# Initialize new repo
mkdir halo && cd halo
git init

# Copy current structure
cp -r ~/.claude/commands .
cp -r ~/.claude/agents .
cp -r ~/.claude/roles .
cp ~/.claude/*.md .

# Organize roles
cd roles
mkdir -p personas functions
mv dieter-rams.md jony-ive.md teenage-engineering.md rick-rubin.md personas/
mv *.md functions/
cd ..

# Initial commit
git add .
git commit -m "Initial halo configuration"
git remote add origin https://github.com/yourusername/halo.git
git push -u origin main
```

### 2. Update .claude Directory
```bash
# Backup current
mv ~/.claude ~/.claude.backup

# Fresh install
mkdir ~/.claude
cd ~/.claude
~/.halo/setup.sh  # Run setup script
```

### 3. Environment-Specific Configs
Each environment can have local overrides:

```
~/.claude/
├── commands/     # Symlink to ~/.halo/commands
├── agents/       # Symlink to ~/.halo/agents
├── roles/        # Symlink to ~/.halo/roles
├── CLAUDE.md     # Symlink to ~/.halo/CLAUDE.md
└── LOCAL.md      # Local overrides (not in halo)
```

## Benefits

1. **Modularity**: Install only what you need
2. **Consistency**: Single source of truth
3. **Flexibility**: Different configs for different projects
4. **Maintainability**: Update once, propagate everywhere
5. **Discoverability**: Public repo can be explored/forked

## Future Enhancements

### Package Manager Integration
```bash
# Potential future CLI
halo install commands
halo install agents
halo install roles/personas
halo update
halo list
```

### Version Management
```bash
# Pin to specific versions
halo install commands@v1.2.0
halo install agents@latest
```

### Profiles
```bash
# Different profiles for different needs
halo use web-dev    # Commands + build agents
halo use ai-dev     # Commands + AI agents + roles
halo use minimal    # Just commands
```

This structure gives you maximum flexibility while keeping things simple and maintainable.