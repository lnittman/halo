# Output standards component

Transforms verbose markdown into clean, readable output following Halo style.

## Core output structure

```xml
<halo_output>
<!-- command acknowledgment -->
<prompt_echo>
## {{command}} {{arguments}}
</prompt_echo>

<!-- clean status display -->
<status_display>
**key metric**: {{value}}
**another metric**: {{value}}
**status**: {{indicator}}
</status_display>

<!-- action prompt -->
<next_actions>
{{#if immediate_action}}
### {{action}}
{{/if}}

<!-- ALWAYS include next-command so the user gets the best next step to run explicitly -->
<generate_next_command>
  <use>@next-command</use>
</generate_next_command>
</next_actions>
</halo_output>
```

## Output templates

### command execution
```markdown
## {{command}} executed

**files**: {{file_stats}}  
**time**: {{duration}}  
**status**: {{indicator}}  

{{#if details}}
### Details
- {{detail_line_1}}
- {{detail_line_2}}
{{/if}}

**next steps**: [BUILD] [TEST] [DEPLOY]
```

### analysis results
```markdown
## Analysis · {{target}}

**health**: {{pct}}%  
**issues**: {{count}} found  
**suggestions**: {{count}} available  

### Top issues
{{#each issues}}
- {{icon}} {{file}}:{{line}}
{{/each}}

**action**: run [FIX] to auto-resolve
```

### error handling
```markdown
## Error · {{error_type}}

**what**: {{error_message}}  
**where**: {{file}}:{{line}}  
**hint**: {{suggestion}}  

**retry?** Y/n
```

### progress display
```markdown
## {{operation}} in progress

{{progress_bar}} {{percentage}}%  
{{status_indicator}} {{current_task}}  

[SPACE] pause [ESC] cancel
```

## Status indicators

```javascript
const indicators = {
  // progress states
  pending:     'pending',
  starting:    'starting',
  running:     'running',
  finishing:   'finishing',
  complete:    'complete',

  // health states
  excellent:   '5/5',
  good:        '4/5',
  fair:        '3/5',
  poor:        '2/5',
  critical:    '1/5',
}
```

## Command-specific formats

### prime (context initialization)
```markdown
## Project context

**type**: {{project_type}}  
**stack**: {{tech_stack}}  
**health**: {{health_bar}}  

### Recent activity
{{#each recent_items}}
- {{item}}
{{/each}}

**ready**: [BUILD] [CREATE] [AUDIT]
```

### build (implementation)
```markdown
## Build success

**created**: {{new}} files  
**updated**: {{mod}} files  
**time**: {{time}}s  

{{#if start_command}}
### Start
```bash
{{start_command}}
```
{{/if}}

**next**: [TEST] [DEPLOY] [ITERATE]
```

### create (project generation)
```markdown
## Project scaffolded

**name**: {{project_name}}  
**type**: {{project_type}}  
**dependencies**: {{dep_count}}  
**size**: {{size_mb}}MB  

### Structure
{{#each structure}}
{{indent}}{{icon}} {{name}}
{{/each}}

### Quick start
```bash
cd {{project_path}} && {{start_cmd}}
```
```

## Interaction patterns

### multi-page results
```markdown
## {{title}} [{{page}}/{{total}}]

{{#each items}}
- {{icon}} {{item}}
{{/each}}

**navigation**: [N]ext [P]rev [G]oto [F]ilter [Q]uit
```

### choice prompts
```markdown
## Select option

{{#each options}}
**{{key}}**: {{label}} {{icon}}
{{/each}}

**choice**: _
```

### confirmation dialogs
```markdown
## {{question}}

**confirm**: Y/n
```

## Formatting rules

### text conventions
- all lowercase (except acronyms/proper nouns)
- concise labels, no fluff
- functional emoji only
- keyboard shortcuts in [BRACKETS]

### spacing & alignment
- 2-space indents
- clean markdown formatting
- single line between major sections
- pack information efficiently

## Implementation guide

### transforming verbose output
```javascript
// OLD (verbose)
## Summary
Successfully analyzed 42 files...

// NEW (halo)
## Scan complete
**result**: 42 files analyzed
```

### adding personality
```javascript
// subtle personality
'processing...'
'analyzing...'
'building...'
'complete!'
```

### showing progress
```javascript
// simple
Analyzing...

// detailed
[75%] processing · 3.2s remaining

// multi-step
scanning files
analyzing code
generating report
formatting output
```

## Output checklist

when generating output:
- [ ] avoid emoji
- [ ] show clear status
- [ ] include progress indicators
- [ ] suggest next actions
- [ ] keep text lowercase (except acronyms)
- [ ] use clean markdown formatting

---
Output standards ready!
