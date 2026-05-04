# Terminal Panel Bottom Cutoff

## Problem

The bottom terminal panel's content extends behind the VS Code status bar, causing the last line of the terminal (including the cursor/typing indicator) to be cut off and invisible.

This occurs because the Islands Dark theme applies CSS borders to `.part.panel.bottom` for the floating glass-panel aesthetic:

```css
.part.panel.bottom {
  border-top: 6px solid var(--islands-bg-canvas);
  border-bottom: none;
  box-sizing: border-box;
}
```

## Root Cause

VS Code's workbench layout engine uses JavaScript (`PartLayout.layout()`) to calculate panel dimensions via absolute positioning in a split-view system — not CSS grid or flexbox. The JS calculates the `.content` element's height as:

```
contentHeight = totalHeight - 35px (title bar height)
```

This calculation does **not** account for CSS borders on the panel element. With `box-sizing: border-box`, the 6px top border reduces the panel's available content area by 6px. However, the JS still sets `.content` height as if all `totalHeight` pixels are available.

The result: the `.content` div is 6px taller than the space it sits in. Combined with `overflow: hidden` on the panel, the bottom 6px of the terminal content is clipped behind the status bar.

### Why other approaches failed

| Approach | Result |
|---|---|
| `border-bottom` / `padding-bottom` on panel | Invisible — the bottom of the panel is literally behind the status bar |
| `margin-bottom` on panel | No effect — panel is absolutely positioned by VS Code's split-view |
| `height: calc(100% - Npx)` on `.content` | Content collapses — parent has no explicit CSS height (set by JS grid) |
| `display: flex` on panel with `height: auto` on `.content` | Content disappears — breaks the `height: 100%` chain used by inner elements |
| `margin-bottom` on `.pane-body.integrated-terminal` | Works but creates a visible gap between terminal and panel bottom edge |

## Fix

Pull `.content` upward by exactly 6px (the top border height) using negative margin, and ensure the title bar paints on top of the overlapping area:

```css
.part.panel.bottom > .composite.title {
  position: relative !important;
  z-index: 1 !important;
}
.part.panel.bottom > .content {
  margin-top: -6px !important;
}
```

### How it works

1. `margin-top: -6px` on `.content` shifts the entire content block up by 6px, recovering the 6px at the bottom that was previously clipped behind the status bar.
2. `position: relative; z-index: 1` on the title bar (`.composite.title`) ensures it paints on top of the content area that now overlaps it by 6px.

The 6px value matches the `border-top: 6px` on `.part.panel.bottom`. The bottom border is removed (`border-bottom: none`) to avoid additional offset.
