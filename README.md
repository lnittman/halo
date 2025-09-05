# halo

minimalist coding agent system with personality.

## what is halo?

halo transforms verbose AI interactions into clean, readable experiences. think of it as a design system for coding agents — making them more human, more useful, more you.

### key features

- **lowercase vibes** - relaxed, approachable tone
- **clear cues** - focused, readable structure for clarity
- **clean output** - no walls of text
- **personality** - subtle, not overwhelming

## quick start

```bash
# use any halo command
/prime    # understand your project
/build    # implement features
/create   # scaffold new projects
/vision   # explore possibilities
```

## structure

```
.halo/
├── README.md           # you are here
├── halo-style-guide.md # the vibe
├── commands/           # all commands (includes specialist command prompts)
├── components/         # reusable parts
├── roles/              # expert personas (referenced by commands)
└── rules/              # coding standards
```

## the halo style

### text rules
- **lowercase everything** (except acronyms: AI, API, etc.)
- **clear, minimal formatting** (no decorative symbols)
- **concise & direct** (no fluff)

### example output
```markdown
## build complete

**created**: 5 files
**time**: 1.3s
**next**: [TEST] [DEPLOY]
```

### not this
```markdown
## Build Successfully Completed!

I've successfully created 5 new files for you...
[wall of text continues]
```

## commands

### `/prime`
understand your project context instantly

### `/build`
transform ideas into working code

### `/create`
scaffold complete project ecosystems

### `/vision`
explore transformative possibilities

### `/design`
audit and document design systems

### `/docs`
comprehensive documentation operations

### `/brand`
create world-class brand identities

## agents

each agent has a personality that matches their purpose:

- **simplify-design** - minimalist refactoring expert
- **polish-interface** - detail-oriented perfectionist
- **audit-codebase** - thorough quality checker
- **tech-docs** - documentation aggregation specialist
- **github-whisperer** - git and github operations expert
- **cloudflare-whisperer** - cloudflare services specialist
- **test-coverage** - comprehensive testing specialist
- **dependency-doctor** - package management expert
- **linear-whisperer** - project tracking sync specialist

## roles

expert personas and functional specialists:

**personas**:
- rick rubin - zen creative guidance
- dieter rams - minimalist design philosophy
- jony ive - obsessive simplification
- teenage engineering - playful utility

**functions**:
- full-stack architect
- ai integration specialist
- product manager
- ux researcher

### role aliases (no symlinks)
Legacy short-hands are mapped in `commands/roles/aliases.json` and resolve to canonical files under `commands/roles/` (e.g., `ive → ./design/jony.md`, `rams → ./design/dieter.md`, `ando → ./architecture/tadao.md`).

Notes:
- Paths are resolved relative to `commands/roles/aliases.json`; use `./`-prefixed relative paths.
- To add a new alias, add a key→path entry to that JSON file.

## philosophy

inspired by:
- **teenage engineering** - constraints breed creativity
- **dieter rams** - less, but better
- **80s-90s computing** - when interfaces had soul

## customization

### modify commands
edit any `.md` file in `/commands/` to adjust behavior

### change style
update `halo-style-guide.md` to match your vibe

### add roles
 drop new personas in `/roles/` folder

### create roles
add expert personas in `/roles/` directory

## tips

1. **be direct** - halo understands context
2. **be concise** - commands work without prefixes
3. **chain commands** - they share context
4. **trust the vibe** - let halo's personality shine

## examples

### understand a project
```bash
/prime
# instant context about your codebase
```

### build a feature
```bash
/build add dark mode to settings
# implements with your patterns
```

### create an app
```bash
/create weather-app
# full ecosystem scaffolded
```

## compatibility

halo works with:
- claude code (primary)
- github copilot
- cursor
- any AI that reads markdown

---

*remember: less noise, more signal. that's halo.*

## license

MIT - do whatever makes you happy

## contributing

keep it simple, keep it clean, keep it halo.

---

made by developers who prefer lowercase
