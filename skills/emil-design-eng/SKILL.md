---
name: emil-design-eng
description: Apply Emil Kowalski's UI design engineering principles to component polish, animation decisions, interactions, and motion performance when building or reviewing interfaces.
---

# Emil Design Engineering

Use this skill for UI polish, component behavior, aesthetic direction, interaction details, and animation decisions. Optimize for details users expect: clear purpose, responsive feedback, cohesive motion, and good defaults.

## Working principles

- Decide whether motion earns its cost. Frequent keyboard actions generally need immediate state changes.
- Give every animation a purpose: spatial consistency, state indication, explanation, feedback, or smoothing a change.
- Use `ease-out` for entry and exit, `ease-in-out` for movement, `ease` for hover and color, and `linear` for constant motion. Prefer strong custom curves; avoid `ease-in` for UI.
- Keep common UI motion under 300ms. Typical ranges: press 100–160ms, tooltip/popover 125–200ms, dropdown 150–250ms, modal/drawer 200–500ms.
- Use springs for interruptible gestures, momentum, and decorative motion. Keep bounce subtle (0.1–0.3) and omit it from most UI.
- Use transitions for rapidly retargeted state changes; use CSS for predetermined motion and JS or WAAPI for dynamic, interruptible motion.
- Build components with good defaults, low adoption friction, invisible edge-case handling, and motion that matches the component's mood.
- Preserve comprehension and access: honor reduced motion, gate hover effects to hover-capable pointers, and keep decorative stagger from blocking interaction.
- Inspect motion in slow motion or frame by frame; test touch interactions on real devices when practical.

## Conditional references

- For component patterns and concrete examples, read [references/components.md](references/components.md).
- For animation decisions, easing, springs, transforms, clip paths, stagger, or debugging, read [references/animation-motion.md](references/animation-motion.md).
- For drag, swipe, momentum, damping, pointer capture, or multi-touch, read [references/gestures.md](references/gestures.md).
- For rendering performance, CSS/JS tradeoffs, reduced motion, or touch hover behavior, read [references/performance-accessibility.md](references/performance-accessibility.md).
- For UI review criteria, read [references/review.md](references/review.md) and report each concrete issue, fix, and reason.

## Related skills

Use these only when the request calls for the corresponding work:

- `prototype` for a throwaway exploratory UI prototype.
- `review-animations` for an explicit strict motion review.
- `improve-animations` for a codebase-wide motion audit and implementation plan; keep direct fixes in implementation work.
- `find-animation-opportunities` for analysis of interface moments that lack useful motion.
- `animation-vocabulary` for naming a motion effect from a vague description.
- `apple-design` for Apple-style gesture details such as springs, drag, swipe, sheets, and momentum.
- `pick-ui-library` only when the user explicitly requests library selection.
