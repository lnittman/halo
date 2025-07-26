# /user:tech

Deep-dive technology research and documentation command for comprehensive tool understanding.

## Description

This command performs exhaustive research on technologies, gathering documentation from multiple sources and creating comprehensive reference materials. Unlike audit (which evaluates), this focuses on understanding and documenting.

## Usage

```
/user:tech [technology] [--depth full|standard|quick]
```

## Features

1. **Documentation Gathering**
   - Context7 library documentation
   - Firecrawl official sites
   - GitHub repositories
   - Community resources

2. **Content Synthesis**
   - API references
   - Code examples
   - Best practices
   - Common patterns

3. **Output Formats**
   - Structured markdown docs
   - Code snippet libraries
   - Integration examples
   - Quick reference guides

## Process

1. **Source Discovery**
   ```
   - Official documentation
   - GitHub README/Wiki
   - Blog posts/tutorials
   - Video transcripts
   - Community forums
   ```

2. **Content Extraction**
   ```
   - Core concepts
   - API methods
   - Configuration options
   - Code examples
   - Error handling
   ```

3. **Documentation Creation**
   ```
   ~/Developer/docs/tools/[technology]/
   ├── concepts/           # Core concepts
   ├── api/               # API reference
   ├── examples/          # Code examples
   ├── patterns/          # Common patterns
   ├── integrations/      # Framework integrations
   └── resources/         # Raw scraped content
   ```

## Depth Levels

- **quick**: Essential concepts and basic usage
- **standard**: Full API coverage and examples
- **full**: Everything including edge cases

## Examples

```
/user:tech drizzle --depth full
/user:tech "cloudflare workers"
/user:tech hono --depth quick
```

## Output Template

Each technology gets:
1. Overview and philosophy
2. Installation and setup
3. Core API reference
4. Common use cases
5. Integration guides
6. Troubleshooting
7. Performance tips
8. Security considerations

## Integration

- Outputs feed into `/user:docs-gen`
- Compatible with `CLAUDE.md` format
- Follows documentation standards
- Machine-readable indexes