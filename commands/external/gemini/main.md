# 🔷 external:gemini:main - intelligent analysis with 2M context

leverage gemini cli's massive context window for any task requiring comprehensive codebase understanding. intelligently determine how to use gemini based on the prompt.

<gemini_main_directive>
you orchestrate gemini cli intelligently based on the user's prompt. analyze what they need and configure gemini + repomix appropriately. gemini excels at tasks requiring full codebase awareness.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
  <use>@file:~/.halo/components/repomix-context.md</use>
</components>

<cli_documentation>
## gemini cli usage patterns

### installation check
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

### invocation methods
- **piping**: `echo "prompt" | gemini`
- **file input**: `cat file.md | gemini`
- **prompt flag**: `gemini -p "prompt"` (avoid for large prompts)
- **interactive**: `gemini -i "initial prompt"`

### key arguments
- `-p, --prompt`: direct prompt (use piping for large prompts)
- `-i, --prompt-interactive`: start interactive session
- `-s, --sandbox`: enable sandbox mode
- `-d, --debug`: debug mode
- `-a, --all-files`: include all files in context
- `--yolo`: auto-approve all actions
- `--include-directories`: add additional directories

### limitations
- command-line argument length limits (~128KB)
- use piping or stdin for large prompts
- binary files handled via base64 encoding
</cli_documentation>

<repomix_integration>
## repomix workflow for gemini

### 1. gather context with repomix
```bash
# basic repomix command
npx repomix \
  --ignore 'node_modules/**,.git/**,dist/**,build/**,*.log' \
  -o .gemini-context.md

# check context size
CONTEXT_SIZE=$(wc -c < .gemini-context.md)
echo "Context: $((CONTEXT_SIZE / 1024))KB (~$((CONTEXT_SIZE / 4)) tokens)"
```

### 2. prepare structured prompt
```bash
cat > .gemini-prompt.md << 'EOF'
# ANALYSIS REQUEST

[Your analysis instructions here]

## Codebase Context
The full codebase follows below:

---
EOF

# append repomix context
cat .gemini-context.md >> .gemini-prompt.md
```

### 3. execute gemini with piping
```bash
# pipe prompt to avoid argument length limits
cat .gemini-prompt.md | gemini > analysis-output.md 2>&1

# alternative for interactive exploration
cat .gemini-prompt.md | gemini -i
```

### 4. cleanup
```bash
rm -f .gemini-context.md .gemini-prompt.md
```
</repomix_integration>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **check gemini installation**
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

2. **run repomix to gather context**
```bash
npx repomix \
  --ignore 'node_modules/**,.git/**,dist/**,build/**,*.log' \
  -o .gemini-context.md
```

3. **create comprehensive prompt file**
```bash
cat > .gemini-prompt.md << 'EOF'
[Full analysis prompt with structure]
EOF
cat .gemini-context.md >> .gemini-prompt.md
```

4. **pipe to gemini (not -p flag)**
```bash
cat .gemini-prompt.md | gemini > output.md 2>&1
```

5. **verify output and cleanup**
```bash
if [ -f output.md ]; then
  echo "✅ Analysis complete: $(wc -l output.md | awk '{print $1}') lines"
  cat output.md
fi
rm -f .gemini-context.md .gemini-prompt.md
```
</execution_workflow>

<prompt_templates>
## world-class analysis prompts

### comprehensive codebase analysis
```markdown
# COMPREHENSIVE CODEBASE ANALYSIS

## Analysis Mission
Provide a world-class technical analysis covering architecture, code quality, security, and strategic opportunities.

## Required Components

1. **Architecture Assessment**
   - Design patterns and principles
   - Component relationships
   - Data flow analysis
   - Integration points

2. **Code Quality Review**
   - Consistency and maintainability
   - Best practices adherence
   - Technical debt assessment
   - Refactoring opportunities

3. **Security Audit**
   - Vulnerability assessment
   - OWASP compliance
   - Sensitive data handling
   - Authentication/authorization

4. **Performance Analysis**
   - Bottlenecks and optimizations
   - Resource usage patterns
   - Scalability considerations

5. **Strategic Recommendations**
   - Prioritized improvements
   - Implementation roadmap
   - Risk/benefit analysis

## Output Format
Provide structured markdown with:
- Executive Summary (2-3 paragraphs)
- Critical Issues (with fixes)
- Detailed Findings (by category)
- Actionable Recommendations
- Technical Appendix

Be specific with file paths and line numbers.
```

### security-focused audit
```markdown
# SECURITY AUDIT REQUEST

Perform a comprehensive security analysis covering:

1. **Vulnerability Assessment**
   - SQL injection risks
   - XSS vulnerabilities
   - CSRF protection
   - Authentication flaws

2. **Dependency Analysis**
   - Known CVEs in dependencies
   - Outdated packages
   - Supply chain risks

3. **Data Protection**
   - Encryption practices
   - PII handling
   - Secret management

4. **Access Control**
   - Authorization mechanisms
   - Role-based access
   - API security

Provide specific vulnerabilities with:
- Severity rating
- Affected files/lines
- Exploitation scenario
- Remediation steps
```
</prompt_templates>

<best_practices>
## gemini cli best practices

### context management
- always use repomix for full codebase context
- monitor token count (aim for <500k tokens)
- use tree command for structure overview
- include relevant documentation files

### prompt engineering
- structure prompts with clear sections
- specify desired output format
- request specific file/line references
- include success criteria

### error handling
- check for gemini installation first
- verify repomix output before proceeding
- handle timeout scenarios (60s default)
- save output to file for persistence

### performance optimization
- use piping instead of -p flag for large prompts
- clean up temporary files after execution
- consider chunking very large codebases
- use --include-directories for multi-repo analysis
</best_practices>

<usage_examples>
## example invocations

### full codebase analysis
```
/external:gemini analyze the entire codebase for architecture patterns
```

### security audit
```
/external:gemini perform comprehensive security audit with OWASP checks
```

### documentation review
```
/external:gemini review documentation completeness and accuracy
```

### performance analysis
```
/external:gemini identify performance bottlenecks and optimization opportunities
```
</usage_examples>

$ARGUMENTS</gemini_directive>