# 🏛️ external:codex:architect - gpt-5 system architecture & design

leverage codex's gpt-5 reasoning for strategic architecture decisions and system design.

<codex_architect_directive>
you orchestrate codex cli for architectural planning, system design, and strategic technical decisions. use gpt-5's deep reasoning capabilities.

<components>
  <use>@file:~/.halo/components/thinking-blocks.md</use>
  <use>@file:~/.halo/components/verification-patterns.md</use>
  <use>@file:~/.halo/components/output-standards.md</use>
</components>

<architecture_capabilities>
## strategic architecture focus

- system design decisions
- architectural patterns selection
- technology stack evaluation
- scalability planning
- migration strategies
- microservices design
- api architecture
- data modeling
</architecture_capabilities>

<execution_workflow>
## actual execution with bash tool

when executing, you MUST:

1. **verify codex installation**
```bash
which codex || npm install -g @openai/codex
```

2. **prepare architecture context**
```bash
# gather current architecture info
find . -name "*.config.*" -o -name "*.json" | grep -E "(package|tsconfig|webpack)" > config-files.txt

# create architecture prompt
cat > .codex-architect-prompt.txt << 'EOF'
# GPT-5 STRATEGIC ARCHITECTURE DESIGN

Think deeply and reason step-by-step about the architectural requirements and provide comprehensive system design.

## Architecture Requirements
$ARGUMENTS

## Design Considerations

### 1. System Architecture Analysis
- **Current State Assessment**
  - Existing architecture patterns
  - Technology stack evaluation
  - Scalability limitations
  - Performance bottlenecks
  - Security vulnerabilities

- **Future State Design**
  - Target architecture patterns
  - Technology recommendations
  - Scalability solutions
  - Performance optimizations
  - Security enhancements

### 2. Architectural Decisions
- **Pattern Selection**
  - Evaluate applicable patterns
  - Compare trade-offs
  - Justify selections
  - Migration path

- **Technology Stack**
  - Framework choices
  - Database selection
  - Caching strategy
  - Message queue needs
  - API design (REST/GraphQL/gRPC)

### 3. System Design Components
- **Service Architecture**
  - Service boundaries
  - Communication patterns
  - Data ownership
  - Transaction management
  - Event sourcing needs

- **Data Architecture**
  - Data models
  - Storage strategies
  - Consistency requirements
  - Partitioning strategy
  - Backup/recovery

### 4. Scalability & Performance
- **Scaling Strategy**
  - Horizontal vs vertical
  - Auto-scaling triggers
  - Load balancing
  - Caching layers
  - CDN strategy

- **Performance Optimization**
  - Query optimization
  - Caching strategy
  - Async processing
  - Resource pooling
  - Connection management

### 5. Security Architecture
- **Security Layers**
  - Authentication design
  - Authorization model
  - Data encryption
  - API security
  - Network security

- **Compliance & Governance**
  - Regulatory requirements
  - Data privacy
  - Audit logging
  - Disaster recovery
  - Business continuity

## Output Format

### Executive Summary
- Architecture vision
- Key decisions
- Risk assessment
- Implementation timeline

### Detailed Architecture Design

#### System Architecture
[Component diagrams and descriptions]

#### Data Architecture
[Data models and flow diagrams]

#### API Architecture
[API design and specifications]

#### Security Architecture
[Security layers and controls]

#### Deployment Architecture
[Infrastructure and deployment strategy]

### Implementation Roadmap
1. Phase 1: [Foundation]
2. Phase 2: [Core Services]
3. Phase 3: [Integration]
4. Phase 4: [Optimization]
5. Phase 5: [Scale]

### Architecture Decision Records (ADRs)
[Key decisions with rationale]

### Risk Mitigation Plan
[Identified risks and mitigation strategies]

### Success Metrics
[KPIs and monitoring strategy]

## Additional Context
- Team size and expertise
- Budget constraints
- Timeline requirements
- Compliance needs
- Performance SLAs
EOF
```

3. **execute codex architect**
```bash
# use gpt-5 for deep architectural reasoning
codex exec -m gpt-5 -s read-only "$(cat .codex-architect-prompt.txt)" 2>&1 | tee architecture-design.md
```

4. **process architecture outputs**
```bash
# extract key decisions
grep -A 20 "Key decisions" architecture-design.md > key-decisions.md

# extract roadmap
grep -A 50 "Implementation Roadmap" architecture-design.md > roadmap.md

# extract ADRs
grep -A 30 "Architecture Decision Records" architecture-design.md > adrs.md

# show summary
echo "=== ARCHITECTURE SUMMARY ==="
head -100 architecture-design.md
```
</execution_workflow>

<specialized_architecture>
## architecture patterns

### microservices design
```bash
codex -m gpt-5 "Think deeply: Design microservices architecture for $SYSTEM"
```

### api architecture
```bash
codex -m gpt-5 "Think deeply: Design RESTful API architecture with versioning, rate limiting, and security"
```

### event-driven architecture
```bash
codex -m gpt-5 "Think deeply: Design event-driven architecture with event sourcing and CQRS"
```

### migration planning
```bash
codex -m gpt-5 "Think deeply: Plan migration from monolith to microservices"
```
</specialized_architecture>

<integration_patterns>
## workflow integration

### architecture pipeline
```bash
# 1. Analyze current state
/external:gemini:analyze architecture

# 2. Design target architecture
/external:codex:architect system design

# 3. Plan implementation
/external:codex:plan migration strategy

# 4. Build components
/external:cursor-agent:build services
```

### continuous architecture
```bash
# architecture evolution
/external:codex:architect review quarterly
/external:gemini:audit architecture
/external:codex:architect optimize
/fix architectural issues
```
</integration_patterns>

<best_practices>
## optimal usage

### when to use codex:architect
- system design decisions
- architecture reviews
- technology selection
- migration planning
- scalability design
- security architecture

### reasoning optimization
- provide context and constraints
- specify quality attributes
- define success criteria
- request trade-off analysis
- ask for alternatives
</best_practices>

<output_format>
## 🏛️ architecture design

**system**: {{system_name}}  
**pattern**: {{architecture_pattern}}  
**complexity**: {{complexity_level}}  

### 📐 design decisions

key patterns:
{{pattern_list}}

technology stack:
{{tech_stack}}

### 🎯 architecture goals

- scalability: {{scalability_approach}}
- performance: {{performance_targets}}
- security: {{security_measures}}
- maintainability: {{maintainability_score}}

### 📋 implementation roadmap

{{roadmap_phases}}

### 💡 recommendations

{{key_recommendations}}

### 🚀 next steps

{{next_actions}}

---
✨ full architecture design: `architecture-design.md`
</output_format>

$ARGUMENTS</codex_architect_directive>