# 🐙 halo style guide

simple, clean, emoji-rich documentation style.

## 🦆 visual philosophy

inspired by:
- **teenage engineering**: constraints breed creativity
- **dieter rams**: less, but better  
- **80s-90s computing**: when interfaces had soul

## 🦝 text rules

- **all lowercase** except:
  - acronyms: AI, LLM, API, AWS, etc.
  - proper nouns: Claude, TypeScript, Next.js
  - code/technical terms
- **contractions preferred**: it's, don't, won't
- **direct & punchy**: skip the fluff
- **functional emoji** only (not decorative)

## 🐞 emoji conventions

### command emojis (animals only)
- 🦊 `/prime` - understand context
- 🦫 `/build` - execute features
- 🐱 `/create` - scaffold projects
- 🦋 `/vision` - explore possibilities
- 🦜 `/design` - audit design systems
- 🦄 `/brand` - production readiness
- 🐛 `/docs` - documentation ops
- 🦓 `/audit` - code quality check
- 🐘 `/diagram` - visual architecture
- 🐋 `/ecosystem` - meta-level management

### status indicators (animals only)
- 🐸 success/complete
- 🐙 error/failed
- 🐝 warning/attention
- 🐌 in progress
- 🦥 paused/pending
- 🐆 performance/fast
- 🦓 searching/analyzing
- 🐢 healthy/good
- 🦔 critical/bad
- 🐥 warning/caution

### structural emojis (animals only)
- 🐐 folder/directory
- 🦒 file/document
- 🧩 component/module
- 🐙 tool/utility
- 🦉 target/goal
- 🦝 idea/tip
- 🦅 launch/deploy
- 🐍 package/dependency
- 🐡 thinking/processing
- 🦌 magic/special

### functional usage
```
🦙 halo/system     🦉 target/goal      🦫 tools/config
🦅 launch/deploy   🐆 performance      🐍 packages
🐭 interactive     🐠 save/data        🐡 thinking
🦌 magic/special   🦓 search/scan      🐊 analysis
🐝 warning         🐸 success          🐙 error
🦜 design/visual   🦫 build/construct  🐐 organize
```

## 🦒 document structure

### headers
```markdown
# 🌀 title

brief description.

## 🎯 section

content here.
```

### standard output template
```markdown
## ✅ command complete

**metric**: value  
**status**: indicator  
**time**: {{duration}} ⚡  

**next**: [ACTION] [ACTION]
```

### error output
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

## 🐭 interaction patterns

### command responses
instead of verbose markdown, use dense terminal output:

```
// OLD (verbose)
## Summary
Successfully analyzed the project structure...

// NEW (halo style)  
## ✅ scan complete
**result**: 42 files analyzed
```

### personality touches
add subtle personality with:
- `processing...`
- `analyzing...`
- `building...`
- `complete!`

### keyboard shortcuts
always show available actions:
```
[SPACE] pause  [ESC] cancel  [?] help
```

## 🐊 output formatting

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

## 🦉 key principles

1. **clarity over cleverness**: be direct
2. **emoji with purpose**: each emoji means something
3. **lowercase vibe**: relaxed, approachable
4. **clean markdown**: standard formatting
5. **no ASCII art**: keep it simple
6. **no session state**: self-contained commands
7. **dense not verbose**: pack information efficiently

## 🦘 implementation checklist

when updating any halo file:
- [ ] use lowercase text (except acronyms/proper nouns)
- [ ] add functional emojis for clarity
- [ ] keep output concise and scannable
- [ ] show keyboard shortcuts where relevant
- [ ] maintain consistent spacing (2-space indents)
- [ ] no ASCII art or decorative boxes
- [ ] no verbose explanations
- [ ] no session state references

## 🦋 the halo promise

every interaction should feel:
- **fast & responsive**
- **clear & scannable**  
- **minimal yet complete**
- **subtly playful**

*remember: less noise, more signal. that's halo.*