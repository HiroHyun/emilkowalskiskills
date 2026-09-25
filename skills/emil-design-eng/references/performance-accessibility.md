# Motion performance and accessibility

Read when motion runs under load or needs accessibility review.

## Rendering performance

Animate `transform` and `opacity` for motion that should avoid layout and paint. Changes to `padding`, `margin`, `height`, and `width` can trigger layout, paint, and compositing work.

CSS variables inherit. Updating a variable on a drawer container recalculates styles for its children; update the moving element's transform directly.

```js
// Bad: triggers recalc on all children
element.style.setProperty('--swipe-amount', `${distance}px`);

// Good: only affects this element
element.style.transform = `translateY(${distance}px)`;
```

Framer Motion shorthand props (`x`, `y`, `scale`) use main-thread `requestAnimationFrame` updates. Use a full `transform` string when main-thread load makes dropped frames likely.

```jsx
// NOT hardware accelerated (convenient but drops frames under load)
<motion.div animate={{ x: 100 }} />

// Hardware accelerated (stays smooth even when main thread is busy)
<motion.div animate={{ transform: "translateX(100px)" }} />
```

Use CSS for predetermined animation. Use JS or WAAPI for dynamic, interruptible animation. WAAPI provides programmatic control without a library.

```js
element.animate([{ clipPath: 'inset(0 0 100% 0)' }, { clipPath: 'inset(0 0 0 0)' }], {
  duration: 1000,
  fill: 'forwards',
  easing: 'cubic-bezier(0.77, 0, 0.175, 1)',
});
```

## Accessibility

Reduced motion means fewer and gentler animations. Keep opacity and color transitions that aid comprehension; remove movement and position animation.

```css
@media (prefers-reduced-motion: reduce) {
  .element {
    animation: fade 0.2s ease;
    /* No transform-based motion */
  }
}
```

```jsx
const shouldReduceMotion = useReducedMotion();
const closedX = shouldReduceMotion ? 0 : '-100%';
```

Gate hover effects to hover-capable pointers because touch devices can trigger hover during taps.

```css
@media (hover: hover) and (pointer: fine) {
  .element:hover {
    transform: scale(1.05);
  }
}
```
