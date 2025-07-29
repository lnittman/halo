# Technical Design System Audit Command

Comprehensive client-side design documentation with technical implementation details and reference analysis.

<design_system_directive>
You are tasked with conducting a thorough technical audit of the client-side codebase to create comprehensive design system documentation. This includes analyzing existing patterns, documenting screenshot references, and creating a complete technical design system.

<components>
  <use>@thinking-blocks</use>
  <use>@xml-transformer</use>
  <use>@verification-patterns</use>
</components>

<references>
@file:~/Developer/docs/apps/docs.md
@file:~/Developer/docs/apps/patterns.md#design-system
@file:~/Developer/docs/inspo/dieter-rams/color.md
@file:~/Developer/docs/inspo/te/te.md
</references>

<context_awareness>
# Leverage conversation context
Understand from previous discussion:
- Project type and structure
- Design preferences mentioned
- Implementation patterns in use
- Quality standards established

# Build on previous insights
- Apply discovered patterns
- Maintain consistency
- Reference earlier decisions
</context_awareness>

<universal_input_handler>
Process $ARGUMENTS to detect and handle:

**URLs Detected:**
- Fetch and analyze design systems
- Extract component patterns and tokens
- Apply insights to audit

**Code Blocks Detected:**
- Parse as component examples
- Extract styling patterns
- Document implementation approaches

**File Paths Detected:**
- Read and analyze specified files
- Extract relevant patterns
- Apply to current task

**Screenshots/Images Detected:**
- Analyze UI components and patterns
- Extract design tokens and spacing
- Document visual references

**Mixed Content:**
- Separate by type and process each
- Combine insights for task
- Apply to command objective
</universal_input_handler>

<prompt_transformation>
<!-- Use enhanced XML transformer component -->
<input_analysis>
  <raw_input>$ARGUMENTS</raw_input>
  <detected_elements>
    <!-- Auto-detect URLs, code blocks, files, images, natural language -->
  </detected_elements>
</input_analysis>

<semantic_extraction>
  <design_intent>
    <primary>{{audit|document|analyze|improve}}</primary>
    <scope>{{components|tokens|patterns|full_system}}</scope>
    <technical_depth>{{surface|standard|deep_dive}}</technical_depth>
  </design_intent>
  
  <context>
    <design_maturity>{{none|basic|established|mature}}</design_maturity>
    <technology>{{css|tailwind|css_in_js|mixed}}</technology>
    <team_size>{{solo|small|large}}</team_size>
  </context>
  
  <audit_focus>
    <priorities>
      {{#if components_mentioned}}
      - Component architecture and composition
      {{/if}}
      {{#if styles_mentioned}}
      - Design token extraction and organization
      {{/if}}
      {{#if accessibility_mentioned}}
      - WCAG compliance and a11y patterns
      {{/if}}
      {{#if performance_mentioned}}
      - Rendering performance and optimization
      {{/if}}
    </priorities>
  </audit_focus>
</semantic_extraction>

<transformation_feedback>
## 🔄 Understanding Your Design Request

**Interpreted as**: {{design_action}} for {{scope}}
**Technical Depth**: {{technical_depth}}
**Primary Focus**: {{main_area_of_interest}}

**Detected Context**:
{{#if urls}}
- Reference materials: {{url_count}} sources
{{/if}}
{{#if code_blocks}}
- Code samples: {{code_count}} examples
{{/if}}
{{#if images}}
- Visual references: {{image_count}} screenshots/mockups
{{/if}}

Proceeding with comprehensive design system analysis...
</transformation_feedback>
</prompt_transformation>

<thinking_process>
<!-- Use enhanced thinking blocks component -->
<extended_thinking>
  <understanding_phase>
    <user_intent>
    Let me understand what you're asking for:
    - Primary goal: Audit and document the design system
    - Context: Technical implementation of UI components
    - Constraints: Must be comprehensive and actionable
    - Success looks like: Complete design system documentation
    </user_intent>
    
    <assumptions>
    I'm making these assumptions:
    - Design consistency impacts development speed
    - Technical documentation is as important as visual
    - Existing patterns should be identified and leveraged
    - Screenshots and examples enhance understanding
    </assumptions>
  </understanding_phase>
  
  <analysis_phase>
    <current_state>
    Current situation:
    - Evaluating existing design patterns
    - Identifying component architecture
    - Analyzing styling approaches
    </current_state>
    
    <options_considered>
    Possible audit approaches:
    1. Component inventory: Catalog all UI elements
    2. Token extraction: Focus on design primitives
    3. Holistic review: Complete system analysis
    </options_considered>
    
    <decision_rationale>
    Choosing approach based on:
    - Current design system maturity
    - Technical stack and constraints
    - Team needs and workflows
    </decision_rationale>
  </analysis_phase>
  
  <planning_phase>
    <execution_plan>
    Here's my design audit plan:
    1. Scan codebase for UI components
    2. Extract design tokens and patterns
    3. Analyze component architecture
    4. Document implementation approaches
    5. Create comprehensive design guide
    </execution_plan>
    
    <risk_mitigation>
    Potential issues and mitigations:
    - Risk: Inconsistent patterns → Mitigation: Create unified system
    - Risk: Performance issues → Mitigation: Document optimizations
    - Risk: Accessibility gaps → Mitigation: Include a11y guidelines
    </risk_mitigation>
    
    <success_metrics>
    How we'll know the audit succeeded:
    - [ ] All components documented
    - [ ] Design tokens extracted
    - [ ] Implementation patterns clear
    - [ ] Accessibility covered
    </success_metrics>
  </planning_phase>
  
  <analytical_thinking>
    <data_synthesis>
    Design patterns discovered:
    - Component composition strategies
    - Styling methodologies
    - State management patterns
    - Animation approaches
    </data_synthesis>
    
    <gap_analysis>
    Missing design elements:
    - Undocumented components
    - Inconsistent spacing
    - Missing dark mode support
    - Accessibility issues
    </gap_analysis>
  </analytical_thinking>
  
  <pattern_recognition>
  Design patterns to document:
  - Color system and theming
  - Typography scale
  - Spacing and layout grid
  - Component variants
  - Interactive states
  </pattern_recognition>
  
  <critical_evaluation>
    <potential_issues>
    What could go wrong:
    - Over-engineering the system
    - Creating too rigid guidelines
    - Missing edge cases
    </potential_issues>
    
    <oversimplifications>
    What I might be oversimplifying:
    - Component complexity and variants
    - Cross-browser compatibility
    - Performance implications
    </oversimplifications>
    
    <skeptical_review>
    A skeptical reviewer would point out:
    - "Is this level of documentation maintainable?"
    - "Are we solving real problems?"
    - "Will developers actually use this?"
    </skeptical_review>
    
    <confidence_assessment>
    My confidence level: High
    Because: Clear patterns for design systems exist
    Areas of uncertainty: Adoption and maintenance
    </confidence_assessment>
  </critical_evaluation>
  
  <thinking_summary>
  ## 🧠 My Thinking Process
  
  **Understanding**: Auditing design system for technical documentation
  
  **Analysis**: Identifying patterns, gaps, and opportunities
  
  **Approach**: Comprehensive scan with actionable documentation
  
  **Next Steps**: Analyze codebase and create design system guide
  </thinking_summary>
</extended_thinking>
</thinking_process>

<analysis_phase>
Launch analysis tasks to comprehensively audit the design system:

**Task 1: Component Architecture Analysis**
- Map all UI components and their relationships
- Identify component composition patterns
- Analyze prop interfaces and type definitions
- Document component dependencies
- Assess component reusability and modularity

**Task 2: Styling System Audit**
- Analyze CSS/styling methodology (CSS-in-JS, Tailwind, etc.)
- Extract color variables and usage patterns
- Document spacing and sizing systems
- Map typography scales and font usage
- Identify animation and transition patterns

**Task 3: Screenshot Reference Analysis**
- Find all screenshot references in the codebase
- Analyze UI patterns copied from other apps
- Document inspiration sources
- Identify adaptation strategies
- Map reference to implementation

**Task 4: Interaction Pattern Documentation**
- Catalog all interaction states (hover, focus, active)
- Document gesture and touch interactions
- Map keyboard navigation patterns
- Analyze loading and error states
- Review transition and animation logic

**Task 5: Accessibility & Performance Audit**
- Check ARIA implementation patterns
- Analyze color contrast ratios
- Document keyboard navigation
- Review responsive breakpoints
- Assess rendering performance patterns

**Task 6: Design Token Extraction**
- Extract all design variables
- Map token relationships
- Identify token categories
- Document token usage patterns
- Create token hierarchy
</analysis_phase>

<documentation_requirements>
Create comprehensive design documentation including:

### 1. Design System Architecture
# Design System Architecture

## System Overview
- **Methodology**: [Atomic Design, Component-Based, etc.]
- **Technology**: [Tailwind, Emotion, styled-components, etc.]
- **Organization**: [How components are structured]

## Component Hierarchy
- components/
  - primitives/     # Base building blocks
    - Box
    - Text
    - ...
  - elements/       # Single-purpose components
    - Button
    - Input
    - ...
  - patterns/       # Composite components
    - Card
    - Modal
    - ...
  - layouts/        # Page-level components
    - Header
    - Sidebar
    - ...
  - templates/      # Full page templates

## Composition Patterns
[How components combine and compose]

## State Management
[How component state is handled]

### 2. Component Documentation
```markdown
# Component Library

## Button Component

### Overview
[Purpose and usage guidelines]

### Variants
- **Primary**: [Usage and visual description]
- **Secondary**: [Usage and visual description]
- **Ghost**: [Usage and visual description]

### Props Interface
**ButtonProps interface**:
- variant?: 'primary' | 'secondary' | 'ghost'
- size?: 'sm' | 'md' | 'lg'
- disabled?: boolean
- loading?: boolean
- onClick?: () => void
- children: ReactNode

### Usage Examples
**Primary action**:
Button with variant="primary" and onClick={handleSubmit}

**Loading state**:
Button with loading prop showing "Processing..."

### Implementation Details
[Technical implementation notes]

### Accessibility
- Keyboard support: [Details]
- Screen reader: [Details]
- Focus management: [Details]
```

### 3. Design Tokens
```markdown
# Design Token System

## Color Tokens
### Primitive Colors
**Color palette**:
- Gray scale: 50 (#fafafa) through 900 (#18181b)
- Brand colors:
  - Primary: #3b82f6
  - Secondary: #8b5cf6

### Semantic Colors
**Background colors**:
- Primary: var(--gray-50)
- Secondary: var(--gray-100)

**Text colors**:
- Primary: var(--gray-900)
- Secondary: var(--gray-600)

**Border colors**:
- Default: var(--gray-200)
- Focus: var(--brand-primary)

## Spacing Tokens
**Spacing scale**:
- px: 1px
- 0.5: 0.125rem (2px)
- 1: 0.25rem (4px)
- 2: 0.5rem (8px)
- [Full scale continues...]

## Typography Tokens
[Font families, sizes, weights, line-heights]

## Animation Tokens
[Durations, easings, keyframes]
```

### 4. Reference Documentation
```markdown
# UI/UX References

## Screenshot References

### [Feature/Component Name]
**Source**: [App/Website Name]
**Screenshot**: ![Reference](path/to/screenshot.png)
**What We Borrowed**: 
- [Specific element or pattern]
- [Another element]

**Our Implementation**:
- How we adapted it
- What we changed
- Why we made those changes

### [Another Feature]
[Same structure]

## Design Inspiration Sources
1. **[App/Website]**: [What we admire about it]
2. **[App/Website]**: [What we admire about it]

## Pattern Library
### [Pattern Name]
- **Seen in**: [Where this pattern appears]
- **Why it works**: [Analysis]
- **Our version**: [How we implement it]
```

### 5. Technical Implementation Guide
```markdown
# Implementation Guide

## Styling Architecture

### CSS-in-JS Setup
**Theme configuration structure**:
- colors object
- spacing object
- typography object
- breakpoints object

**Component styling pattern**:
- Use styled-components with theme access
- Apply theme tokens for consistency
- Handle variant props for different styles

### Tailwind CSS v4 Configuration
**Global styles setup**:
- Import tailwindcss in globals.css
- Define inline theme with design tokens
- Map colors and spacing to design system

## Component Patterns

### Compound Components
**Pattern implementation**:
- Main Card component as container
- Card.Header for header content
- Card.Body for main content
- Card.Footer for footer actions

### Render Props
[Pattern examples]

### Custom Hooks
[UI-related hooks]

## Performance Patterns
- Code splitting strategies
- Lazy loading components
- Memoization patterns
- Virtual scrolling
```

### 6. Accessibility Guidelines
```markdown
# Accessibility Standards

## Color Contrast
- Text contrast ratios
- Interactive element contrast
- Error state visibility

## Keyboard Navigation
- Tab order management
- Focus indicators
- Keyboard shortcuts

## Screen Reader Support
- ARIA labels
- Live regions
- Semantic HTML

## Motion Preferences
- Respecting prefers-reduced-motion
- Alternative interactions
```
</documentation_requirements>

<output_structure>
## 🎨 Design System Audit: [ProjectName]

### 📊 System Overview
- **Component Count**: [Number] components
- **Design Tokens**: [Number] tokens defined
- **Styling Method**: [Tailwind/CSS-in-JS/etc.]
- **Accessibility Score**: [A/B/C grade]
- **Performance Grade**: [Assessment]

### 🏗️ Architecture Summary
[Visual representation of component hierarchy]

### 🎯 Key Findings

#### Strengths 💪
1. **[Pattern]**: [Why it works well]
2. **[Pattern]**: [Why it works well]
3. **[Pattern]**: [Why it works well]

#### Improvements Needed 🔧
1. **[Issue]**: [Impact and solution]
2. **[Issue]**: [Impact and solution]
3. **[Issue]**: [Impact and solution]

### 📸 Reference Analysis
**Screenshot References Found**: [Number]
**Primary Inspirations**:
1. [App/Website] - [What patterns]
2. [App/Website] - [What patterns]

design tokens ▸
{{#each token_categories}}
  ▪ {{category}}: ▪▪▪ {{count}} tokens
{{/each}}

╔═══════════════════════════════╗
║  ★ ☆ ★  DOCS CREATED   ★ ☆ ★ ║
╠═══════════════════════════════╣
║ 📁 {{projectName}}-docs/design/   ║
╚═══════════════════════════════╝

files generated ▸
  ✓ component architecture guide
  ✓ complete component library
  ✓ design token reference
  ✓ screenshot reference catalog
  ✓ implementation patterns
  ✓ accessibility guidelines

### 🚀 Immediate Actions
1. **Critical**: [Most important fix]
2. **High Priority**: [Important improvement]
3. **Quick Win**: [Easy enhancement]

strategic roadmap ▸

short term (this sprint) ▸
{{#each short_term}}
  ▫ {{task}}
{{/each}}

medium term (next month) ▸
{{#each medium_term}}
  ▫ {{task}}
{{/each}}

long term (quarterly) ▸
{{#each long_term}}
  ▫ {{task}}
{{/each}}

### 🦋 metrics
**coverage**: {{pct}}% 🐢🐢🐢🐢🔴  
**tokens**: {{pct}}% 🐢🐢🐢🐢🐢  
**a11y**: {{pct}}% 🐢🐢🐢🐢🔴  
**bundle**: {{size}}kb 🐆

⚠️ caveats & limitations ▸
- assumptions made: 
  - design patterns are consistent enough to systematize
  - technical implementation reflects design intent
  - screenshot references are up-to-date and relevant
  - team will adopt and maintain the system
- not addressed: 
  - cross-browser rendering differences
  - device-specific UI adaptations
  - internationalization and RTL support
  - dynamic theming and user customization
- technical debt: 
  - may not catch all edge cases and variants
  - performance metrics are estimates
  - accessibility audit may miss nuanced issues
- alternative approaches: 
  - using established design systems (material, ant, etc.)
  - hiring dedicated design system team
  - progressive enhancement without full system
  - design tokens as a service (specify, style dictionary)

---
*Design system documented. Ready for scaling and optimization!*

next ▸ [BRAND] [BUILD] [VISION] [DOCS]
</output_structure>

<execution_notes>
1. Be thorough but prioritize actionable insights
2. Document both what exists and what's missing
3. Include code examples from actual implementation
4. Reference screenshot sources with context
5. Create reusable patterns and anti-patterns
6. Focus on technical implementation details
7. Provide migration paths for improvements
8. Consider both developer and designer needs
</execution_notes>
</design_system_directive>

$ARGUMENTS