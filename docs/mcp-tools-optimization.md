# 🛠️ MCP Tools Optimization Plan

Comprehensive plan to optimize MCP (Model Context Protocol) tool usage across all agents.

## 🎯 Key Optimizations

### 1. Prefer Context7 Over Firecrawl
- **Why**: Context7 is free vs Firecrawl which costs money
- **Use Context7 for**: Library documentation, API references, framework docs
- **Use Firecrawl only when**: Context7 doesn't have the content, need to scrape specific sites

### 2. Add Missing MCP Integrations
Based on research, these MCP tools should be added:

| Tool | Purpose | Agents to Add |
|------|---------|---------------|
| **mcp__cloudflare__*** | Deploy & manage Cloudflare resources | cloudflare-whisperer |
| **mcp__mastra__*** | AI workflow orchestration | ai-architect, tech-docs |
| **mcp__prisma__*** | Database schema management | stack-expert-dev |
| **mcp__github__*** | GitHub operations (if available) | github-whisperer |
| **mcp__postgres__*** | Direct DB operations | stack-expert-dev |

### 3. Tool Usage Guidelines

#### For Documentation Tasks
```yaml
priority_order:
  1. mcp__context7__* # Free, comprehensive
  2. WebFetch         # For specific pages
  3. mcp__firecrawl__* # Only if needed (costs $)
```

#### For AI Development
```yaml
ai_agents_should_have:
  - mcp__mastra__* # Workflow orchestration
  - mcp__context7__* # AI library docs
  - WebSearch # Latest AI trends
```

#### For Infrastructure
```yaml
cloudflare_agents_need:
  - mcp__cloudflare__deploy
  - mcp__cloudflare__workers
  - mcp__cloudflare__d1
  - mcp__cloudflare__r2
  - mcp__cloudflare__kv
```

## 📊 Agent Updates Needed

### High Priority Updates

1. **cloudflare-whisperer**
   - ADD: All Cloudflare MCP tools
   - REMOVE: Manual wrangler commands where MCP available
   - CONTEXT: Manages ~/Developer/apps/*/*-xyz/ turborepos

2. **ai-architect**
   - ADD: mcp__mastra__* tools
   - PREFER: context7 over firecrawl
   - FOCUS: Mastra workflows, Vercel AI SDK

3. **tech-docs & tech-researcher**
   - REORDER: context7 before firecrawl
   - ADD: More context7 capabilities
   - MINIMIZE: firecrawl usage

### Medium Priority Updates

4. **stack-expert-dev**
   - ADD: mcp__prisma__* for schema management
   - ADD: mcp__postgres__* for DB operations
   - KEEP: context7 for framework docs

5. **motion-expert, 3d-artist, video-studio**
   - REORDER: Prioritize context7
   - KEEP: firecrawl only for specific creative sites

### Low Priority Updates

6. **github-whisperer**
   - CHECK: If mcp__github__* tools exist
   - COMPLEMENT: gh CLI with MCP tools

## 🔧 Implementation Strategy

### Phase 1: Update Tool Lists
```yaml
# Example update for an agent
tools_before: 
  - mcp__firecrawl__firecrawl_scrape
  - mcp__context7__get-library-docs
  - Read, Write

tools_after:
  - mcp__context7__resolve-library-id  # First
  - mcp__context7__get-library-docs    # First
  - mcp__firecrawl__firecrawl_scrape  # Last resort
  - Read, Write
```

### Phase 2: Update Usage Patterns
```typescript
// Before
const docs = await firecrawl.scrape(url);

// After
try {
  const libId = await context7.resolveLibraryId(library);
  const docs = await context7.getLibraryDocs(libId);
} catch {
  // Fallback to firecrawl only if needed
  const docs = await firecrawl.scrape(url);
}
```

### Phase 3: Add Context
Each agent should know:
- Which tools are free vs paid
- When to use each tool
- Fallback strategies

## 📈 Expected Benefits

1. **Cost Reduction**: 80%+ less firecrawl usage
2. **Better Documentation**: Context7 has curated, up-to-date docs
3. **Faster Operations**: MCP tools are optimized
4. **More Capabilities**: Direct integration vs CLI commands

## 🚀 Additional MCP Tools to Consider

Based on the research and your stack:

### Should Add
- **Tavily**: AI-optimized search (better than WebSearch)
- **Neon**: If using Neon for Postgres
- **Universal DB**: For multi-database support

### Maybe Later
- **Unstructured**: For document processing
- **21st.dev Magic**: For UI component generation
- **ActionKit**: For SaaS integrations

## 📋 Validation Checklist

For each updated agent:
- [ ] Context7 listed before firecrawl
- [ ] Relevant MCP tools added
- [ ] Usage patterns updated
- [ ] Cost considerations documented
- [ ] Fallback strategies defined

---

*This optimization will make agents more efficient, cost-effective, and capable.*