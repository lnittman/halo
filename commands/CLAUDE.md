# Claude Code Commands - System Guide

This guide helps Claude Code understand and maintain the command system itself. It documents the architecture, patterns, and standards that make the command system consistent and powerful.

## System Overview

The Claude Code command system provides specialized commands that transform natural language requests into structured, executable workflows. Each command has a specific purpose and integrates seamlessly with others through shared context and standardized patterns.

### Command Directory Structure
```
.claude/
├── commands/              # Command definitions
│   ├── prime.md          # Session context initialization
│   ├── create.md         # Project creation
│   ├── build.md          # Implementation execution  
│   ├── vision.md         # Creative exploration
│   ├── design.md         # Design system creation
│   ├── brand.md          # Production readiness
│   ├── multitask.md      # Multi-agent planning
│   ├── docaudit.md       # Documentation review
│   ├── diagram.md        # Visual architecture
│   └── CLAUDE.md         # This file
├── commands/components/   # Reusable components
│   ├── thinking-blocks.md      # Structured reasoning
│   ├── xml-transformer.md      # Input transformation
│   ├── verification-patterns.md # Safety checks
│   ├── session-state.md        # State management
│   ├── planning-phases.md      # Planning patterns
│   ├── output-standards.md     # Output formatting
│   ├── interop-patterns.md     # Command integration
│   └── diagram-patterns.md     # Visualization
├── session/              # Session persistence
│   ├── current/         # Active session
│   └── archive/         # Historical sessions
└── config/              # Configuration
    └── defaults.json    # Default preferences
```

## Architecture Principles

### 1. Component-Based Architecture
Each command is composed of standardized components that ensure consistency:
- **Universal Input Handler**: Processes URLs, code, files, images
- **XML Transformer**: Converts natural language to structured format
- **Thinking Blocks**: Shows reasoning process transparently
- **Verification Patterns**: Ensures safe execution
- **Session State**: Maintains context across commands
- **Output Standards**: Consistent formatting

### 2. Session-Aware Execution
Commands share context through a persistent session:
```javascript
// Every command follows this pattern
async function executeCommand(input) {
  const session = await loadSession();
  const context = selectRelevantContext(session);
  const transformed = transformInput(input, context);
  const thinking = generateThinking(transformed);
  const verified = verifyActions(thinking);
  const result = executeWithContext(verified, session);
  await updateSession(result);
  return formatOutput(result);
}
```

### 3. Progressive Enhancement
Commands build on each other's outputs:
- `prime` → establishes context
- `vision` → explores possibilities  
- `create` → plans implementation
- `build` → executes plans
- `docaudit` → ensures quality

## Command Development Standards

### Required Sections
Every command must include these sections in order:

1. **Header**: Command name and purpose
2. **Directive**: Main instruction block
3. **Components**: List of used components
4. **Session Management**: How session is used
5. **Universal Input Handler**: Input processing
6. **XML Transformation**: Structured input parsing
7. **Thinking Process**: Reasoning display
8. **Verification Phase**: Safety checks
9. **Main Execution**: Core logic
10. **Output Format**: Standardized output
11. **Context Output**: Session update

### Component Integration Pattern
```xml
<command_structure>
  <header>
    # Command Name
    Purpose statement.
  </header>
  
  <directive>
    <components>
      <use>@session-state</use>
      <use>@xml-transformer</use>
      <use>@thinking-blocks</use>
      <use>@verification-patterns</use>
      <use>@output-standards</use>
    </components>
    
    <!-- Command-specific content -->
  </directive>
</command_structure>
```

## State Management

### Session Lifecycle
1. **Initialization**: First command creates session
2. **Accumulation**: Each command adds context
3. **Persistence**: State saved after each command
4. **Archival**: Old sessions auto-archived after 24h

### Context Selection
Commands declare what context they need:
```javascript
const contextNeeds = {
  'build': ['implementation_plan', 'project_structure', 'recent_builds'],
  'vision': ['project_context', 'design_philosophy', 'user_goals'],
  'docaudit': ['documentation_state', 'quality_metrics', 'gaps']
};
```

## Testing Standards

### Command Validation
Each command should be testable for:
- Input transformation accuracy
- Thinking process coherence
- Verification appropriateness
- Output format compliance
- Context preservation

### Integration Testing
Test command chains:
```javascript
// Test natural workflows
testWorkflow([
  { cmd: 'prime', input: 'analyze project' },
  { cmd: 'create', input: 'task tracker' },
  { cmd: 'build', input: 'implement auth' }
]);
```

## Extension Guidelines

### Adding New Commands
1. Create command file in `/commands/`
2. Include all required sections
3. Integrate standard components
4. Define interop relationships
5. Update this CLAUDE.md
6. Test with other commands

### Adding New Components
1. Create component in `/commands/components/`
2. Define clear integration points
3. Document usage patterns
4. Update existing commands if needed
5. Maintain backward compatibility

## Common Patterns

### Thinking Display Pattern
```xml
<thinking_process>
  <understanding_phase>
    What I understand: {{interpretation}}
  </understanding_phase>
  <analysis_phase>
    Options considered: {{options}}
    Selected approach: {{choice}}
  </analysis_phase>
  <planning_phase>
    Steps to take: {{plan}}
  </planning_phase>
  <thinking_summary>
    User-visible summary of thinking
  </thinking_summary>
</thinking_process>
```

### Verification Pattern
```xml
<verification_phase>
  <impact_assessment>
    What will change: {{changes}}
    Risk level: {{risk}}
  </impact_assessment>
  <user_confirmation>
    Show what will happen
    Get confirmation if needed
  </user_confirmation>
</verification_phase>
```

### Output Pattern
```markdown
## 🎯 Command: Result

### Summary
What happened

### Details
Specific information

### Next Steps
- [ ] Immediate action
- [ ] Follow-up task

### Resources
- Created: `file.ts`
- Modified: `other.ts`

---
*Session: xyz | Next: suggested command*
```

## Quality Checklist

For every command update:
- [ ] Follows standard structure
- [ ] Integrates required components
- [ ] Preserves session state
- [ ] Shows thinking process
- [ ] Verifies dangerous operations
- [ ] Formats output consistently
- [ ] Suggests logical next steps
- [ ] Updates interop relationships
- [ ] Maintains backward compatibility
- [ ] Documents changes here

## Maintenance Guidelines

### Regular Updates
- Review component usage monthly
- Update patterns based on user feedback
- Refactor common code into components
- Maintain consistent emoji usage
- Keep session storage clean

### Breaking Changes
When making breaking changes:
1. Version the change
2. Provide migration path
3. Update all affected commands
4. Test full command suite
5. Document in changelog

## Future Enhancements

### Planned Improvements
- [ ] Command aliases for common workflows
- [ ] Parallel command execution
- [ ] Richer session analytics
- [ ] Command composition syntax
- [ ] Plugin architecture
- [ ] External tool integration

### Research Areas
- Natural language command chaining
- Predictive next command suggestions
- Automated workflow optimization
- Cross-session learning
- Collaborative sessions

---

*This guide is the source of truth for Claude Code command development. Keep it updated as the system evolves.*