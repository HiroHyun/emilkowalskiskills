# Gesture and drag interactions

Read when implementing drawers, sheets, swipe actions, or other pointer-driven motion.

## Dismissal and boundaries

Use velocity as well as distance. If `Math.abs(dragDistance) / elapsedTime` exceeds about `0.11`, dismiss a quick flick regardless of distance.

```js
const timeTaken = new Date().getTime() - dragStartTime.current.getTime();
const velocity = Math.abs(swipeAmount) / timeTaken;

if (Math.abs(swipeAmount) >= SWIPE_THRESHOLD || velocity > 0.11) {
  dismiss();
}
```

Apply damping past a natural boundary. Increasing drag distance should produce decreasing movement. Use increasing friction to make overscroll feel physical; this keeps motion natural at the boundary.

## Pointer ownership

Capture pointer events when dragging starts so the gesture continues after the pointer leaves the element bounds. Ignore additional touch points after the initial drag begins.

```js
function onPress() {
  if (isDragging) return;
  // Start drag...
}
```

Springs suit drag-to-dismiss because they preserve velocity when users interrupt or reverse the gesture. Keep bounce subtle.
