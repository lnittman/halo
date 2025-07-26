# Claude System Design: Commands, Roles, and Agents

A cohesive system where modular commands serve as building blocks that can be orchestrated by agents, roles, or direct human control.

## Core Philosophy

**Commands are tools. Agents are specialists. Roles are personas.**

The system achieves high cohesion without bloat through clear separation of concerns and intelligent orchestration.

## Architecture Layers

### 1. Commands (`/commands/`) - The Tools
**Purpose**: Modular, reusable actions that anyone can invoke

Commands are the foundational building blocks:
- **Focused**: Each does one thing well
- **Composable**: Can be chained together
- **Context-aware**: Work within conversation flow
- **Direct**: No intermediary needed

Examples:
- `/user:build` - Implementation execution
- `/user:create` - Project scaffolding
- `/user:vision` - Creative exploration
- `/user:design` - Design system work
- `/user:audit` - Quality checking

### 2. Roles (`/roles/`) - The Personas
**Purpose**: Personalities and philosophies that inform decision-making

Roles are character definitions:
- **People**: Real or fictional individuals with distinct approaches
- **Philosophies**: Ways of thinking and creating
- **Perspectives**: Lenses through which to view problems

Examples:
- `dieter-rams.md` - Minimalist design philosophy
- `jony-ive.md` - Obsessive craft and detail
- `teenage-engineering.md` - Playful innovation
- `design-system-engineer.md` - Technical design expertise

### 3. Agents (`/agents/`) - The Specialists
**Purpose**: Task-focused workers that orchestrate commands and channel roles

Agents are verb-based specialists:
- **Action-oriented**: Named after what they do
- **Isolated context**: Don't pollute main conversation
- **Tool access**: Can use specific tools including commands
- **Role channeling**: Can embody personalities from `/roles/`

Examples:
- `recreate-design` - Browse and recreate UIs
- `build-anything` - Rapid prototyping
- `simplify-design` - Radical reduction
- `polish-interface` - Add final touches
- `envision-product` - Product strategy
- `audit-codebase` - Quality analysis

## System Cohesion Patterns

### 1. Agents Using Commands
```markdown
# In envision-product agent
You leverage commands:
- /user:vision for exploration
- /user:brand for identity
- /user:design for systems
```

### 2. Agents Channeling Roles
```markdown
# In simplify-design agent
You channel wisdom from:
- @roles/dieter-rams.md for principles
- @roles/jony-ive.md for craft
```

### 3. Commands Remaining Pure
Commands don't need to know about agents or roles. They:
- Accept input
- Process it
- Return output
- Stay modular

### 4. Human Orchestration
Users can:
- Call commands directly: `/user:build feature`
- Invoke agents: "Use build-anything agent"
- Mix approaches: Command → Agent → Command

## Delegation Intelligence

### When Claude Chooses Agents

**Verb indicators** trigger agents:
- "recreate this" → `recreate-design`
- "simplify this" → `simplify-design`
- "polish this" → `polish-interface`
- "audit this" → `audit-codebase`
- "envision X" → `envision-product`

**Context indicators** guide selection:
- Seeing a URL → `recreate-design`
- Code review needed → `audit-codebase`
- UI feels rough → `polish-interface`
- Too complex → `simplify-design`

### Agent Collaboration Patterns

Agents can work together:
1. `recreate-design` → `simplify-design` → `polish-interface`
2. `envision-product` → `build-anything` → `audit-codebase`
3. `audit-codebase` → `simplify-design` → `build-anything`

## Benefits of This Design

### 1. Modularity
- Commands work independently
- Agents compose capabilities
- Roles provide consistency

### 2. Flexibility
- Multiple ways to achieve goals
- Mix automated and manual control
- Adapt to user preferences

### 3. Clarity
- Verb-based agents (what they do)
- Person-based roles (how they think)
- Action-based commands (what happens)

### 4. Scalability
- Easy to add new commands
- Simple to create new agents
- Natural to add new roles

## Best Practices

### For Commands
- Keep focused on single responsibility
- Don't assume context beyond input
- Return clear, actionable output
- Document usage patterns

### For Roles
- Define clear philosophy
- Include concrete examples
- Show how thinking applies
- Maintain consistent voice

### For Agents
- Name with action verbs
- Clear description for delegation
- List specific tools needed
- Reference commands and roles

### For Users
- Start with commands for control
- Use agents for specialized work
- Mix approaches as needed
- Let context guide choices

## The Magic: Emergent Behavior

The true power comes from combination:
- Human creativity directing
- Agents specializing
- Commands executing
- Roles inspiring

Together, they create a system that's both powerful and intuitive, structured yet flexible, automated yet controllable.

## Remember

"The best system is invisible. Users think about what they want to achieve, not how the system works."

Commands, roles, and agents work together seamlessly, each playing their part in helping users create amazing things.