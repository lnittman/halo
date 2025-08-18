# 🔮 external:codex:main - intelligent gpt-5 reasoning

leverage codex's deep reasoning capabilities for any task requiring strategic thinking, research, or complex problem solving. intelligently determine how to use codex based on the prompt.

<codex_main_directive>
you orchestrate codex cli intelligently based on the user's prompt. analyze what they need and configure codex appropriately with gpt-5. codex excels at strategic planning, debugging, and deep technical reasoning.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<cli_documentation>
## codex cli usage patterns

### installation
```bash
# check if installed
which codex || {
  # install via npm (preferred)
  npm install -g @openai/codex
  # or via homebrew
  brew install codex
}
```

### authentication methods
```bash
# option 1: chatgpt plan (plus, pro, team)
codex login

# option 2: openai api key
export OPENAI_API_KEY="your-api-key"
```

### approval modes
- **suggest** (default): reads files, proposes changes, requires approval
- **auto-edit**: reads and writes files automatically, asks before commands
- **full-auto**: autonomous operation with sandboxing

### key arguments
- `-m, --model`: ALWAYS USE GPT-5 for deep reasoning and analysis
- `--auto-edit`: enable automatic file editing
- `--full-auto`: enable full autonomous mode
- `--sandbox`: control sandbox level (read-only, workspace-write, danger-full-access)
- `--ask-for-approval`: approval policy (never, on-request, untrusted)
- `--profile`: use predefined configuration profile

### multimodal capabilities
- accepts text prompts
- processes screenshots and images
- analyzes diagrams and visual content
- generates code from visual mockups
</cli_documentation>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **check codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **prepare strategic prompt**
```bash
cat > .codex-prompt.txt << 'EOF'
[Your research/debugging task here]
EOF
```

3. **execute with appropriate mode**
```bash
# for research and exploration (safe mode) - ALWAYS USE GPT-5
codex -m gpt-5 --sandbox read-only "Think deeply and reason step-by-step: $(cat .codex-prompt.txt)"

# for implementation planning (with file writes)
codex -m gpt-5 --auto-edit "Think deeply and reason step-by-step: $(cat .codex-prompt.txt)"

# for autonomous execution (sandboxed)
codex -m gpt-5 --full-auto --sandbox workspace-write "Think deeply and reason step-by-step: $(cat .codex-prompt.txt)"
```

4. **non-interactive execution for ci/cd**
```bash
codex exec -m gpt-5 -s read-only "Think deeply: analyze architecture patterns"
```
</execution_workflow>

<prompt_templates>
## gpt-5 research prompts

### architectural research
```markdown
# ARCHITECTURAL RESEARCH TASK

## Research Objective
[Specific architectural problem to investigate]

## Context
- Current architecture: [Brief description]
- Pain points: [Current issues]
- Constraints: [Technical/business constraints]

## Research Requirements
1. **Pattern Analysis**
   - Identify applicable design patterns
   - Compare alternative approaches
   - Evaluate trade-offs

2. **Implementation Strategy**
   - Step-by-step migration path
   - Risk assessment
   - Resource requirements

3. **Best Practices**
   - Industry standards
   - Similar successful implementations
   - Common pitfalls to avoid

## Deliverables
- Architectural decision record (ADR)
- Implementation roadmap
- Risk mitigation strategies
- Proof of concept code
```

### debugging investigation
```markdown
# DEBUGGING INVESTIGATION

## Issue Description
[Detailed description of the problem]

## Symptoms
- Error messages: [Include full stack traces]
- Reproduction steps: [How to trigger the issue]
- Environment: [OS, versions, dependencies]

## Investigation Strategy
1. **Root Cause Analysis**
   - Trace execution flow
   - Identify failure points
   - Analyze state at failure

2. **Hypothesis Testing**
   - List potential causes
   - Design tests to validate
   - Isolate variables

3. **Solution Development**
   - Minimal fix approach
   - Long-term solution
   - Prevention strategies

## Success Criteria
- [ ] Issue reproduced consistently
- [ ] Root cause identified
- [ ] Fix implemented and tested
- [ ] Regression prevention added
```

### strategic planning
```markdown
# STRATEGIC PLANNING TASK

## Planning Objective
[High-level goal or initiative]

## Current State Analysis
- Existing capabilities: [What we have]
- Gaps: [What we need]
- Resources: [Available assets]

## Strategic Requirements
1. **Technical Roadmap**
   - Milestone definition
   - Dependency mapping
   - Technology choices

2. **Risk Analysis**
   - Technical risks
   - Business risks
   - Mitigation strategies

3. **Implementation Plan**
   - Phase breakdown
   - Resource allocation
   - Success metrics

## Outputs
- Executive summary
- Detailed technical plan
- Risk register
- Success KPIs
```

### performance optimization
```markdown
# PERFORMANCE OPTIMIZATION RESEARCH

## Optimization Target
[System/component to optimize]

## Current Performance
- Metrics: [Current measurements]
- Bottlenecks: [Known issues]
- SLAs: [Requirements to meet]

## Analysis Approach
1. **Profiling**
   - CPU usage patterns
   - Memory allocation
   - I/O operations
   - Network latency

2. **Optimization Strategies**
   - Algorithm improvements
   - Caching strategies
   - Parallel processing
   - Resource pooling

3. **Validation**
   - Benchmark design
   - A/B testing approach
   - Rollback strategy

## Expected Outcomes
- Performance improvements: [Target metrics]
- Trade-offs: [What we sacrifice]
- Implementation complexity: [Effort estimate]
```
</prompt_templates>

<best_practices>
## codex cli best practices

### approval mode selection
- use `--sandbox read-only` for research and analysis
- use `--auto-edit` for controlled file modifications
- use `--full-auto` only in isolated environments
- always use version control before auto modes

### prompt engineering
- provide clear success criteria
- include relevant context and constraints
- specify desired output format
- reference existing code patterns

### safety considerations
- review proposed changes before approval
- use sandboxing for untrusted operations
- maintain backups before major changes
- test in isolated environments first

### optimal use cases
- architectural decision making
- complex debugging investigations
- performance optimization research
- security vulnerability analysis
- technical debt assessment
- migration planning
- technology evaluation
</best_practices>

<execution_patterns>
## common execution patterns

### quick analysis
```bash
# code review - ALWAYS USE GPT-5
codex -m gpt-5 "Think deeply: review this codebase for architectural patterns and anti-patterns"

# security audit
codex -m gpt-5 "Think deeply: analyze for security vulnerabilities following OWASP guidelines"

# performance analysis  
codex -m gpt-5 "Think deeply: identify performance bottlenecks and optimization opportunities"
```

### strategic planning
```bash
# architecture planning
PROMPT="Design a migration strategy from monolith to microservices:
- Current: Django monolith with PostgreSQL
- Target: Kubernetes microservices
- Constraints: Zero downtime, 6-month timeline
- Team: 5 engineers"

codex -m gpt-5 --auto-edit "Think deeply: $PROMPT"
```

### debugging workflow
```bash
# complex debugging
ERROR_CONTEXT=$(cat error.log debug.log | tail -200)
codex -m gpt-5 "Think deeply: Debug this production issue: $ERROR_CONTEXT"

# root cause analysis
codex exec -m gpt-5 --full-auto "Think deeply: perform root cause analysis on the memory leak in worker.js"
```

### ci/cd integration
```bash
# automated pr review
codex exec -m gpt-5 -s read-only \
  "Think deeply: review pr changes and suggest improvements"

# test generation
codex exec -m gpt-5 --auto-edit "Think deeply: generate comprehensive tests for new features"
```
</execution_patterns>

<integration_notes>
## integration with halo system

### workflow coordination
```bash
# after gemini analysis
codex "based on the security audit in audit.md, create a remediation plan"

# before cursor-agent build
codex "research best practices for implementing oauth2 with pkce"

# architecture decisions
codex "evaluate tradeoffs between graphql and rest for our api redesign"
```

### agent handoffs
- use codex for strategic planning → cursor-agent for implementation
- use gemini for analysis → codex for solution design
- use codex for debugging → cursor-agent for fixes

### output formats
- codex provides markdown documentation
- generates architectural decision records
- creates implementation roadmaps
- produces debugging reports
</integration_notes>

<advanced_features>
## advanced codex features

### multimodal inputs
```bash
# from screenshot
codex "implement this ui design" --attach screenshot.png

# from diagram
codex "generate database schema from this erd" --attach erd.pdf
```

### configuration profiles
```bash
# create profiles in ~/.codex/config.toml
[profiles.research]
approval_policy = "never"
sandbox_mode = "read-only"
model = "gpt-5"

[profiles.debug]
approval_policy = "on-request"
sandbox_mode = "workspace-write"
model = "gpt-5"  # Always use GPT-5 for best results

# use profiles
codex --profile research "analyze codebase"
codex --profile debug "fix production issue"
```

### model selection
```bash
# ALWAYS use gpt-5 for ALL tasks - deep reasoning is crucial
codex -m gpt-5 "Think deeply: design distributed system architecture"

# Even for simple tasks, use gpt-5 for quality
codex -m gpt-5 "Think deeply: explain this regex pattern"

# Always prioritize quality over cost
codex -m gpt-5 "Think deeply: write comprehensive unit tests"
```
</advanced_features>

<usage_examples>
## example invocations

### research tasks
```
/external:codex research microservices patterns for our use case
```

### debugging
```
/external:codex debug the race condition in the payment processor
```

### architecture planning
```
/external:codex design event-driven architecture for real-time features
```

### optimization
```
/external:codex optimize database queries for 10x scale
```

### security analysis
```
/external:codex perform threat modeling for the authentication system
```
</usage_examples>

$ARGUMENTS</codex_directive>