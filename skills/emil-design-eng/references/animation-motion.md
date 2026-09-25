# Animation and motion

Read when selecting, implementing, or debugging animation.

## Decide first

| Frequency | Guidance |
| --- | --- |
| 100+ times/day | Immediate state change; omit animation |
| Tens of times/day | Remove or reduce motion |
| Occasional | Standard animation |
| Rare or first-time | Add delight when it supports the task |

Give motion a purpose: spatial consistency, state indication, explanation, feedback, or smoothing a change. Frequent keyboard actions need immediate feedback.

## Easing and duration

Use `ease-out` for entry and exit, `ease-in-out` for movement or morphing, `ease` for hover or color, and `linear` for constant motion. Avoid `ease-in` for UI animation.

```css
/* Strong ease-out for UI interactions */
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);

/* Strong ease-in-out for on-screen movement */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);

/* iOS-like drawer curve (from Ionic Framework) */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
```

Use [easing.dev](https://easing.dev/) or [easings.co](https://easings.co/) for curve references. Typical durations: press 100–160ms; tooltip or small popover 125–200ms; dropdown or select 150–250ms; modal or drawer 200–500ms. Keep common UI motion under 300ms.

Perceived speed matters: a fast spinner, 180ms select, and instant adjacent tooltip each reduce perceived waiting.

## Springs

Use springs for drag momentum, interruptible gestures, lively decorative elements, and mouse tracking. Omit decorative motion when it competes with functional information.

```jsx
import { useSpring } from 'framer-motion';

// Direct mapping: feels artificial, instant
const rotation = mouseX * 0.1;

// Spring mapping: feels natural, has momentum
const springRotation = useSpring(mouseX * 0.1, {
  stiffness: 100,
  damping: 10,
});
```

**Apple's approach (recommended — easier to reason about):**

```js
{ type: "spring", duration: 0.5, bounce: 0.2 }
```

**Traditional physics (more control):**

```js
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }
```

Keep bounce subtle (0.1–0.3). Springs retain velocity when interrupted, which suits gestures whose direction can change.

## Transforms and clip paths

Percentages in `translate()` use the element's own size, so they adapt to content.

```css
/* Works regardless of drawer height */
.drawer-hidden {
  transform: translateY(100%);
}

/* Works regardless of toast height */
.toast-enter {
  transform: translateY(-100%);
}
```

`scale()` scales descendants; use it when proportional press feedback is desired. Use `transform-origin` to match the trigger for anchored surfaces. Use `transform-style: preserve-3d` with `rotateX()` or `rotateY()` for depth effects.

```css
.wrapper {
  transform-style: preserve-3d;
}

@keyframes orbit {
  from {
    transform: translate(-50%, -50%) rotateY(0deg) translateZ(72px) rotateY(360deg);
  }
  to {
    transform: translate(-50%, -50%) rotateY(360deg) translateZ(72px) rotateY(0deg);
  }
}
```

Use `clip-path: inset(top right bottom left)` for reveals, hold actions, and comparison sliders.

```css
/* Fully hidden from right */
.hidden {
  clip-path: inset(0 100% 0 0);
}

/* Fully visible */
.visible {
  clip-path: inset(0 0 0 0);
}

/* Reveal from left to right */
.overlay {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 200ms ease-out;
}
.button:active .overlay {
  clip-path: inset(0 0 0 0);
  transition: clip-path 2s linear;
}
```

For continuous tab color changes, duplicate the tab list, style one copy as active, clip it to the active tab, and animate the clip. For an image reveal, use `clip-path: inset(0 0 100% 0)` to `inset(0 0 0 0)` on viewport entry with `IntersectionObserver` or `useInView({ once: true, margin: "-100px" })`. For a comparison slider, overlay images and update the top image's right inset from the drag position.

## Stagger and inspection

Stagger decorative entries by 30–80ms. Keep interaction available while items animate.

```css
.item {
  opacity: 0;
  transform: translateY(8px);
  animation: fadeIn 300ms ease-out forwards;
}

.item:nth-child(1) {
  animation-delay: 0ms;
}
.item:nth-child(2) {
  animation-delay: 50ms;
}
.item:nth-child(3) {
  animation-delay: 100ms;
}
.item:nth-child(4) {
  animation-delay: 150ms;
}

@keyframes fadeIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

Inspect with durations increased 2–5 times, or frame by frame. Check color blending, easing, transform origin, and synchronization between opacity, transform, and color. Use Chrome DevTools' Animations panel and test touch interactions on physical devices when available.
