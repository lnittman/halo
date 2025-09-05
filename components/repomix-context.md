# repomix intelligent context component

smart context gathering using repomix with automatic token management and tree visualization.

<repomix_component>
## usage trigger
invoke this component when:
- user explicitly says "use repomix"
- comprehensive codebase understanding is required
- full context audit is needed

## intelligent repomix execution

### step 1: project structure visualization
always start with a tree view to understand project layout:
```bash
# Get project structure (excluding common large directories)
tree -L 3 -I 'node_modules|.git|dist|build|coverage|.next|.turbo|.cache|vendor|target|out|*.log' --dirsfirst
```

if tree is not available:
```bash
# Fallback to find-based structure
find . -type d -name node_modules -prune -o \
       -type d -name .git -prune -o \
       -type d -name dist -prune -o \
       -type d -name build -prune -o \
       -type d -path "*/.*" -prune -o \
       -type f -print | head -100 | sed 's|^\./||' | sort
```

### step 2: smart repomix execution

#### initial context gathering
```bash
# First attempt - comprehensive but size-aware
npx repomix \
  ${FOCUS_PATH:+--include "$FOCUS_PATH/**/*"} \
  --ignore 'node_modules/**' \
  --ignore '.git/**' \
  --ignore 'dist/**' \
  --ignore 'build/**' \
  --ignore 'coverage/**' \
  --ignore '.next/**' \
  --ignore '.turbo/**' \
  --ignore '*.log' \
  --ignore '*.lock' \
  --ignore 'package-lock.json' \
  --ignore 'yarn.lock' \
  --ignore 'pnpm-lock.yaml' \
  --ignore '.DS_Store' \
  --ignore '**/*.min.js' \
  --ignore '**/*.min.css' \
  --ignore '**/*.map' \
  --ignore 'vendor/**' \
  --ignore 'public/assets/**' \
  --ignore 'static/**' \
  --output-file .repomix-full.md

# Check file size
FILE_SIZE=$(wc -c < .repomix-full.md)
TOKEN_ESTIMATE=$((FILE_SIZE / 4))  # Rough estimate: 1 token ≈ 4 characters

echo "Context size: $FILE_SIZE bytes (~$TOKEN_ESTIMATE tokens)"
```

#### token limit handling
if context is too large (>50k tokens), progressively refine:

```bash
# If too large, try focused approach
if [ $TOKEN_ESTIMATE -gt 50000 ]; then
  echo "Context too large, refining..."
  
  # Option 1: Focus on source code only
  npx repomix \
    --include 'src/**/*' \
    --include 'app/**/*' \
    --include 'components/**/*' \
    --include 'lib/**/*' \
    --include 'utils/**/*' \
    --include '*.md' \
    --include '*.json' \
    --include '*.yaml' \
    --include '*.yml' \
    --ignore 'node_modules/**' \
    --ignore '.git/**' \
    --ignore 'dist/**' \
    --ignore 'build/**' \
    --ignore '**/*.test.*' \
    --ignore '**/*.spec.*' \
    --ignore '**/*.stories.*' \
    --output-file .repomix-focused.md
    
  NEW_SIZE=$(wc -c < .repomix-focused.md)
  NEW_TOKENS=$((NEW_SIZE / 4))
  echo "Refined context: $NEW_SIZE bytes (~$NEW_TOKENS tokens)"
  
  # Option 2: If still too large, exclude specific file types
  if [ $NEW_TOKENS -gt 50000 ]; then
    echo "Still too large, excluding test files and configs..."
    
    npx repomix \
      --include 'src/**/*.{ts,tsx,js,jsx}' \
      --include 'app/**/*.{ts,tsx,js,jsx}' \
      --include 'README.md' \
      --exclude '**/*.test.*' \
      --exclude '**/*.spec.*' \
      --exclude '**/*.config.*' \
      --exclude '**/test/**' \
      --exclude '**/tests/**' \
      --exclude '**/__tests__/**' \
      --output-file .repomix-minimal.md
      
    FINAL_SIZE=$(wc -c < .repomix-minimal.md)
    FINAL_TOKENS=$((FINAL_SIZE / 4))
    echo "Minimal context: $FINAL_SIZE bytes (~$FINAL_TOKENS tokens)"
  fi
fi
```

### step 3: read and analyze context
```bash
# Use the appropriate context file
if [ -f .repomix-minimal.md ]; then
  echo "Using minimal context (core source only)"
  cat .repomix-minimal.md
  rm .repomix-minimal.md
elif [ -f .repomix-focused.md ]; then
  echo "Using focused context (source code)"
  cat .repomix-focused.md
  rm .repomix-focused.md
else
  echo "Using full context"
  cat .repomix-full.md
  rm .repomix-full.md
fi
```

### step 4: supplementary context
always gather additional key information:
```bash
# Project metadata
[ -f package.json ] && echo "=== package.json ===" && cat package.json
[ -f README.md ] && echo "=== README.md ===" && head -50 README.md
[ -f CLAUDE.md ] && echo "=== CLAUDE.md ===" && cat CLAUDE.md
[ -f .env.example ] && echo "=== .env.example ===" && cat .env.example

# Recent activity
echo "=== Recent Git Activity ==="
git log --oneline -10 2>/dev/null || echo "Not a git repository"
git status --short 2>/dev/null || true
```

## intelligent filtering strategies

### by project type
detect project type and adjust filters:

**javascript/typescript project:**
```bash
--include '**/*.{ts,tsx,js,jsx,mjs,cjs}'
--include '**/*.{json,md,mdx}'
--exclude '**/node_modules/**'
--exclude '**/.next/**'
--exclude '**/dist/**'
```

**python project:**
```bash
--include '**/*.py'
--include '**/*.{md,txt,yml,yaml}'
--exclude '**/__pycache__/**'
--exclude '**/venv/**'
--exclude '**/.pytest_cache/**'
```

**rust project:**
```bash
--include '**/*.rs'
--include '**/*.toml'
--include '**/*.md'
--exclude '**/target/**'
```

### by focus area
when user specifies a path or component:

**specific feature:**
```bash
--include "features/${FEATURE}/**/*"
--include "**/*${FEATURE}*"
```

**api focus:**
```bash
--include '**/api/**/*'
--include '**/routes/**/*'
--include '**/controllers/**/*'
```

**ui focus:**
```bash
--include '**/components/**/*'
--include '**/pages/**/*'
--include '**/styles/**/*'
```

## token management strategy

### progressive refinement levels
1. **full context** (<20k tokens): everything except ignored
2. **source focused** (20-50k tokens): source code only
3. **core only** (50-100k tokens): main source, no tests
4. **minimal** (>100k tokens): critical files only
5. **summary** (fallback): file list + key files

### smart exclusions by size
```bash
# Find large files to exclude
find . -type f -size +100k -not -path "*/node_modules/*" -not -path "*/.git/*" | while read file; do
  echo "Large file detected: $file ($(du -h "$file" | cut -f1))"
done

# Exclude them in repomix
LARGE_FILES=$(find . -type f -size +100k -not -path "*/node_modules/*" -exec basename {} \; | paste -sd "|" -)
npx repomix --exclude "**/{$LARGE_FILES}" ...
```

## output optimization

### structured output format
ensure repomix output includes:
1. file tree structure
2. file contents with clear separators
3. file paths as headers
4. syntax highlighting hints

### context metadata
always include at the top of context:
```markdown
# Project Context Summary
- Total files: X
- Total lines: Y  
- Token estimate: Z
- Primary language: detected
- Framework: detected
- Key patterns: identified
```

## usage in commands

when any .halo command needs context:
```xml
<use_repomix>
  <trigger>user said "use repomix" OR comprehensive context needed</trigger>
  <execute>@file:./components/repomix-context.md</execute>
  <adapt>adjust filters based on task type</adapt>
  <optimize>ensure token limit compliance</optimize>
</use_repomix>
```

## integration example

in any command:
```bash
# Check if repomix requested
if echo "$ARGUMENTS" | grep -i "use repomix" > /dev/null; then
  echo "Gathering comprehensive context with repomix..."
  # Execute this component's full workflow
  source ./components/repomix-context.md
fi
```

## cleanup
always clean up temporary files:
```bash
rm -f .repomix-*.md
```
</repomix_component>