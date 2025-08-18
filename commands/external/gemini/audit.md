# 🔍 external:gemini:audit - comprehensive security & architecture audit

leverage gemini's 2m context for exhaustive security and architecture auditing with repomix.

<gemini_audit_directive>
you orchestrate gemini cli for deep security audits and architecture reviews. use repomix to gather complete codebase context for thorough vulnerability analysis.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
  <use>@file:~/.halo/components/repomix-context.md</use>
</components>

<audit_scope>
## comprehensive audit coverage

### security analysis
- authentication & authorization flaws
- injection vulnerabilities (sql, xss, etc.)
- sensitive data exposure
- broken access control
- security misconfiguration
- vulnerable dependencies
- api security issues

### architecture review
- design pattern violations
- architectural anti-patterns
- coupling and cohesion issues
- scalability bottlenecks
- maintainability concerns
- technical debt accumulation
</audit_scope>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify gemini installation**
```bash
which gemini || npm install -g @google-gemini/gemini-cli
```

2. **gather complete codebase**
```bash
npx repomix \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --output-file .audit-context.md
```

3. **create comprehensive audit prompt**
```bash
cat > .gemini-audit-prompt.md << 'EOF'
# COMPREHENSIVE SECURITY & ARCHITECTURE AUDIT

Think deeply and perform exhaustive analysis of this codebase for security vulnerabilities and architectural issues.

## Security Audit Requirements

### 1. Authentication & Authorization
- Analyze all auth mechanisms
- Check for privilege escalation paths
- Review session management
- Validate token handling
- Inspect access control lists

### 2. Input Validation & Sanitization
- SQL injection vulnerabilities
- XSS attack vectors
- Command injection risks
- Path traversal possibilities
- XXE vulnerabilities

### 3. Data Protection
- Sensitive data in code
- Encryption implementation
- Secrets management
- PII handling
- Data leakage points

### 4. Dependencies & Supply Chain
- Vulnerable package versions
- Outdated dependencies
- License compliance
- Dependency confusion risks
- Typosquatting protection

### 5. API Security
- Broken object level authorization
- Excessive data exposure
- Rate limiting gaps
- Mass assignment vulnerabilities
- Security misconfiguration

## Architecture Audit Requirements

### 1. Design Patterns
- Identify pattern violations
- Detect anti-patterns
- Review SOLID compliance
- Check DRY violations
- Assess abstraction levels

### 2. System Design
- Component coupling analysis
- Cohesion evaluation
- Boundary definitions
- Interface segregation
- Dependency management

### 3. Performance & Scalability
- N+1 query problems
- Memory leak potential
- Inefficient algorithms
- Resource bottlenecks
- Caching opportunities

### 4. Maintainability
- Code complexity metrics
- Documentation coverage
- Test coverage gaps
- Refactoring needs
- Technical debt items

## Output Format

### Critical Security Issues
[List with severity, impact, and remediation]

### Architecture Violations
[Pattern violations with recommendations]

### Risk Matrix
[Security and architecture risks by severity]

### Remediation Roadmap
[Prioritized fixes with effort estimates]

### Quick Wins
[Immediate improvements with high impact]

## Context
$(cat .audit-context.md)
EOF
```

4. **execute gemini audit**
```bash
cat .gemini-audit-prompt.md | gemini > audit-report.md 2>&1
```

5. **generate actionable outputs**
```bash
# extract critical issues
grep -A 20 "Critical Security Issues" audit-report.md > critical-issues.md

# create remediation checklist
grep -A 30 "Remediation Roadmap" audit-report.md > remediation-plan.md

# display summary
echo "=== AUDIT SUMMARY ===" 
head -50 audit-report.md
```
</execution_workflow>

<specialized_prompts>
## security-specific prompts

### owasp top 10 check
```markdown
Analyze against OWASP Top 10:
- A01: Broken Access Control
- A02: Cryptographic Failures
- A03: Injection
- A04: Insecure Design
- A05: Security Misconfiguration
- A06: Vulnerable Components
- A07: Authentication Failures
- A08: Data Integrity Failures
- A09: Logging Failures
- A10: SSRF
```

### compliance verification
```markdown
Check compliance with:
- GDPR data protection
- SOC 2 requirements
- PCI DSS standards
- HIPAA regulations (if applicable)
```
</specialized_prompts>

<integration_patterns>
## workflow integration

### after audit
```bash
# generate fixes
/external:cursor-agent:fix critical-issues.md

# plan remediation
/external:codex:plan remediation strategy

# implement security
/build security improvements
```

### continuous auditing
```bash
# daily security check
/external:gemini:audit --focus security

# weekly architecture review  
/external:gemini:audit --focus architecture

# pre-deployment audit
/external:gemini:audit --comprehensive
```
</integration_patterns>

<output_format>
## 🔍 security & architecture audit

**scope**: full codebase audit  
**files analyzed**: {{file_count}}  
**vulnerabilities found**: {{vuln_count}}  
**architecture issues**: {{arch_count}}  

### 🚨 critical findings

security:
{{critical_security_issues}}

architecture:
{{critical_arch_issues}}

### 📊 risk assessment

- high severity: {{high_count}}
- medium severity: {{medium_count}}
- low severity: {{low_count}}

### 🎯 immediate actions

1. {{top_priority_1}}
2. {{top_priority_2}}
3. {{top_priority_3}}

### 💡 recommendations

quick wins:
{{quick_wins}}

strategic improvements:
{{strategic_items}}

---
✨ full audit report: `audit-report.md`
</output_format>

$ARGUMENTS</gemini_audit_directive>