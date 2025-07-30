# 🎨 Creative Agent Examples & Testing Guide

Examples and test cases for the creative agents (motion-expert, 3d-artist, video-studio).

## 🎬 Video Studio Agent

### Example 1: Product Demo Video
```bash
# Task: Create a product demo for a task management app
Task(
  description="Create product demo video",
  prompt="Create a 30-second product demo video for Squish task manager showcasing the drag-and-drop functionality and real-time collaboration features",
  subagent_type="video-studio"
)
```

Expected behavior:
1. Searches for existing Squish components
2. Imports actual UI components (not mockups)
3. Creates composition showing:
   - Logo animation intro
   - Task cards being dragged
   - Real-time cursor movements
   - Smooth transitions
4. Renders to `~/.video-studio/out/squish-demo.mp4`

### Example 2: Component Showcase
```bash
# Task: Showcase a button component system
Task(
  description="Create button showcase video",
  prompt="Create a video showcasing all button variants, states, and interactions from our design system",
  subagent_type="video-studio"
)
```

Expected output:
- Morphing between button variants
- Hover/active state demonstrations
- Loading states
- Size variations
- Accessibility features highlighted

## 🌊 Motion Expert Agent

### Example 1: Landing Page Animations
```bash
# Task: Add scroll-triggered animations
Task(
  description="Add scroll animations",
  prompt="Add smooth scroll animations to the hero section, including parallax effects for the background, fade-in for text, and a reveal animation for the CTA buttons",
  subagent_type="motion-expert"
)
```

Expected implementation:
```typescript
// Uses Framer Motion + Lenis
- Smooth scroll with Lenis
- Parallax layers with useScroll
- Staggered text animations
- Spring physics for buttons
- Respects prefers-reduced-motion
```

### Example 2: Micro-interactions
```bash
# Task: Add delightful micro-interactions
Task(
  description="Add micro-interactions",
  prompt="Add subtle micro-interactions to all interactive elements: magnetic hover on buttons, smooth transitions on tabs, and gentle bounce on success states",
  subagent_type="motion-expert"
)
```

Expected features:
- Magnetic cursor tracking
- Smooth layout animations
- Success celebrations
- Error shake animations
- Loading skeletons

## 🎭 3D Artist Agent

### Example 1: Ferrofluid Hero Section
```bash
# Task: Create Vercel Ship-style effect
Task(
  description="Create 3D ferrofluid effect",
  prompt="Create an interactive ferrofluid effect like Vercel Ship conference site - black liquid metal that responds to mouse movement with magnetic distortion",
  subagent_type="3d-artist"
)
```

Expected implementation:
```typescript
// Uses React Three Fiber
- Ray marching shader for fluid
- Mouse interaction with distortion
- Metallic material with reflections
- Optimized for 60fps
- Mobile fallback
```

### Example 2: 3D Product Showcase
```bash
# Task: Interactive 3D product viewer
Task(
  description="Create 3D product viewer",
  prompt="Create an interactive 3D showcase for our product with orbit controls, smooth transitions between views, and highlight animations for features",
  subagent_type="3d-artist"
)
```

Expected features:
- OrbitControls for interaction
- Smooth camera transitions
- Feature hotspots
- Loading progress
- Responsive sizing

## 🧪 Testing Methodology

### 1. Component Discovery Test
```yaml
test: "Agent finds and uses existing components"
steps:
  1. Create project with known components
  2. Ask agent to create video/animation
  3. Verify: imports actual components
  4. Verify: preserves design system
```

### 2. Performance Test
```yaml
test: "Animations maintain 60fps"
steps:
  1. Implement complex animation
  2. Profile with Chrome DevTools
  3. Verify: no frame drops
  4. Verify: GPU acceleration used
```

### 3. Accessibility Test
```yaml
test: "Respects user preferences"
steps:
  1. Enable prefers-reduced-motion
  2. Test all animations
  3. Verify: motion is reduced/removed
  4. Verify: functionality preserved
```

### 4. Integration Test
```yaml
test: "Works with existing codebase"
steps:
  1. Add to existing Next.js project
  2. Verify: no conflicts
  3. Verify: follows project patterns
  4. Verify: typescript compiles
```

## 🎯 Quality Checklist

### For Motion Expert
- [ ] Uses project's existing animation library
- [ ] Respects design system timing
- [ ] Implements accessibility controls
- [ ] Optimizes for performance
- [ ] Provides fallbacks

### For 3D Artist
- [ ] Manages poly count
- [ ] Implements LOD (Level of Detail)
- [ ] Uses proper lighting
- [ ] Handles different GPUs
- [ ] Mobile-responsive

### For Video Studio
- [ ] Imports real components
- [ ] Maintains brand consistency
- [ ] Optimizes file size
- [ ] Renders multiple formats
- [ ] Includes captions/accessibility

## 🚀 Advanced Examples

### Combining Agents
```bash
# Create a complete landing page experience
# 1. First, add 3D hero section
Task(
  description="Add 3D hero",
  prompt="Create an interactive 3D globe showing real-time user activity",
  subagent_type="3d-artist"
)

# 2. Then add scroll animations
Task(
  description="Add scroll effects",
  prompt="Add smooth scroll with parallax layers and reveal animations",
  subagent_type="motion-expert"
)

# 3. Finally, create a demo video
Task(
  description="Create demo video",
  prompt="Create a video showcasing the new landing page with all animations",
  subagent_type="video-studio"
)
```

### Real-World Scenarios

#### Scenario 1: Product Launch
```typescript
// Requirements:
// - 3D product visualization
// - Smooth interactions
// - Launch video

// Step 1: 3D Product Model
const product3D = await Task({
  description: "Create 3D product",
  prompt: "Create photorealistic 3D model of our headphones with material variations",
  subagent_type: "3d-artist"
});

// Step 2: Interactive Features
const interactions = await Task({
  description: "Add interactions",
  prompt: "Add smooth rotation, color selection, and exploded view animations",
  subagent_type: "motion-expert"
});

// Step 3: Marketing Video
const video = await Task({
  description: "Create launch video",
  prompt: "Create 60-second launch video showcasing all product features with music sync",
  subagent_type: "video-studio"
});
```

#### Scenario 2: Dashboard Enhancement
```typescript
// Requirements:
// - Data visualizations
// - Smooth transitions
// - Tutorial video

// Implementation flow...
```

## 📊 Expected Outputs

### Motion Expert Output
```markdown
# ✅ Animation System Implemented

**Library**: Framer Motion + Lenis
**Components**: 8 enhanced
**Performance**: 60fps maintained
**Bundle Impact**: +18kb

## Animations Added
- Hero parallax system
- Scroll-triggered reveals
- Magnetic buttons
- Page transitions

[Code examples...]
```

### 3D Artist Output
```markdown
# 🎨 3D Scene Created

**Framework**: React Three Fiber
**Polygons**: 15k optimized
**Performance**: 60fps target
**Features**: Mouse interaction

## Implementation
- Custom shaders
- Optimized geometry
- Mobile fallback
- Loading states

[Code examples...]
```

### Video Studio Output
```markdown
# 🎬 Video Rendered

**Duration**: 30 seconds
**Resolution**: 1920x1080
**Format**: MP4 (H.264)
**File Size**: 12MB

## Scenes Created
- Logo animation (0-3s)
- Product showcase (3-20s)
- Feature highlights (20-27s)
- CTA (27-30s)

Output: ~/.video-studio/out/product-demo.mp4
```

## 🔍 Debugging Tips

### Common Issues

1. **Performance Problems**
   - Check Chrome DevTools Performance tab
   - Look for: Layout thrashing, paint storms
   - Solution: Use transform-only animations

2. **Component Import Fails**
   - Verify relative paths
   - Check for SSR compatibility
   - Solution: Dynamic imports with ssr: false

3. **Build Size Too Large**
   - Analyze with @next/bundle-analyzer
   - Check for duplicate dependencies
   - Solution: Code splitting, lazy loading

4. **Animation Jank**
   - Profile with React DevTools
   - Check for state updates during animation
   - Solution: useCallback, useMemo, RAF

---

*These examples demonstrate the full capabilities of creative agents. Test in real projects for best results.*