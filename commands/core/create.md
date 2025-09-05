# project creation command

Creates a production‑grade application ecosystem aligned with your standards.

<project_creation_directive>
you are a master project architect with deep knowledge of the user's specific patterns, standards, and conventions. your mission is to take any concept—from a vague idea to detailed specifications—and transform it into a fully-realized, multi-repository project ecosystem that perfectly follows the STANDARDS.md specifications.

<components>
  <use>@file:../../components/xml-transformer.md</use>
  <use>@file:../../components/thinking-blocks.md</use>
  <use>@file:../../components/verification-patterns.md</use>
  <use>@file:../../components/planning-phases.md</use>
  <use>@file:../../components/output-standards.md</use>
  <use>@file:../../components/next-command.md</use>
</components>

<references>
@file:../../.ruler/04-coding-standards.md
@file:../../components/output-standards.md
@file:../../components/planning-phases.md
@file:../../components/thinking-blocks.md
@file:../../CLAUDE.md
@file:../../CLAUDE.md
@file:../../CLAUDE.md
@file:../../CLAUDE.md
@file:../../CLAUDE.mdstructure.md
@file:../../CLAUDE.mdstate_management.md
@file:../../CLAUDE.md
@file:../../CLAUDE.mdservice_architecture.md
@file:../../CLAUDE.mdstructions.md
@file:../../CLAUDE.mdstructure.md
@file:../../CLAUDE.mds.md
@file:../../CLAUDE.mds.md
@file:../../CLAUDE.md
</references>

<deep_initialization_knowledge>
## project structure standards

### 1. repository structure
every project consists of:
- `[projectName]-xyz/` - main turborepo monorepo (web, AI, docs)
- `[projectName]-apple/` - iOS/macOS native app (separate repo)

### 2. turborepo structure
[projectName]-xyz/
- apps/
  - app/              # main Next.js 15+ application
  - ai/               # AI service (Mastra)
  - api/              # webhooks, cron (optional)
- packages/
  - analytics/        # PostHog wrapper
  - api/              # business logic, services, schemas
  - auth/             # Clerk wrapper with middleware
  - cache/            # Redis utilities
  - database/         # Drizzle ORM client & schema
  - design/           # UI components (shadcn/ui)
  - email/            # React Email templates
  - github/           # GitHub integration
  - logger/           # structured logging
  - ai/               # AI service client
  - next-config/      # shared Next.js config
  - rate-limit/       # rate limiting
  - security/         # security middleware
  - seo/              # SEO utilities
  - typescript-config/ # base tsconfig files
  - webhooks/         # webhook utilities
- biome.json            # extends ultracite
- turbo.json
- pnpm-workspace.yaml
- package.json

### 3. route organization
apps/app/src/app/
- (authenticated)/      # protected routes
  - layout.tsx         # auth check wrapper
  - c/[id]/           # chat/conversation pages
  - p/[projectId]/    # project pages
  - settings/         # user settings
  - upgrade/          # billing
- (unauthenticated)/   # public routes
  - layout.tsx        # public wrapper
  - signin/[[...sign-in]]/   # Clerk Elements
  - signup/[[...sign-up]]/   # Clerk Elements
- api/                # API routes (limited use)
  - chat/            # streaming endpoints
  - webhooks/        # external webhooks
  - ws/              # WebSocket
- share/[token]/      # public share pages

### 4. standard scripts
- build: turbo build
- dev: turbo dev
- lint: ultracite lint
- format: ultracite format
- test: turbo test
- analyze: turbo analyze
- boundaries: turbo boundaries
- bump-deps: npx npm-check-updates --deep -u && pnpm install
- migrate: cd packages/database && npx prisma format && npx prisma generate && npx prisma db push
- clean: git clean -xdf node_modules

### 5. AI service structure (apps/ai)
the AI service lives within the monorepo:
- apps/ai/
  - src/
    - mastra/
    - agents/ (Mastra runtime agents)
      - chat/
        - index.ts
        - instructions.xml
        - memory.ts
      - [domain]/
    - tools/
      - attachment-search.ts
      - jina/
      - mcp/
      - output/
    - workflows/
    - lib/
      - attachments/
    - index.ts
- tools/
  - mcp/
- package.json         # type: "module"
- tsconfig.json

### 6. apple project structure
[projectName]-apple/
- Packages/
  - Auth/            # ClerkAuth integration
  - Design/          # SwiftUI components
  - [Name]Networking/ # API client
  - Analytics/       # PostHog
- [projectName]-ios/
  - Assets.xcassets/
  - Resources/
  - Views/
  - ViewModels/
  - Services/
  - Managers/
  - Models/
- [projectName].xcodeproj

### 7. documentation structure (docs/)
documentation at monorepo root:
- docs/
  - .docindex.json       # AI navigation
  - README.md            # overview
- architecture/        # system design
- guides/              # how-to guides
- operations/          # DevOps
- planning/            # roadmaps
- reference/           # API docs
- archive/             # historical
</deep_initialization_knowledge>

<session_memory>
# maintain command context
- load any previous command results
- build on existing project knowledge
- use context from previous operations

# save command results
- store deliverables for other commands
- maintain command history
- preserve project state
</session_memory>

<universal_input_handler>
process $ARGUMENTS to detect and handle:

**URLs detected:**
- fetch and analyze for project inspiration
- extract features and design patterns
- apply insights to project creation

**code blocks detected:**
- parse as project specifications
- extract requirements and constraints
- use as foundation for architecture

**file paths detected:**
- read and analyze specified files
- extract relevant patterns
- apply to current task

**screenshots/images detected:**
- analyze UI/UX patterns
- extract design language
- inform project design decisions

**mixed content:**
- separate by type and process each
- combine insights for task
- apply to command objective
</universal_input_handler>

<prompt_transformation>
# transform stream of consciousness to structured XML

convert user input into structured requirements:
```xml
<project_concept>
  <name>{{extracted_project_name}}</name>
  <description>{{clear_description}}</description>
  <core_features>
    <feature>{{feature_1}}</feature>
    <feature>{{feature_2}}</feature>
  </core_features>
  <technical_requirements>
    <requirement>{{req_1}}</requirement>
    <requirement>{{req_2}}</requirement>
  </technical_requirements>
  <constraints>
    <constraint>{{constraint_1}}</constraint>
  </constraints>
</project_concept>
```

show understanding to user:
## Analyzing project concept

**name**: {{project_name}}  
**type**: {{project_type}}  
**scope**: {{scope_level}}  
**repos**: {{repo_count}}  

### Core features
{{#each features}}
- {{feature}}
{{/each}}

Ready to architect...
</prompt_transformation>

<thinking_process>
<extended_thinking>
  <understanding_phase>
    let me understand what's being asked:
    - project name and concept
    - core features required
    - technical constraints
    - business objectives
    - user experience goals
  </understanding_phase>
  
  <analysis_phase>
    analyzing the requirements:
    - complexity level assessment
    - technology stack selection
    - architecture pattern matching
    - scalability considerations
    - security requirements
  </analysis_phase>
  
  <planning_phase>
    project structure planning:
    - repository organization
    - package dependencies
    - service boundaries
    - data flow design
    - deployment strategy
  </planning_phase>
</extended_thinking>
</thinking_process>

<output_format>
## Project ecosystem created

**name**: {{project_name}}  
**repos**: {{repo_count}}  
**packages**: {{package_count}}  
**services**: {{service_count}}  

### Repositories created
- `{{name}}-xyz` → web platform
- `{{name}}-apple` → iOS/macOS app

### Key features
{{#each features}}
- {{feature}}
{{/each}}

### Tech stack
- Next.js 15 + React 19
- Tailwind CSS v4
- Drizzle + PostgreSQL
- Mastra AI framework
- Clerk authentication

### Quick start
```bash
cd {{name}}-xyz
pnpm install
pnpm dev
```

**next steps**: [BUILD] [DEPLOY] [DOCS]

### Next command

<!-- analyze context and generate perfect next command with PRD -->
<use>@next-command</use>
---
Ecosystem architected. ready to build!
</output_format>

<error_handling>
## Creation warning

**warning**: {{warning_type}}  
**message**: {{warning_message}}  
**suggestion**: {{fix}}  

**adjust parameters?** Y/n
</error_handling>

<task_execution>
## project creation tasks

### phase 1: architecture design
- analyze requirements
- select appropriate patterns
- design data models
- plan service boundaries
- create system diagrams

### phase 2: repository setup
- initialize git repositories
- set up turborepo structure
- configure tooling
- establish ci/cd pipelines
- set up environment configs

### phase 3: core implementation
- scaffold base packages
- implement auth system
- set up database schema
- create API structure
- build ui components

### phase 4: integration
- connect services
- implement data flow
- set up monitoring
- configure analytics
- test integrations

### phase 5: documentation
- generate API docs
- create architecture diagrams
- write setup guides
- document patterns
- prepare onboarding
</task_execution>

<deliverables>
## what gets created

### 1. complete turborepo ([name]-xyz/)
- fully configured monorepo
- all standard packages
- working development environment
- production-ready setup
- comprehensive documentation

### 2. ios/macos app ([name]-apple/)
- xcode project structure
- swiftui components
- networking layer
- auth integration
- app store ready

### 3. project documentation
- architecture overview
- setup instructions
- deployment guides
- API documentation
- contribution guidelines

### 4. development tools
- vs code workspace
- debugging configs
- testing setup
- ci/cd pipelines
- monitoring setup
</deliverables>

<contextual_learning>
## learning from context

### pattern recognition
- identify similar projects
- apply proven patterns
- avoid past mistakes
- optimize for use case

### standards application
- follow STANDARDS.md strictly
- apply all rules
- maintain consistency
- ensure quality

### continuous improvement
- learn from each creation
- refine templates
- optimize processes
- enhance patterns
</contextual_learning>

$ARGUMENTS</project_creation_directive>
