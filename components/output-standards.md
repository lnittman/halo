# 📋 output standards component

transforms verbose markdown into clean, emoji-rich output following halo style.

## 🌀 core output structure

```xml
<halo_output>
<!-- command acknowledgment -->
<prompt_echo>
## 🎯 {{command}} {{arguments}}
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
### ⚡ {{action}}
{{/if}}

<!-- ALWAYS include next-command so the user gets the best next step to run explicitly -->
<generate_next_command>
  <use>@next-command</use>
</generate_next_command>
</next_actions>
</halo_output>
```

## 🎮 output templates

### command execution
```markdown
## ✅ {{command}} executed

**files**: {{file_stats}}  
**time**: {{duration}} ⚡  
**status**: {{indicator}}  

{{#if details}}
### 📊 details
- {{detail_line_1}}
- {{detail_line_2}}
{{/if}}

**next steps**: [BUILD] [TEST] [DEPLOY]
```

### analysis results
```markdown
## 📊 analysis · {{target}}

**health**: {{pct}}% 🟢🟢🟢🟢🔴  
**issues**: {{count}} found  
**suggestions**: {{count}} available  

### 🔍 top issues
{{#each issues}}
- {{icon}} {{file}}:{{line}}
{{/each}}

**action**: run [FIX] to auto-resolve
```

### error handling
```markdown
## ❌ error · {{error_type}}

**what**: {{error_message}}  
**where**: {{file}}:{{line}}  
**hint**: {{suggestion}}  

**retry?** Y/n
```

### progress display
```markdown
## 🔄 {{operation}} in progress

{{progress_bar}} {{percentage}}%  
{{status_indicator}} {{current_task}}  

[SPACE] pause [ESC] cancel
```

## 📊 status indicators

```javascript
const indicators = {
  // progress states
  pending:     '⏸️',
  starting:    '▶️',
  running:     '⏳',
  finishing:   '⏱️',
  complete:    '✅',
  
  // health states
  excellent:   '🟢🟢🟢🟢🟢',
  good:        '🟢🟢🟢🔶🔴',
  fair:        '🟢🟢🔶🔴🔴',
  poor:        '🟢🔶🔴🔴🔴',
  critical:    '🔴🔴🔴🔴🔴',
}
```

## 🎯 command-specific formats

### prime (context initialization)
```markdown
## 🎯 project context

**type**: {{project_type}}  
**stack**: {{tech_stack}}  
**health**: {{health_bar}}  

### 📡 recent activity
{{#each recent_items}}
- {{item}}
{{/each}}

**ready**: [BUILD] [CREATE] [AUDIT]
```

### build (implementation)
```markdown
## ✅ build success

**created**: {{new}} files  
**updated**: {{mod}} files  
**time**: {{time}}s ⚡  

{{#if start_command}}
### 🚀 start
```bash
{{start_command}}
```
{{/if}}

**next**: [TEST] [DEPLOY] [ITERATE]
```

### create (project generation)
```markdown
## 🌐 project scaffolded

**name**: {{project_name}}  
**type**: {{project_type}}  
**dependencies**: {{dep_count}}  
**size**: {{size_mb}}MB  

### 📁 structure
{{#each structure}}
{{indent}}{{icon}} {{name}}
{{/each}}

### 🚀 quick start
```bash
cd {{project_path}} && {{start_cmd}}
```
```

## 🖥️ interaction patterns

### multi-page results
```markdown
## 📄 {{title}} [{{page}}/{{total}}]

{{#each items}}
- {{icon}} {{item}}
{{/each}}

**navigation**: [N]ext [P]rev [G]oto [F]ilter [Q]uit
```

### choice prompts
```markdown
## 🎮 select option

{{#each options}}
**{{key}}**: {{label}} {{icon}}
{{/each}}

**choice**: _
```

### confirmation dialogs
```markdown
## ❓ {{question}}

**confirm**: Y/n
```

## 🎨 formatting rules

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

## 🚀 implementation guide

### transforming verbose output
```javascript
// OLD (verbose)
## Summary
Successfully analyzed 42 files...

// NEW (halo)
## ✅ scan complete
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
⏳ analyzing...

// detailed
[75%] processing · 3.2s remaining

// multi-step
✅ scanning files
✅ analyzing code
⏳ generating report
⏸️ formatting output
```

## 📋 output checklist

when generating output:
- [ ] use functional emoji
- [ ] show clear status
- [ ] include progress indicators
- [ ] suggest next actions
- [ ] keep text lowercase (except acronyms)
- [ ] use clean markdown formatting

---
✨ output standards ready!