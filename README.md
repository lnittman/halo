# halo

universal prompt framework for AI CLI tools. one system, many contexts.

## installation

```bash
git clone https://github.com/lnittman/halo.git
cd halo
```

## usage

```bash
/prime                     # analyze project context
/build feature-name        # implement features
/test                      # generate tests
/docs                      # create documentation

/external:codex task       # deep reasoning & debugging
/external:gemini audit     # comprehensive codebase analysis
/external:claude task      # orchestration with MCP tools
/external:charlie task     # autonomous TypeScript via GitHub
```

## structure

```
./
├── commands/           # executable commands
│   ├── core/          # essential commands
│   ├── external/      # tool orchestration
│   ├── creative/      # specialized workflows
│   └── roles/         # persona perspectives
├── components/         # reusable patterns
│   └── external/      # structured prompt templates
└── .ruler/            # configuration source
```

## core commands

- `/prime` - analyze project structure and context
- `/build` - implement features with existing patterns  
- `/test` - generate comprehensive test suites
- `/docs` - create technical documentation
- `/create` - scaffold new projects
- `/fix` - debug and resolve issues
- `/diagram` - generate visual architecture

## external commands

orchestrate specialized AI tools:

- `/external:codex` - GPT-5 for deep reasoning and debugging
- `/external:gemini` - 2M context window for full codebase analysis
- `/external:claude` - MCP tool orchestration and cross-project work
- `/external:charlie` - autonomous TypeScript implementation via GitHub
- `/external:general` - universal prompt generation for any tool

## components

reusable patterns across commands:

- `xml-structure.md` - structured prompt templates
- `reasoning-patterns.md` - CoT, CoVe, ReAct patterns
- `output-formats.md` - standardized response structures
- `thinking-blocks.md` - transparent reasoning display
- `verification-patterns.md` - safety checks

## configuration

`.ruler/` contains:
- coding standards
- project structure patterns
- delegation logic between tools
- technology stack defaults

## external tool workflow

```bash
# 1. generate world-class prompt
/external:codex debug authentication issue

# 2. copy generated XML prompt
# 3. run target CLI tool
codex

# 4. paste prompt into tool
```

charlie workflow (special case):
```bash
/external:charlie implement new feature
# creates GitHub issue automatically
# manually add @CharlieHelps comment to trigger
```

## requirements

- bash/zsh shell
- git
- gh CLI (for charlie)
- target AI CLI tools as needed

## extending

add new commands:
```bash
touch commands/custom/your-command.md
```

add personas:
```bash
touch commands/roles/your-persona.md
```

commands adapt to available tools and degrade gracefully when dependencies are missing.

## license

MIT
