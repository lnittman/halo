# Zero‑Scroll Single‑Screen 3D Art Experience (R3F + Motion + Lenis)

## Objective
- Build a full‑screen, single‑page, no‑scroll web experience: a living 3D artwork with cinematic polish.
- Feel: avant‑garde minimalism; liquid metal/iridescent; premium interactive art installation.
- Use latest stack and patterns; ship as production‑grade.

## Stack & Tech (align with workspace standards)
- App: Next.js 15 App Router, React 19, TypeScript, Tailwind v4
- 3D: three.js, @react-three/fiber, @react-three/drei, @react-three/postprocessing
- Motion: framer‑motion (primary), motion.dev (support)
- Input/Scroll: @studio-freight/lenis (use wheel/gesture as timeline input; no page scroll)
- Utilities: @pmndrs/detect-gpu (quality tiers), leva (dev‑only), Sentry/PostHog hooks ready
- Performance: WebGL2 preferred; graceful degradation; mobile-safe

## Experience Constraints
- No scroll. Body is overflow-hidden; layout is 100vw x 100dvh.
- Single screen composition with subtle UI chrome; no page transitions.
- Mouse/trackpad wheel maps to a time/timeline parameter via Lenis (smooth inertial feel) despite no document scrolling.
- Pointer drives subtle parallax and camera micro‑dolly; space toggles pause; H toggles high/low quality.
- Respect prefers-reduced-motion: freeze timeline at a tasteful still, lower effects.

## Concept (choose 1 and execute with originality)
1) Ferrofluid Monolith
   - Ray-marched SDF core with magnetic spikes; metallic sheen; HDRI reflections.
   - Wheel input modulates “magnetic field strength” and spike resonance.
2) Iridescent Metaball Nebula
   - MarchingCubes metaballs with thin‑film interference shader; soft bloom + vignette.
   - Pointer proximity warps field; wheel shifts color dispersion and threshold.
3) Particle Interference Hologram
   - 50–150k GPU particles (instanced or custom shader) forming interference patterns.
   - Audio-reactive optional; otherwise procedural beat. Wheel scrubs scene states.

## Visual Direction
- Palette: onyx/graphite base, iridescent accents (teal→violet), subtle film grain.
- Lighting: single key rim + environment; avoid flatness; maintain depth cues.
- Post: gentle Bloom, SMAA/FXAA, ChromaticAberration (very subtle), Vignette; configurable per GPU tier.
- Typography: micro label only (top‑left), unobtrusive; hide on idle.

## Interaction & Motion
- Use framer‑motion for UI micro‑interactions and entrance choreography (orchestrated reveal).
- Use motion.dev where spring primitives help for tactile controls.
- Wheel/gesture via Lenis → timeline param (no page scroll).
- Provide dev hotkeys: [Space]=pause, [H]=quality, [.] step frame, [G]=toggle GUI.

## Performance Targets
- 60fps on mid‑range laptops; degrade gracefully on mobile (LOD, particle count, shader branches).
- Draw calls < 100; texture memory < 100MB; avoid heavy assets.
- Use detect-gpu tiers (high/medium/low) to adjust resolution scale, effect passes, counts.
- Avoid expensive conditionals in fragments; precompute; small shader files; early exits.

## Accessibility
- prefers-reduced-motion → static composition with tiny breathing pulse only.
- Keyboard equivalents for main interactions; ARIA labels for UI elements.
- Provide “Reduce effects” toggle in dev, auto‑select on low tier.

## Deliverables (file structure; create or update as appropriate)
- `app/(experience)/page.tsx` — single route filling viewport (SSR off for Canvas)
- `app/(experience)/Scene.tsx` — Canvas with camera, lights, effects, chosen concept
- `app/(experience)/components/{Effect}.tsx` — main effect implementation
- `app/providers/MotionProvider.tsx` — framer + Lenis wrapper (root usage)
- `lib/gpu/useQualityTier.ts` — detect‑gpu wrapper and tiered settings
- `styles/globals.css` — Tailwind v4 base; body overflow-hidden
- Optional: `components/UI/Controls.tsx` — minimal controls; Leva dev‑only
- `README_experience.md` — run/build instructions + controls

## Implementation Notes
- Canvas: `preserveDrawingBuffer=false`, `powerPreference="high-performance"`, `dpr` clamped per tier.
- Use `Environment` preset from drei; avoid external heavy HDRI.
- Guard mobile: reduce samples, particle counts, disable heavy post.
- No `OrbitControls`; implement pointer parallax and gentle camera drift manually.
- Keep shaders concise; uniforms for time, mouse, intensity, dispersion; avoid large loops.

## Quality Gates (ship only if all pass)
- First meaningful paint < 2.5s; LCP stable.
- No WebGL context loss in 5‑minute soak test.
- INP within acceptable range (no jank on wheel).
- Accessibility checks pass; reduced motion honored.

## Handoff & Reporting
- Follow the 3d-artist command `output_format`: include fps, memory, files generated, effects count.
- Suggest a follow‑up “motion‑expert” run for advanced micro‑interactions:
  - Section title entrance, subtle HUD reveal, quality toggle transitions, idle attract loop.

## Constraints
- Zero marketing fluff; minimal UI.
- No dependency bloat; only libraries listed.
- Keep bundle lean; dynamic import Canvas scene (ssr: false).

---

Now, implement the best concept above for the target environment with production-hardening, then output your artifact report and perfect next command.
