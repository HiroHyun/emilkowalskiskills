# Component patterns

Use these patterns when component behavior or polish is in scope.

## Responsive controls

Add subtle press feedback to pressable elements (0.95–0.98 scale).

```css
.button {
  transition: transform 160ms ease-out;
}

.button:active {
  transform: scale(0.97);
}
```

Start entrances at `scale(0.9)` or higher with opacity. This gives the element a visible shape during entry.

```css
/* Bad */
.entering {
  transform: scale(0);
}

/* Good */
.entering {
  transform: scale(0.95);
  opacity: 0;
}
```

## Origin-aware surfaces

Scale popovers from their trigger. Keep modals centered because they are viewport-anchored.

```css
/* Base UI */
.popover {
  transform-origin: var(--transform-origin);
}
```

Tooltips use an initial delay to prevent accidental activation. Adjacent tooltips can open instantly after one is active.

```css
.tooltip {
  transition: transform 125ms ease-out, opacity 125ms ease-out;
  transform-origin: var(--transform-origin);
}

.tooltip[data-starting-style],
.tooltip[data-ending-style] {
  opacity: 0;
  transform: scale(0.97);
}

/* Skip animation on subsequent tooltips */
.tooltip[data-instant] {
  transition-duration: 0ms;
}
```

## Interruptible state changes

CSS transitions can be interrupted and retargeted mid-animation. Use them for rapidly triggered UI such as toasts and toggles.

```css
/* Interruptible - good for UI */
.toast {
  transition: transform 400ms ease;
}

/* Not interruptible - avoid for dynamic UI */
@keyframes slideIn {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}
```

## Crossfades and entry

Use subtle blur during a crossfade when two states remain visually distinct. Keep blur under 20px; heavy blur costs more in Safari.

```css
.button {
  transition: transform 160ms ease-out;
}

.button:active {
  transform: scale(0.97);
}

.button-content {
  transition: filter 200ms ease, opacity 200ms ease;
}

.button-content.transitioning {
  filter: blur(2px);
  opacity: 0.7;
}
```

Use `@starting-style` for CSS entry animation when browser support allows it; use a `data-mounted` attribute fallback where needed.

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 400ms ease, transform 400ms ease;

  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

```jsx
// Legacy pattern (still works everywhere)
useEffect(() => {
  setMounted(true);
}, []);
// <div data-mounted={mounted}>
```

## Component defaults and edge cases

- Ship strong defaults before adding options.
- Keep adoption friction low; a component should need only the setup its behavior requires.
- Handle hidden-tab timers, stacked-item hover gaps, and pointer capture within the component.
- Match easing, duration, and feedback to the component's personality and task.
- Tune opacity with height when list items enter or exit; validate the combined result visually.
- Use slower deliberate feedback for hold actions and a fast release response.

```css
/* Release: fast */
.overlay {
  transition: clip-path 200ms ease-out;
}

/* Press: slow and deliberate */
.button:active .overlay {
  transition: clip-path 2s linear;
}
```
