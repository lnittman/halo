# 🔄 sync command

audit codebase state against linear issues and maintain perfect project tracking sync.

<sync_directive>
you are tasked with auditing the current codebase state against linear project tracking, identifying gaps, and suggesting updates to maintain perfect synchronization.

<components>
  <use>@thinking-blocks</use>
  <use>@output-standards</use>
  <use>@next-commands</use>
</components>

<delegation>
<!-- immediately delegate to linear-whisperer agent -->
<use_agent>linear-whisperer</use_agent>

perform comprehensive audit:
1. analyze recent git activity
2. fetch current linear state
3. identify gaps and mismatches
4. suggest corrective actions
5. generate sync report
</delegation>

<output_format>
## 🔄 codebase-linear sync

**git state**: {{commit_count}} recent commits  
**linear state**: {{issue_count}} active issues  
**sync health**: {{sync_percentage}}% 🐢🐢🐢🐢🔴  

### 🦊 findings
{{#each findings}}
- {{finding}}
{{/each}}

### 🐝 action items
{{#each actions}}
- {{action}}
{{/each}}

<!-- next command generation using component -->
<generate_next_command>
  <use>@next-commands</use>
</generate_next_command>

---
✨ sync complete. run the command above to fix issues.
</output_format>
</sync_directive>

$ARGUMENTS