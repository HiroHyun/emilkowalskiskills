# UI review checklist

Read when reviewing interface code. Report concrete current behavior, proposed change, and rationale for each finding. Match the review depth to the request.

- Replace `transition: all` with exact properties such as `transition: transform 200ms ease-out`.
- Start entry animation around `scale(0.95)` with `opacity: 0`; avoid `scale(0)`.
- Replace `ease-in` on UI elements with `ease-out` or a custom curve.
- Set popover `transform-origin` to the trigger location or `var(--transform-origin)`; keep modals centered.
- Remove animation from keyboard-initiated actions.
- Reduce UI durations above 300ms toward the relevant 100–250ms range.
- Gate hover animation with `@media (hover: hover) and (pointer: fine)`.
- Use transitions for rapidly triggered elements so motion can retarget.
- Under load, replace Framer Motion `x`/`y` props with a full `transform` when frame drops matter.
- Make deliberate enter timing and fast release timing distinct for hold interactions.
- Add short 30–80ms stagger when simultaneous decorative entry benefits from it.
- Check `prefers-reduced-motion`, touch behavior, pointer capture, and interaction availability.
