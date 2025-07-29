# Parallel Tasks Component

Comprehensive patterns for decomposing complex work into parallel, independent tasks that can be executed by multiple agents or in parallel tool calls within Claude Code.

## Core Parallel Execution Pattern

```xml
<parallel_task_execution>
<!-- Phase 1: Task Analysis -->
<task_decomposition>
  <complexity_assessment>
  Analyzing task complexity:
  - Total scope: {{scope_description}}
  - Estimated effort: {{effort_estimate}}
  - Parallelizable: {{yes|partial|no}}
  - Independent units: {{count}}
  </complexity_assessment>
  
  <dependency_mapping>
  Task dependencies:
  - Sequential requirements: {{must_be_done_in_order}}
  - Parallel opportunities: {{can_be_done_simultaneously}}
  - Shared resources: {{resources_that_need_coordination}}
  </dependency_mapping>
  
  <agent_boundaries>
  Natural divisions:
  - By domain: {{frontend|backend|infrastructure|data}}
  - By feature: {{auth|payments|notifications|analytics}}
  - By layer: {{ui|api|database|services}}
  - By responsibility: {{create|read|update|delete}}
  </agent_boundaries>
</task_decomposition>

<!-- Phase 2: Parallel Planning -->
<parallel_planning>
  <agent_specifications>
  {{#each agents}}
  <agent id="{{id}}" priority="{{priority}}">
    <name>{{descriptive_name}}</name>
    <mission>{{one_line_mission}}</mission>
    <scope>{{detailed_scope}}</scope>
    <dependencies>
      {{#each dependencies}}
      <depends_on agent="{{agent_id}}" type="{{hard|soft}}">
        {{what_is_needed}}
      </depends_on>
      {{/each}}
    </dependencies>
    <deliverables>
      {{#each deliverables}}
      <deliverable>{{description}}</deliverable>
      {{/each}}
    </deliverables>
    <effort>{{estimated_days}} days</effort>
  </agent>
  {{/each}}
  </agent_specifications>
  
  <execution_phases>
  <phase number="1" name="Foundation">
    <parallel_agents>{{agent_ids}}</parallel_agents>
    <duration>{{days}}</duration>
    <critical_path>{{yes|no}}</critical_path>
  </phase>
  <phase number="2" name="Core Implementation">
    <parallel_agents>{{agent_ids}}</parallel_agents>
    <duration>{{days}}</duration>
    <critical_path>{{yes|no}}</critical_path>
  </phase>
  <phase number="3" name="Integration">
    <parallel_agents>{{agent_ids}}</parallel_agents>
    <duration>{{days}}</duration>
    <critical_path>{{yes|no}}</critical_path>
  </phase>
  </execution_phases>
</parallel_planning>

<!-- Phase 3: Task Execution -->
<parallel_execution>
  <claude_parallel_tools>
  # Execute multiple tool calls simultaneously
  Task 1: {{tool_name}} - {{description}}
  Task 2: {{tool_name}} - {{description}}
  Task 3: {{tool_name}} - {{description}}
  Task 4: {{tool_name}} - {{description}}
  </claude_parallel_tools>
  
  <progress_tracking>
  Parallel execution status:
  - [ ] Task 1: {{status}} - {{progress}}%
  - [ ] Task 2: {{status}} - {{progress}}%
  - [ ] Task 3: {{status}} - {{progress}}%
  - [ ] Task 4: {{status}} - {{progress}}%
  </progress_tracking>
  
  <coordination_points>
  Synchronization needed:
  - After: {{task_groups}} complete
  - Before: {{next_phase}} begins
  - For: {{shared_resource_access}}
  </coordination_points>
</parallel_execution>

<!-- Phase 4: Results Integration -->
<results_integration>
  <merge_strategy>
  Combining parallel outputs:
  - Type: {{sequential|merged|layered}}
  - Order: {{priority_based|dependency_based|arbitrary}}
  - Conflicts: {{resolution_strategy}}
  </merge_strategy>
  
  <validation>
  Integration checks:
  - [ ] All agents completed: {{status}}
  - [ ] Interfaces align: {{status}}
  - [ ] No conflicts: {{status}}
  - [ ] Tests pass: {{status}}
  </validation>
</results_integration>
</parallel_task_execution>
```

## Multi-Agent Planning Patterns

### Agent Definition Template
```xml
<agent_template>
# Agent {{number}}: {{name}}
*"{{mission_statement}}"*

## Scope
{{clear_description_of_responsibilities}}

## Packages to modify
- `{{package_1}}` - {{what_will_be_modified}}
- `{{package_2}}` - {{what_will_be_modified}}

## Implementation Details
### Step 1: {{step_name}}
```{{language}}
{{code_example}}
```

### Step 2: {{step_name}}
{{detailed_instructions}}

## Dependencies
- Agent {{X}} must complete {{deliverable}} first
- Requires {{external_service}} to be configured

## Testing Strategy
- Unit tests: {{approach}}
- Integration tests: {{approach}}
- Validation: {{criteria}}

## Security Considerations
- {{security_concern_1}}: {{mitigation}}
- {{security_concern_2}}: {{mitigation}}

## Effort Estimate
{{X-Y}} developer days

## Success Metrics
- [ ] {{specific_measurable_outcome}}
- [ ] {{another_measurable_outcome}}
</agent_template>
```

### Coordination Matrix
```markdown
| Agent | Depends On | Provides To | Can Run Parallel With |
|-------|------------|-------------|----------------------|
| A1    | None       | A3, A4      | A2                   |
| A2    | None       | A4          | A1                   |
| A3    | A1         | A5          | A4                   |
| A4    | A1, A2     | A5          | A3                   |
| A5    | A3, A4     | None        | None                 |
```

## Parallel Execution Strategies

### 1. Domain-Based Parallelization
```xml
<domain_parallel>
  <frontend_agent>
    - UI components
    - User interactions
    - Client-side state
    - Styling and theming
  </frontend_agent>
  
  <backend_agent>
    - API endpoints
    - Business logic
    - Database operations
    - Authentication
  </backend_agent>
  
  <infrastructure_agent>
    - CI/CD setup
    - Deployment config
    - Monitoring
    - Security hardening
  </infrastructure_agent>
</domain_parallel>
```

### 2. Feature-Based Parallelization
```xml
<feature_parallel>
  <auth_feature_agent>
    - Login/logout
    - Registration
    - Password reset
    - Session management
  </auth_feature_agent>
  
  <payment_feature_agent>
    - Payment processing
    - Subscription management
    - Invoice generation
    - Refund handling
  </payment_feature_agent>
  
  <notification_feature_agent>
    - Email service
    - Push notifications
    - In-app messages
    - Notification preferences
  </notification_feature_agent>
</feature_parallel>
```

### 3. Layer-Based Parallelization
```xml
<layer_parallel>
  <presentation_layer>
    - View components
    - Layout systems
    - Design tokens
    - Accessibility
  </presentation_layer>
  
  <application_layer>
    - Controllers
    - Services
    - Middleware
    - Routing
  </application_layer>
  
  <data_layer>
    - Models
    - Migrations
    - Repositories
    - Caching
  </data_layer>
</layer_parallel>
```

## Claude Code Parallel Tool Usage

### Parallel File Operations
```bash
# Execute these simultaneously
Task 1: "Create authentication structure"
Task 2: "Set up database schema"
Task 3: "Initialize API routes"
Task 4: "Create base UI components"
```

### Parallel Analysis Tasks
```bash
# Run these in parallel for faster analysis
Task 1: "Analyze frontend code patterns"
Task 2: "Scan backend for security issues"
Task 3: "Review database schema"
Task 4: "Check API documentation"
```

### Parallel Testing
```bash
# Execute all test suites simultaneously
Task 1: "Run unit tests"
Task 2: "Run integration tests"
Task 3: "Run E2E tests"
Task 4: "Run performance tests"
```

## Integration with Commands

### Usage in Commands
```xml
<!-- In any command that needs parallel execution -->
<command_execution>
  <use_component>@parallel-tasks</use_component>
  
  <when_to_parallelize>
    - Multiple independent operations
    - Large analysis tasks
    - Multi-step builds
    - Comprehensive testing
  </when_to_parallelize>
  
  <parallel_section>
    <!-- Apply parallel patterns -->
    <parallel_task_execution>
      <!-- Task decomposition and execution -->
    </parallel_task_execution>
  </parallel_section>
</command_execution>
```

### Command-Specific Applications

**For /create**:
- Parallel project setup tasks
- Simultaneous package creation
- Concurrent configuration

**For /build**:
- Parallel feature implementation
- Simultaneous service creation
- Concurrent testing

**For /vision**:
- Parallel concept exploration
- Simultaneous prototype creation
- Concurrent experimentation

**For /diagram**:
- Parallel diagram generation
- Simultaneous visualization creation
- Concurrent documentation

## Success Patterns

### Clear Agent Boundaries
```xml
<boundary_definition>
  <owned_by_agent>
    - Specific files/directories
    - Clear functionality domain
    - Defined interfaces
  </owned_by_agent>
  
  <shared_resources>
    - Minimize shared state
    - Clear access patterns
    - Conflict resolution rules
  </shared_resources>
</boundary_definition>
```

### Effective Communication
```xml
<agent_communication>
  <interfaces>
    - Well-defined APIs
    - Clear data contracts
    - Version compatibility
  </interfaces>
  
  <documentation>
    - Interface specifications
    - Usage examples
    - Integration guides
  </documentation>
</agent_communication>
```

## Best Practices

1. **Independence First**: Maximize agent autonomy
2. **Clear Interfaces**: Define precise boundaries
3. **Minimal Dependencies**: Reduce coupling
4. **Parallel by Default**: Look for parallelization opportunities
5. **Progress Visibility**: Show parallel execution status
6. **Graceful Degradation**: Handle partial completions
7. **Result Integration**: Plan for merging outputs
8. **Resource Awareness**: Consider system constraints

## Anti-Patterns

- ❌ Over-decomposition (too many tiny tasks)
- ❌ Tight coupling between agents
- ❌ Unclear ownership boundaries
- ❌ Missing coordination points
- ❌ No progress visibility
- ❌ Ignoring dependencies
- ❌ Poor error handling in parallel tasks