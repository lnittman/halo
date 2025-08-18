# 🌐 External CLI Orchestration Framework

Claude orchestrates external CLIs by gathering context, writing comprehensive specs, and delegating execution.

## 🎯 Orchestration Philosophy

### Claude as Orchestrator
1. **Gathers Context** - Uses file tools, MCP, and native analysis capabilities
2. **Writes Specifications** - Creates comprehensive PRDs with technical excellence
3. **Delegates Execution** - Sends focused specs to specialized CLIs
4. **Coordinates Results** - Manages multi-tool workflows

### Tool Capabilities

**Gemini (2M Context)**
- Specializes in analysis, auditing, pattern extraction
- Can process entire codebases in single context

**Cursor (GPT-5 + Sonnet 1M)**  
- Model auto-selection: GPT-5 for reasoning, Sonnet for large context
- Autonomous file operations and implementation
- Never uses Opus (explicitly avoided)

**Codex (GPT-5)**
- Strategic planning and deep reasoning
- Architecture design and complex debugging

## 📋 Command Structure

```
commands/external/
├── gemini/          # 2M context analysis
│   ├── main.md      # Intelligent routing
│   ├── prime.md     # Full initialization
│   ├── audit.md     # Security audit
│   └── analyze.md   # Pattern extraction
│
├── cursor/          # GPT-5/Sonnet execution
│   ├── main.md      # Model-agnostic routing
│   ├── prime.md     # Sonnet 1M initialization
│   ├── build.md     # Spec execution
│   ├── fix.md       # Bug fixing
│   ├── architect.md # Architecture + scaffolding
│   └── debug.md     # Debug + immediate fixes
│
└── codex/           # GPT-5 strategic reasoning
    ├── main.md      # Intelligent routing
    ├── build.md     # Build planning
    ├── fix.md       # Root cause analysis
    ├── architect.md # System design
    └── debug.md     # Deep debugging
```

## 🔄 Orchestration Workflow

### Standard Pattern
```bash
# 1. Claude gathers context
/prime                          # Analyze project with Claude's tools

# 2. Claude writes comprehensive spec
cat > spec.md << 'EOF'
[Claude creates detailed PRD using all available context]
EOF

# 3. Delegate to appropriate CLI
/external:cursor:build          # Execute spec with auto-selected model
/external:cursor:fix           # Fix with Claude's analysis
```

### Model Selection (Cursor)
- **Sonnet 4**: Large context operations (>100k tokens), full codebase tasks
- **GPT-5**: Complex reasoning, architecture, strategic debugging
- **Never Opus**: Explicitly avoided in all commands

## 🚀 Usage Examples

### Build Feature with Orchestration
```bash
# Claude analyzes and writes spec
/build authentication system    # Claude creates comprehensive PRD

# Execute with cursor (auto-selects model)
/external:cursor:build          # Sonnet for large context or GPT-5 for complexity
```

### Fix Bug with Full Context
```bash
# Claude gathers logs and analyzes
/analyze bug in payment flow    # Claude investigates issue

# Execute fix with optimal model
/external:cursor:fix            # Auto-selects based on complexity
```

### Initialize with Large Context
```bash
# Two options for comprehensive initialization
/external:gemini:prime          # 2M context with Gemini
/external:cursor:prime          # 1M context with Sonnet + immediate fixes
```

## 🎛️ Key Principles

### Spec-Driven Execution
- Claude prepares comprehensive specifications
- External CLIs receive complete context upfront
- No need for CLIs to gather additional context
- Focus on execution excellence

### Intelligent Model Selection
- Commands auto-select optimal model
- Sonnet for large context (1M tokens)
- GPT-5 for complex reasoning
- Never use Opus

### Clean Command Names
- Simple, direct naming (`build`, `fix`, `debug`)
- No redundant prefixes or suffixes
- Clear hierarchy (`/external:cursor:build`)

## 📊 Tool Selection Matrix

| Task Type | Primary Tool | Model | Reason |
|-----------|-------------|-------|---------|
| Full codebase analysis | Gemini | - | 2M context window |
| Initialization | Cursor or Gemini | Sonnet | 1M or 2M context |
| Build from spec | Cursor | Auto | Executes Claude's PRD |
| Fix bugs | Cursor | Auto | Immediate implementation |
| Strategic planning | Codex | GPT-5 | Deep reasoning |
| Architecture design | Codex or Cursor | GPT-5 | Planning vs scaffolding |
| Complex debugging | Codex or Cursor | GPT-5 | Analysis vs fixing |

## 🔧 Configuration

### Environment Setup
```bash
# Install CLIs
npm install -g @google-gemini/gemini-cli
npm install -g @openai/codex
curl https://cursor.com/install -fsSL | bash

# Verify installations
which gemini && which codex && which cursor-agent
```

### Model Configuration
- Cursor auto-selects between GPT-5 and Sonnet
- Codex always uses GPT-5 for reasoning
- Gemini uses its native 2M context model
- Never configure Opus

## 💡 Best Practices

1. **Let Claude Orchestrate**
   - Claude gathers all context first
   - Claude writes detailed specifications
   - External CLIs execute with focus

2. **Model Selection**
   - Let commands auto-select models
   - Trust Sonnet for large context
   - Use GPT-5 for complex reasoning

3. **Workflow Optimization**
   - Use `/external:cursor:prime` for immediate action
   - Use `/external:gemini:prime` for analysis only
   - Chain commands for complex workflows

4. **Spec Quality**
   - Claude provides comprehensive PRDs
   - Include success criteria
   - Define technical constraints
   - Provide example patterns

---

*This orchestration framework enables Claude to effectively coordinate external CLI tools, leveraging each tool's strengths while maintaining comprehensive context and control.*