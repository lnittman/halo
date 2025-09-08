# /init-docs

Initialize a standardized, tech-agnostic documentation structure for capturing product philosophy and vision.

## Command Pattern
```
/init-docs
```

## What It Does

Sets up a `docs/` folder with:
- Role-based directory structure (vision, design, product, architecture, intelligence)
- XML metaprompt templates (AGENTS.md) in each subdirectory
- Project-agnostic documentation framework
- Clear separation between philosophy (docs/) and implementation (code)

## Directory Structure Created

```
docs/
├── vision/              # Strategic direction (CEO mindset)
│   ├── AGENTS.md       # XML metaprompt for vision docs
│   └── *.md            # Your product manifesto, beliefs, philosophy
│
├── development/         # Building guidance
│   ├── design/         # Design philosophy (Rauno/Dieter Rams inspired)
│   │   ├── AGENTS.md   # XML metaprompt for design docs
│   │   └── *.md        # Design principles, influences, system
│   │
│   ├── product/        # Product thinking
│   │   ├── AGENTS.md   # XML metaprompt for product docs
│   │   └── *.md        # Features, user stories, workflows
│   │
│   ├── architecture/   # System design (senior architect mindset)
│   │   ├── AGENTS.md   # XML metaprompt for architecture docs
│   │   └── *.md        # Patterns, data flow, system design
│   │
│   └── intelligence/   # AI/ML approach
│       ├── AGENTS.md   # XML metaprompt for AI docs
│       └── *.md        # AI features, agents, workflows
│
├── AGENTS.md           # Root metaprompt explaining the system
├── CLAUDE.md           # Symlink to AGENTS.md for AI tool compatibility
├── README.md           # Documentation index
└── glossary.md         # Domain terminology
```

## Core Principles

1. **Tech-Agnostic**: Never mention specific frameworks, versions, or implementation details
2. **Philosophy Over Implementation**: Focus on the "why" and "what", never the "how"
3. **Timeless**: Should remain valid even if you completely change your tech stack
4. **Portable**: Can be copied to any project and remain useful
5. **Role-Based**: Each subdirectory maps to a specific role/mindset

## AGENTS.md System

Each subdirectory contains an XML-formatted metaprompt. CLAUDE.md files are symlinks to AGENTS.md for compatibility with AI tools that look for CLAUDE.md:

```xml
<agent role="[role-name]">
  <context>
    <!-- Role-specific context and mindset -->
  </context>
  <instructions>
    <!-- How to generate docs for this domain -->
  </instructions>
  <style>
    <!-- Writing style and tone guidelines -->
  </style>
  <examples>
    <!-- Example patterns or references -->
  </examples>
</agent>
```

## Content Guidelines

### ✅ What BELONGS in docs/:
- Product vision and philosophy
- Design principles and beliefs
- User personas and journeys
- Conceptual architecture patterns
- AI/ML strategies and approaches
- Domain glossary and concepts

### ❌ What DOESN'T belong in docs/:
- API documentation
- Code examples
- Framework guides
- Deployment instructions
- Version numbers
- Package names
- Technical HOWTOs

## The Litmus Test

Ask yourself: **"If I switched from Next.js to SvelteKit, from Convex to Supabase, from React to Vue - would these docs still be 100% valid?"**

- If **yes** → It belongs in docs/
- If **no** → It belongs in technical documentation outside of docs/

## Implementation Steps

When you run `/init-docs`, I will:

1. **Check for existing docs/** - Warn if it exists
2. **Create directory structure** - All subdirectories with proper organization
3. **Create AGENTS.md templates** with XML metaprompts for each role
4. **Create CLAUDE.md symlinks** to AGENTS.md in each directory
5. **Initialize base files** - README.md, glossary.md
5. **Provide next steps** - Guide you on how to start documenting

## Usage Examples

### Starting a new project:
```
/init-docs
# Creates full structure
# Write vision/manifesto.md first
# Use AGENTS.md prompts to generate domain docs
```

### Migrating existing docs:
```
/init-docs
# Move technical docs to README files
# Extract philosophy into docs/
# Keep implementation details outside of docs/
```

## Post-Initialization Workflow

1. **Vision First**: Start with `vision/manifesto.md` - your north star
2. **Design Philosophy**: Document your design principles in `development/design/`
3. **Product Features**: Describe features conceptually in `development/product/`
4. **Architecture Patterns**: Outline system design in `development/architecture/`
5. **AI Strategy**: Define AI/ML approach in `development/intelligence/`

## Related Commands

- `/prime` - Initialize full project context including docs
- `/docs` - Generate documentation for existing code
- `/diagram` - Create visual architecture diagrams

## Notes

- This structure is based on successful patterns from turbokit
- Each AGENTS.md contains world-class metaprompts inspired by industry leaders
- The structure intentionally avoids technical implementation details
- Perfect for projects that may pivot technology but maintain product vision

---

*Initialize your documentation to capture timeless product philosophy, not temporary technical choices.*