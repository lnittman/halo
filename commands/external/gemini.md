# external:gemini - 2M context analysis orchestrator

intelligently leverage gemini cli's massive context window based on user intent. automatically uses repomix for comprehensive codebase understanding.

<gemini_directive>
you orchestrate gemini cli based on the user's prompt. analyze intent and configure gemini + repomix appropriately. gemini excels at tasks requiring full codebase awareness with its 2M token context.

<components>
  <use>@file:../../components/thinking-blocks.md</use>
  <use>@file:../../components/repomix-context.md</use>
  <use>@file:../../components/output-standards.md</use>
</components>

<intent_detection>
analyze $ARGUMENTS to determine task type:
- **audit** → security/quality audit with full codebase
- **analyze** → pattern extraction and architecture analysis  
- **prime** → comprehensive initialization with all context
- **review** → code review with entire project awareness
- **document** → generate docs understanding full structure
</intent_detection>

<execution_workflow>
## actual execution with bash tool

1. **verify gemini installation**
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

2. **gather context with repomix**
```bash
# use repomix component for smart context gathering
npx repomix --include '**/*.{ts,tsx,js,jsx,md,json}' \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --ignore 'build/**' \
  -o .repomix-context.md

# check token count
TOKEN_COUNT=$(($(wc -c < .repomix-context.md) / 4))
echo "Context size: ~$TOKEN_COUNT tokens"
```

3. **prepare task-specific prompt**
```bash
cat > .gemini-prompt.txt << 'EOF'
# COMPREHENSIVE ANALYSIS TASK

$ARGUMENTS

## Context
[Full codebase provided via repomix - $(wc -l < .repomix-context.md) lines]

## Requirements
- Analyze the entire codebase holistically
- Identify patterns, issues, and opportunities
- Provide actionable insights and recommendations
- Consider all interdependencies
EOF
```

4. **execute with gemini's 2M context**
```bash
# pipe repomix context + prompt to gemini
cat .repomix-context.md .gemini-prompt.txt | gemini

# cleanup
rm -f .repomix-context.md .gemini-prompt.txt
```
</execution_workflow>

<task_templates>
## security audit
```markdown
Perform comprehensive security audit:
- Identify vulnerabilities (OWASP Top 10)
- Check for exposed secrets/credentials
- Analyze authentication/authorization
- Review data validation and sanitization
- Assess dependency vulnerabilities
```

## architecture analysis
```markdown
Analyze architecture and patterns:
- Identify design patterns in use
- Detect anti-patterns and code smells
- Map component dependencies
- Assess modularity and coupling
- Suggest architectural improvements
```

## codebase prime
```markdown
Initialize comprehensive understanding:
- Map project structure and organization
- Identify key components and their roles
- Understand data flow and state management
- Document conventions and patterns
- Highlight areas needing attention
```
</task_templates>

<best_practices>
## gemini optimization
- always use repomix for full context
- leverage 2M tokens for holistic analysis
- focus on cross-cutting concerns
- provide actionable recommendations
- use gemini for analysis, not implementation
</best_practices>

$ARGUMENTS</gemini_directive>
