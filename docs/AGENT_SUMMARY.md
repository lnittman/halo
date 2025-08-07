# 🦊 Halo Specialist Command Summary

## 📊 Specialist Categories & Permissions

### 🔍 Analyzers (READ-ONLY)
These specialists only read and analyze - they NEVER modify files.

#### audit-codebase ✅
- **Tools**: Grep, Glob, Read (no write tools)
- **Purpose**: Code quality analysis and reporting
- **Output**: Structured audit report with issues, warnings, suggestions
- **Usage**: "Audit this codebase" or automatically after code changes

#### pattern-extractor ✅
- **Tools**: Read, Grep, Glob (READ-ONLY)
- **Purpose**: Extract patterns and best practices
- **Note**: Enforced read-only; no Task tool

### 🏗️ Builders (READ-WRITE)
These agents create and modify files to build features.

#### polish-interface
- **Tools**: Read, Edit, MultiEdit, Write
- **Purpose**: Add final UI touches and polish
- **Usage**: "Polish this interface" after building

#### video-studio
- **Tools**: Read, Write, MultiEdit, Bash, mcp tools
- **Purpose**: Create videos with Remotion
- **Usage**: "Create a product video showcasing my button component"

#### 3d-artist
- **Tools**: Read, Write, MultiEdit, Bash, mcp tools
- **Purpose**: Create 3D/WebGL experiences
- **Usage**: "Add ferrofluid effect like Vercel Ship"

#### motion-expert
- **Tools**: Read, Write, MultiEdit, mcp tools
- **Purpose**: Create animations with Framer Motion/Lenis
- **Usage**: "Add smooth scroll and reveal animations"

### 🔗 Integrations (SERVICE-SPECIFIC)
These agents integrate with external services.

#### linear-whisperer
- **Tools**: All Linear MCP tools + Read, Write, Task
- **Purpose**: Sync code with Linear issues
- **Output**: Sync report and updated issues

#### github-whisperer
- **Tools**: Bash, Read, MultiEdit, Grep, Glob
- **Purpose**: Git operations and GitHub management
- **Usage**: "Commit these changes" or "Create a PR"

#### cloudflare-whisperer
- **Tools**: Bash, Read, Write, MultiEdit, Grep
- **Purpose**: Deploy to Cloudflare services
- **Usage**: "Deploy to Cloudflare Workers"

### 📚 Specialists (MIXED PERMISSIONS)

#### tech-docs ⚠️
- **Tools**: MCP tools + Read, Write, MultiEdit
- **Purpose**: Aggregate documentation
- **Note**: Should possibly be READ-ONLY with report output
- **Usage**: "Get me Remotion documentation"

#### test-coverage
- **Tools**: Bash, Read, Write, MultiEdit, Grep, Glob
- **Purpose**: Write and run tests
- **Usage**: "Add tests for this component"

#### dependency-doctor
- **Tools**: Bash, Read, Write, MultiEdit, WebSearch, Grep
- **Purpose**: Manage dependencies
- **Usage**: "Update all packages"

#### github-analyzer ✅
- **Tools**: Bash, Read, Grep, Glob, WebFetch, Context7, Firecrawl
- **Purpose**: Analyze GitHub repositories by URL (not local git)
- **Note**: Now properly READ-ONLY, analyzes remote repos only
- **Usage**: "Analyze https://github.com/vercel/next.js"

### 🎨 Refiners (MIXED PERMISSIONS)

#### simplify-design
- **Tools**: Read, Edit, MultiEdit, Grep
- **Purpose**: Simplify code/UI
- **Usage**: "Simplify this component"

#### docs-generator
- **Tools**: Read, Write, MultiEdit, Grep, Glob
- **Purpose**: Generate documentation
- **Usage**: After research to create docs

#### tech-researcher ⚠️
- **Tools**: MCP tools + Read, Write, MultiEdit
- **Purpose**: Research technologies
- **Note**: Overlaps with tech-docs
- **Action**: Consider merging or clarifying distinction

#### stack-expert-dev
- **Tools**: Read, Write, MultiEdit, Bash, Grep, Glob
- **Purpose**: Expert guidance on tech stack
- **Usage**: "How do I implement auth in Next.js 15?"

## 🚨 Agents That Should Be READ-ONLY

1. **pattern-extractor** - Remove Task tool
2. **tech-docs** - Should generate reports, not modify files
3. **github-analyzer** - Now properly READ-ONLY, analyzes GitHub repos by URL
4. **tech-researcher** - Should research and report

## 💡 How to Use Creative Agents

### For Motion & Animation
```bash
# Basic usage
"Add smooth scroll to my site" → commands/builder/motion-expert
"Create page transitions" → commands/builder/motion-expert
"Add micro-interactions to buttons" → commands/builder/motion-expert

# Advanced
"Create a reveal animation like Apple's site" → commands/builder/motion-expert
"Add magnetic hover effects" → commands/builder/motion-expert
```

### For 3D Effects
```bash
# Basic usage
"Add 3D hero section" → commands/builder/3d-artist
"Create particle effects" → commands/builder/3d-artist

# Advanced
"Create ferrofluid effect like Vercel Ship" → commands/builder/3d-artist
"Add WebGL background with shader effects" → commands/builder/3d-artist
"Build interactive 3D product showcase" → commands/builder/3d-artist
```

### For Video Creation
```bash
# Basic usage
"Create product demo video" → commands/builder/video-studio
"Make UI component showcase video" → commands/builder/video-studio

# Advanced
"Create animated explainer for my API" → commands/builder/video-studio
"Build conference intro video with logo animation" → commands/builder/video-studio
"Generate social media videos from my components" → commands/builder/video-studio
```

## 📋 Output Templates Needed

### Linear Whisperer
```markdown
# 🔄 Linear Sync Report

**Synced**: [timestamp]
**Issues Updated**: [count]
**New Issues**: [count]

## 📊 Summary
- Active issues: [count]
- Completed this cycle: [count]
- Blocked: [count]

## 🔄 Updates Made
1. Issue LIN-123: Updated to "In Progress"
2. Issue LIN-456: Created from TODO in code
```

### Tech-Docs
```markdown
# 📚 [Technology] Documentation

**Version**: X.X.X
**Generated**: [timestamp]
**Sources**: [count] documents aggregated

## 🚀 Quick Start
[Installation and basic usage]

## 📖 Core Concepts
[Key concepts with examples]

## 🔗 All URLs Found
- Official docs: [url]
- API reference: [url]
- Examples: [urls]
```

### Git-Research
```markdown
# 🔬 Repository Analysis: [repo-name]

**Stars**: [count]
**Language**: [primary]
**Architecture**: [type]

## 🏗️ Structure
[Visual tree of key directories]

## 🔍 Key Patterns
[Identified patterns with code examples]

## 💡 Integration Guide
[How to adopt patterns in your project]
```

## 🎯 Recommendations

1. **Make truly read-only agents READ-ONLY** by removing write tools
2. **Add explicit output templates** to each agent's prompt
3. **Use "PROACTIVELY" in descriptions** for auto-triggering
4. **Clarify overlapping agents** (tech-docs vs tech-researcher)
5. **Add usage examples** in each agent's prompt

## 🚀 Next Steps

1. Update agents to enforce read-only where appropriate
2. Add output templates to all agents
3. Test creative agents with real projects
4. Create agent interaction flowchart
5. Document agent handoff patterns