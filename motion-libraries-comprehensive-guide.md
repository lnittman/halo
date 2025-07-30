# Motion/Animation Libraries Comprehensive Guide

This guide covers powerful motion and animation libraries for modern web development, with a focus on integration patterns for Next.js and React projects.

## Table of Contents

1. [Motion (motion.dev)](#motion-motiondev)
2. [Motion Primitives](#motion-primitives)
3. [Lenis](#lenis)
4. [Darkroom Engineering Libraries](#darkroom-engineering-libraries)
5. [Integration Patterns](#integration-patterns)
6. [Performance Considerations](#performance-considerations)

---

## Motion (motion.dev)

### Overview

Motion is a modern animation library that provides a unique hybrid engine combining browser performance with JavaScript flexibility. It's the evolution of Framer Motion, offering both vanilla JavaScript and framework-specific implementations.

### Key Features

- **Hybrid Engine**: Combines hardware-accelerated browser animations with JavaScript flexibility
- **Tiny Bundle Size**: Core animate function is just 2.3kb
- **Framework Support**: Works with vanilla JS, React, and Vue
- **Gesture Support**: Built-in hover, tap, focus, and drag gestures
- **Layout Animations**: Industry-leading layout animation engine
- **Scroll Animations**: Both scroll-triggered and scroll-linked animations

### Installation

```bash
# Package manager
npm install motion

# For React projects
import { motion } from "motion/react"

# For vanilla JS
import { animate, scroll } from "motion"
```

### Basic Usage

#### Vanilla JavaScript

```javascript
import { animate } from "motion"

// Animate by selector
animate(".box", { rotate: 360 }, { duration: 2 })

// Animate elements directly
const boxes = document.querySelectorAll(".box")
animate(boxes, { scale: [0.5, 1], opacity: [0, 1] }, { 
  delay: stagger(0.1),
  ease: "spring"
})
```

#### React Usage

```jsx
import { motion } from "motion/react"

function Component() {
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.5 }}
      animate={{ opacity: 1, scale: 1 }}
      whileHover={{ scale: 1.1 }}
      whileTap={{ scale: 0.95 }}
      transition={{ type: "spring", stiffness: 300 }}
    >
      Interactive Element
    </motion.div>
  )
}
```

### Advanced Features

#### Scroll Animations

```jsx
// Scroll-triggered
<motion.div
  initial={{ opacity: 0, y: 50 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, amount: 0.3 }}
/>

// Scroll-linked
import { useScroll } from "motion/react"

function ScrollProgress() {
  const { scrollYProgress } = useScroll()
  
  return (
    <motion.div 
      style={{ scaleX: scrollYProgress }}
      className="progress-bar"
    />
  )
}
```

#### Layout Animations

```jsx
// Animate layout changes
<motion.div layout>
  {/* Content that changes size */}
</motion.div>

// Shared layout animations
<motion.div layoutId="shared-element">
  {/* Element that animates between components */}
</motion.div>
```

#### Exit Animations

```jsx
import { AnimatePresence } from "motion/react"

<AnimatePresence>
  {isVisible && (
    <motion.div
      key="modal"
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    />
  )}
</AnimatePresence>
```

---

## Motion Primitives

### Overview

Motion Primitives is a UI kit providing beautifully designed, ready-to-use animated components built with Motion (Framer Motion) and Tailwind CSS. It's designed for engineers and designers who want to implement sophisticated animations quickly.

### Key Features

- **Pre-built Components**: Ready-to-use animated UI components
- **Customizable**: Built with Tailwind CSS for easy customization
- **Open Source**: MIT licensed with regular updates
- **CLI Tool**: Easy installation of components
- **TypeScript Support**: Full type safety

### Installation

```bash
# Install the CLI
npm install -g @motion-primitives/cli

# Add components to your project
npx motion-primitives add [component-name]
```

### Component Examples

#### Text Effects

```jsx
// Typewriter effect
import { Typewriter } from "@/components/motion-primitives/typewriter"

<Typewriter
  text="Animate your ideas with motion-primitives"
  duration={0.1}
  className="text-4xl font-bold"
/>
```

#### Interactive Cards

```jsx
// Tilt card effect
import { TiltCard } from "@/components/motion-primitives/tilt-card"

<TiltCard className="w-64 h-96">
  <div className="p-6">
    <h3>Interactive Card</h3>
    <p>Responds to mouse movement</p>
  </div>
</TiltCard>
```

#### Scroll Effects

```jsx
// Scroll-triggered animations
import { ScrollReveal } from "@/components/motion-primitives/scroll-reveal"

<ScrollReveal
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.6 }}
>
  <div>Content reveals on scroll</div>
</ScrollReveal>
```

### Creating Custom Primitives

```jsx
import { motion } from "motion/react"
import { cn } from "@/lib/utils"

export function CustomPrimitive({ children, className }) {
  return (
    <motion.div
      className={cn("relative", className)}
      initial={{ scale: 0.9, opacity: 0 }}
      animate={{ scale: 1, opacity: 1 }}
      whileHover={{ scale: 1.05 }}
      transition={{ type: "spring", stiffness: 400 }}
    >
      {children}
    </motion.div>
  )
}
```

---

## Lenis

### Overview

Lenis is a lightweight, robust, and performant smooth scroll library designed by Darkroom Engineering. It provides native-like smooth scrolling with excellent performance and minimal configuration.

### Key Features

- **Lightweight**: Small bundle size with zero dependencies
- **Performant**: Optimized for 60fps scrolling
- **Touch Support**: Native-like touch scrolling behavior
- **Framework Agnostic**: Works with any framework or vanilla JS
- **Extensible**: Plugin system for additional features

### Installation

```bash
npm install lenis

# For React
npm install @lenis/react
```

### Basic Setup

```javascript
import Lenis from 'lenis'

// Initialize Lenis
const lenis = new Lenis({
  duration: 1.2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  orientation: 'vertical',
  gestureOrientation: 'vertical',
  smoothWheel: true,
  wheelMultiplier: 1,
  touchMultiplier: 2,
  infinite: false,
})

// Animation loop
function raf(time) {
  lenis.raf(time)
  requestAnimationFrame(raf)
}

requestAnimationFrame(raf)
```

### React Integration

```jsx
import { ReactLenis, useLenis } from '@lenis/react'

function App() {
  return (
    <ReactLenis root>
      <div className="content">
        {/* Your app content */}
      </div>
    </ReactLenis>
  )
}

// Using the hook
function ScrollComponent() {
  const lenis = useLenis(({ scroll }) => {
    console.log(scroll) // Current scroll position
  })
  
  return <div>Scroll position tracked</div>
}
```

### Advanced Configuration

```javascript
const lenis = new Lenis({
  // Wrapper element
  wrapper: document.querySelector('.wrapper'),
  
  // Content element
  content: document.querySelector('.content'),
  
  // Smooth scroll options
  lerp: 0.1, // Linear interpolation intensity
  duration: 1.2, // Animation duration
  
  // Orientation
  orientation: 'vertical', // vertical, horizontal
  gestureOrientation: 'vertical', // vertical, horizontal, both
  
  // Touch options
  syncTouch: false, // Mimic touch scroll
  syncTouchLerp: 0.075,
  touchInertiaExponent: 1.7,
  
  // Scroll behavior
  infinite: false, // Infinite scrolling
  overscroll: true, // Allow overscroll
  
  // Events
  prevent: (node) => node.classList.contains('no-smooth'),
  virtualScroll: (e) => {
    // Modify scroll events
    e.deltaY *= 0.5 // Slow down scroll
  }
})
```

### GSAP Integration

```javascript
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

// Sync Lenis with GSAP
lenis.on('scroll', ScrollTrigger.update)

gsap.ticker.add((time) => {
  lenis.raf(time * 1000)
})

gsap.ticker.lagSmoothing(0)
```

### Scroll Controls

```javascript
// Scroll to specific position
lenis.scrollTo(1000, {
  offset: 0,
  immediate: false,
  duration: 2,
  easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  lerp: undefined,
  onComplete: () => console.log('Scrolled!')
})

// Scroll to element
lenis.scrollTo('#section', {
  offset: -100, // Offset from top
  duration: 1.5
})

// Stop/start scrolling
lenis.stop()
lenis.start()

// Get scroll info
console.log(lenis.scroll) // Current scroll
console.log(lenis.limit) // Max scroll
console.log(lenis.velocity) // Scroll velocity
console.log(lenis.direction) // 1 or -1
console.log(lenis.progress) // 0 to 1
```

---

## Darkroom Engineering Libraries

### Satus - Next.js Starter

Advanced Next.js App Router starter for content-driven sites.

```bash
npx create-next-app@latest my-app --example https://github.com/darkroomengineering/satus
```

**Features:**
- Optimized for content sites
- Built-in animation setup
- Performance optimized
- SEO ready

### Tempus - RAF Manager

Single requestAnimationFrame loop for your entire app.

```javascript
import Tempus from '@darkroom.engineering/tempus'

const tempus = new Tempus()

// Add a task
tempus.add((time, deltaTime) => {
  // Animation logic
}, 0) // Priority

// Remove a task
tempus.remove(task)
```

### Hamo - React Hooks Collection

Collection of useful React hooks for animations and interactions.

```jsx
import { useWindowSize, useMousePosition } from '@darkroom.engineering/hamo'

function Component() {
  const { width, height } = useWindowSize()
  const { x, y } = useMousePosition()
  
  return (
    <div>
      Window: {width}x{height}
      Mouse: {x}, {y}
    </div>
  )
}
```

---

## Integration Patterns

### Next.js App Router Setup

```jsx
// app/components/smooth-scroll-provider.jsx
'use client'

import { ReactLenis } from '@lenis/react'

export function SmoothScrollProvider({ children }) {
  return (
    <ReactLenis root options={{
      lerp: 0.1,
      duration: 1.5,
      smoothWheel: true,
    }}>
      {children}
    </ReactLenis>
  )
}

// app/layout.jsx
import { SmoothScrollProvider } from '@/components/smooth-scroll-provider'

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <SmoothScrollProvider>
          {children}
        </SmoothScrollProvider>
      </body>
    </html>
  )
}
```

### Combining Motion + Lenis

```jsx
import { motion, useScroll, useTransform } from 'motion/react'
import { useLenis } from '@lenis/react'

function ParallaxSection() {
  const { scrollYProgress } = useScroll()
  const y = useTransform(scrollYProgress, [0, 1], [0, -100])
  
  useLenis(({ scroll }) => {
    // Additional scroll logic
  })
  
  return (
    <motion.div
      style={{ y }}
      className="parallax-element"
    >
      Smooth parallax with Lenis + Motion
    </motion.div>
  )
}
```

### Motion Primitives + Custom Animations

```jsx
import { motion } from 'motion/react'
import { cn } from '@/lib/utils'

// Extend Motion Primitive
export function EnhancedCard({ children, className, ...props }) {
  return (
    <motion.div
      className={cn("relative overflow-hidden", className)}
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      whileHover={{ y: -5 }}
      transition={{ type: "spring", stiffness: 300 }}
      {...props}
    >
      <motion.div
        className="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-500 opacity-0"
        whileHover={{ opacity: 0.1 }}
        transition={{ duration: 0.3 }}
      />
      {children}
    </motion.div>
  )
}
```

---

## Performance Considerations

### Motion Optimization

```jsx
// Use LazyMotion for smaller bundle
import { LazyMotion, domAnimation } from "motion/react"

function App() {
  return (
    <LazyMotion features={domAnimation}>
      {/* Your app */}
    </LazyMotion>
  )
}

// Disable animations on low-end devices
import { useReducedMotion } from "motion/react"

function Component() {
  const prefersReducedMotion = useReducedMotion()
  
  return (
    <motion.div
      animate={prefersReducedMotion ? {} : { x: 100 }}
    />
  )
}
```

### Lenis Performance

```javascript
// Optimize for performance
const lenis = new Lenis({
  lerp: 0.1, // Higher = less smooth but better performance
  wheelMultiplier: 1,
  touchMultiplier: 2,
  normalizeWheel: true,
  smoothTouch: false, // Disable on mobile for better performance
})

// Conditional smooth scroll
const isMobile = window.innerWidth < 768
if (!isMobile) {
  lenis.start()
}
```

### Best Practices

1. **Use CSS transforms** over positional properties
2. **Batch animations** using Motion's `stagger` or Lenis's RAF
3. **Lazy load** heavy animations
4. **Respect prefers-reduced-motion**
5. **Test on low-end devices**
6. **Monitor frame rates** during development

### Debugging

```javascript
// Motion debugging
import { motion } from "motion/react"

// Enable visual debugging
motion.config.dev = process.env.NODE_ENV === 'development'

// Lenis debugging
lenis.on('scroll', ({ scroll, limit, velocity, direction, progress }) => {
  console.log({
    scroll,
    limit,
    velocity,
    direction,
    progress
  })
})
```

---

## Resources

### Official Documentation
- [Motion Docs](https://motion.dev/docs)
- [Motion Examples](https://motion.dev/examples)
- [Lenis Documentation](https://lenis.darkroom.engineering/)
- [Motion Primitives](https://motion-primitives.com/)

### GitHub Repositories
- [Motion](https://github.com/motiondivision/motion)
- [Motion Primitives](https://github.com/ibelick/motion-primitives)
- [Lenis](https://github.com/darkroomengineering/lenis)
- [Darkroom Engineering](https://github.com/darkroomengineering)

### Community Resources
- [Motion Discord](https://motion.dev/discord)
- [Darkroom Engineering Twitter](https://twitter.com/darkroomdevs)

This guide provides a comprehensive overview of modern motion libraries for web development. Each library offers unique strengths - Motion for declarative animations, Motion Primitives for pre-built components, and Lenis for smooth scrolling. Combined, they provide a powerful toolkit for creating engaging, performant web experiences.