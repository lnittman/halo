# Motion Layer Brief for 3D Art Experience (Framer Motion + Lenis)

## Objective
- Add premium motion design to the single‑screen 3D experience: micro‑interactions, entrance choreography, HUD polish.
- Maintain zero‑scroll; use Lenis input to drive a timeline param without moving the document.
- Respect performance and accessibility across GPU tiers.

## Stack & Tech
- framer‑motion (primary), motion.dev (support)
- @studio-freight/lenis wired as an inertial input driver (no page scroll)
- Tailwind v4 utilities; React 19; Next.js App Router

## Motion System
- Root provider: `app/providers/MotionProvider.tsx` wraps with `LazyMotion` and `ReactLenis`.
- Timeline: map wheel/gesture to a `motionValue` timeline; clamp and spring for tactility.
- State: orchestrate entrance of HUD, labels, and on‑canvas overlays.
- Controls: minimal HUD with quality toggle, pause, and help.

## Patterns to Implement
1) Orchestrated Entrance
   - Staggered reveal of title → subtitle → subtle divider → HUD icons.
   - Ease: `[0.22, 1, 0.36, 1]`; duration 0.6–0.9; spring where appropriate.
2) Magnetic Hover for Buttons
   - Slight follow and spring return; limit translation to avoid layout shift.
3) Idle Attractor Loop
   - After inactivity, introduce barely‑there breathing of HUD opacity/blur for life.
4) Reduced Motion Mode
   - Skip entrance and maintain static states; ensure keyboard navigation.
5) Lenis‑Driven Scrub
   - Wheel updates `timelineValue`; bind parallax or shader intensity to this value.

## Components & Files
- `app/providers/MotionProvider.tsx` — `LazyMotion` + `ReactLenis` root
- `components/UI/HUD.tsx` — minimal overlay (top‑left label, top‑right controls)
- `components/UI/TypewriterText.tsx` — optional title effect using stagger
- `components/UI/MagneticButton.tsx` — tactile CTA/control
- `components/hooks/useTimeline.ts` — wraps Lenis to expose `motionValue`

## Accessibility & Performance
- `useReducedMotion()` gates animations and durations.
- Prefer transform/opacity; avoid layout-affecting properties.
- `will-change` only while animating.
- Keyboard: `Space` pause, `H` quality, `?` help; focus rings preserved.

## Deliverables
- Implement the motion system and minimal HUD with the patterns above.
- Wire the timeline to at least one 3D parameter (intensity/threshold/parallax).
- Provide a short usage README section within `README_experience.md`.

## Quality Gates
- 60fps target on mid‑range; no jank on wheel.
- Reduced motion respected; tab order logical; ARIA labels present.

## Handoff & Reporting
- Follow the motion-expert command `output_format`: list animated elements, durations, files modified, performance metrics.
- Suggest a follow‑up: fine‑tune shader‑driven motions or add audio‑reactive hooks.

---

Implement the motion layer now, then output your report and a perfect next command.
