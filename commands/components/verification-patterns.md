# Verification Patterns Component

Comprehensive verification and validation patterns for all Claude Code commands to ensure quality, catch errors early, and build user trust through transparency.

## Core Verification Pattern

```xml
<verification_process>
<!-- Phase 1: Pre-Execution Verification -->
<pre_execution_checks>
  <requirements_validation>
  Checking requirements are met:
  - [ ] {{requirement_1}}: {{status}}
  - [ ] {{requirement_2}}: {{status}}
  - [ ] {{requirement_3}}: {{status}}
  </requirements_validation>
  
  <dependency_check>
  Verifying dependencies:
  - {{dependency_1}}: {{available|missing|version_mismatch}}
  - {{dependency_2}}: {{available|missing|version_mismatch}}
  </dependency_check>
  
  <environment_validation>
  Environment status:
  - Working directory: {{correct|needs_adjustment}}
  - Permissions: {{adequate|insufficient}}
  - Resources: {{available|constrained}}
  </environment_validation>
</pre_execution_checks>

<!-- Phase 2: During Execution Verification -->
<execution_monitoring>
  <progress_tracking>
  Task progress:
  - [ ] Step 1: {{status}} - {{outcome}}
  - [ ] Step 2: {{status}} - {{outcome}}
  - [ ] Step 3: {{status}} - {{outcome}}
  </progress_tracking>
  
  <error_detection>
  Issues encountered:
  - {{error_type}}: {{description}} → {{resolution}}
  - {{warning_type}}: {{description}} → {{mitigation}}
  </error_detection>
  
  <assumption_verification>
  Verifying assumptions:
  - {{assumption_1}}: {{confirmed|invalidated}}
  - {{assumption_2}}: {{confirmed|invalidated}}
  </assumption_verification>
</execution_monitoring>

<!-- Phase 3: Post-Execution Verification -->
<post_execution_validation>
  <output_verification>
  Checking outputs:
  - Expected: {{expected_output}}
  - Actual: {{actual_output}}
  - Match: {{full|partial|failed}}
  </output_verification>
  
  <test_execution>
  Running verification tests:
  ```bash
  {{test_command}} # {{result}}
  ```
  - Tests passed: {{count}}/{{total}}
  - Coverage: {{percentage}}%
  - Performance: {{metrics}}
  </test_execution>
  
  <side_effect_check>
  Unintended changes:
  - Files modified: {{list_of_files}}
  - State changes: {{state_differences}}
  - External impacts: {{api_calls|db_changes}}
  </side_effect_check>
</post_execution_validation>

<!-- Phase 4: Quality Assurance -->
<quality_assurance>
  <code_quality>
  Static analysis:
  - Linting: {{pass|fail}} - {{issues}}
  - Type checking: {{pass|fail}} - {{errors}}
  - Complexity: {{score}} - {{assessment}}
  </code_quality>
  
  <security_scan>
  Security checks:
  - Vulnerabilities: {{none|found}} - {{details}}
  - Secrets scan: {{clear|exposed}} - {{findings}}
  - Permissions: {{appropriate|excessive}}
  </security_scan>
  
  <performance_check>
  Performance metrics:
  - Build time: {{duration}}
  - Bundle size: {{size}} - {{assessment}}
  - Runtime performance: {{metrics}}
  </performance_check>
</quality_assurance>
</verification_process>
```

## Command-Specific Verification

### For Build Commands
```xml
<build_verification>
  <compilation_check>
  Build verification:
  - Compilation: {{success|errors}}
  - Warnings: {{count}} - {{critical_warnings}}
  - Output artifacts: {{generated|missing}}
  </compilation_check>
  
  <integration_test>
  Integration verification:
  - API endpoints: {{responsive|failing}}
  - Database connection: {{established|failed}}
  - External services: {{connected|unreachable}}
  </integration_test>
  
  <smoke_test>
  Basic functionality:
  - Application starts: {{yes|no}}
  - Core features work: {{yes|no|partial}}
  - No critical errors: {{confirmed|errors_found}}
  </smoke_test>
</build_verification>
```

### For Create Commands
```xml
<creation_verification>
  <structure_validation>
  Project structure:
  - Required directories: {{created|missing}}
  - Configuration files: {{present|incomplete}}
  - Dependencies installed: {{yes|no|partial}}
  </structure_validation>
  
  <template_verification>
  Template application:
  - Placeholders replaced: {{all|some|none}}
  - Customizations applied: {{success|failed}}
  - No template artifacts: {{clean|remnants}}
  </template_verification>
</creation_verification>
```

### For Analysis Commands
```xml
<analysis_verification>
  <data_integrity>
  Analysis validity:
  - Data completeness: {{percentage}}%
  - Accuracy checks: {{passed|concerns}}
  - Edge cases handled: {{yes|no|partial}}
  </data_integrity>
  
  <conclusion_validation>
  Findings verification:
  - Evidence supports conclusions: {{strong|weak}}
  - Alternative explanations: {{considered|missed}}
  - Confidence level: {{high|medium|low}}
  </conclusion_validation>
</analysis_verification>
```

## Verification Loops

```xml
<verification_loops>
<!-- Continuous verification during long operations -->
<continuous_loop interval="{{seconds}}">
  <health_check>
  System health:
  - Memory usage: {{percentage}}%
  - CPU usage: {{percentage}}%
  - Disk space: {{available}}
  - Process status: {{running|stalled|crashed}}
  </health_check>
  
  <progress_validation>
  Progress verification:
  - Expected progress: {{percentage}}%
  - Actual progress: {{percentage}}%
  - Estimated completion: {{time}}
  - Stuck detection: {{moving|potentially_stuck}}
  </progress_validation>
</continuous_loop>

<!-- Retry logic with verification -->
<retry_verification max_attempts="3">
  <attempt number="{{n}}">
    <action>{{action_description}}</action>
    <result>{{success|failed}}</result>
    <error>{{error_if_any}}</error>
    <adjustment>{{what_changed_for_retry}}</adjustment>
  </attempt>
</retry_verification>
</verification_loops>
```

## User-Visible Verification Summary

```markdown
### ✅ Verification Report

**Pre-execution checks**: {{all_passed|some_failed}}
{{#if failed_checks}}
- ⚠️ {{failed_check_description}}
{{/if}}

**Execution status**: {{completed|completed_with_warnings|failed}}
- Tasks completed: {{n}}/{{total}}
- Warnings: {{warning_count}}
- Errors: {{error_count}}

**Quality checks**:
- 🧪 Tests: {{test_status}} ({{passed}}/{{total}})
- 🔍 Linting: {{lint_status}}
- 🔒 Security: {{security_status}}
- ⚡ Performance: {{performance_status}}

**Confidence level**: {{high|medium|low}}
{{confidence_explanation}}

{{#if issues_found}}
### ⚠️ Issues Found
{{#each issues}}
- **{{issue.type}}**: {{issue.description}}
  - Impact: {{issue.impact}}
  - Suggested fix: {{issue.fix}}
{{/each}}
{{/if}}
```

## Verification Strategies

### 1. Fail-Fast Verification
```xml
<fail_fast>
  <critical_checks>
  Stop immediately if:
  - Required tools missing
  - Permissions insufficient  
  - Disk space inadequate
  - Critical services down
  </critical_checks>
</fail_fast>
```

### 2. Progressive Verification
```xml
<progressive>
  <stages>
  Stage 1: Basic requirements
  Stage 2: Full environment
  Stage 3: Integration points
  Stage 4: Performance targets
  </stages>
</progressive>
```

### 3. Parallel Verification
```xml
<parallel_verification>
  <independent_checks>
  Run simultaneously:
  - Lint check
  - Type check
  - Unit tests
  - Security scan
  </independent_checks>
</parallel_verification>
```

## Error Recovery Patterns

```xml
<error_recovery>
  <automatic_fixes>
  Common issues auto-resolved:
  - Missing directories: {{created}}
  - Outdated dependencies: {{updated}}
  - Format issues: {{auto_formatted}}
  </automatic_fixes>
  
  <manual_intervention>
  Requires user action:
  - Issue: {{description}}
  - Why we can't auto-fix: {{reason}}
  - Suggested command: {{fix_command}}
  - Alternative approach: {{alternative}}
  </manual_intervention>
</error_recovery>
```

## Integration with Commands

### Placement
```xml
<!-- In command structure -->
<command_name>
  <universal_input_handler/>
  <prompt_transformation/>
  <thinking_process/>
  
  <!-- Add verification at key points -->
  <pre_execution_verification>
    <!-- Use appropriate patterns -->
  </pre_execution_verification>
  
  <main_execution>
    <!-- Include execution_monitoring -->
  </main_execution>
  
  <post_execution_verification>
    <!-- Full validation -->
  </post_execution_verification>
  
  <output_generation>
    <!-- Include verification summary -->
  </output_generation>
</command_name>
```

## Best Practices

1. **Transparent Verification**: Show users what's being checked
2. **Actionable Feedback**: Provide clear fixes for issues
3. **Progressive Detail**: Summary first, details on request
4. **Continuous Validation**: Don't wait until the end
5. **Smart Recovery**: Auto-fix when safe, ask when not
6. **Performance Aware**: Don't let verification slow things down
7. **Context Sensitive**: More thorough for production commands
8. **Learning System**: Use past failures to improve checks

## Anti-Patterns

- ❌ Silent verification failures
- ❌ Over-verification of simple tasks
- ❌ Cryptic error messages
- ❌ Blocking on non-critical issues
- ❌ Ignoring verification results
- ❌ Verification theater (checks that don't matter)