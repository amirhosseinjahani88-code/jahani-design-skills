---
name: motion-rules
description: >-
  The owner's motion language for any web UI: 20 motion rules plus 12 transitions.dev recipes (tabs sliding,
  number pop-in, spinning counter, error shake, input clear with dissolve, skeleton reveal, texts reveal, tooltip,
  menu dropdown, accordion, checkbox check, toggle), page-specific skeletons, view transitions between pages and
  a save indicator. Use whenever you add or change anything that moves, appears, disappears, loads or confirms:
  dialogs, sheets, menus, toasts, lists, tabs, numbers, buttons, page changes, loading states. Works for vanilla
  JS/CSS and React; RTL-aware.
---

# Motion rules

One motion language across the whole product. Every UI change follows it, on every page. Motion explains what
happened (where a thing came from, where it went, that it worked); it never decorates.

## The 20 rules

| # | Rule | In practice |
|---|------|-------------|
| 1 | Ease-out for entrances | `cubic-bezier(.22,1,.36,1)` for anything appearing |
| 2 | Dropdowns 150-250 ms | menus 250 ms open, 150 ms close |
| 3 | Stagger list rows by 30 ms | `animation-delay: calc(var(--i) * 30ms)`, cap at ~10 rows |
| 4 | Scale to 0.97 on press | `:active { transform: scale(.97); transition-duration: 0ms }` |
| 5 | Stretch moving knobs 12% | a switch knob gets ~12% wider while pressed |
| 6 | Stagger as details settle | rows first, then the numbers/key-values ~120 ms later |
| 7 | Arcs for object movement | things travelling across the screen curve, not slide straight |
| 8 | Pulse to confirm success | one pulse (scale 1.18 at 50%, 360 ms) of the success tick |
| 9 | Ease-in-out for moves | `cubic-bezier(.65,0,.35,1)` for something going from A to B |
| 10 | Start popovers at 0.95 | `from { opacity:0; transform: scale(.95) }` |
| 11 | Enter from the trigger | `transform-origin` = the button that opened it |
| 12 | Exit to the trigger | close back toward the same origin |
| 13 | No bounce on everyday UI | no overshoot, except the two exceptions below |
| 14 | Don't tween while held | while pressed, follow the finger at once (0 ms) |
| 15 | Exits 20% shorter | open 200 ms, close 160 ms; sheets 260 ms in, ~210 ms out, with ease-in |
| 16 | Overlap old & new states | the old page fades out (160 ms) while the new one fades in (220 ms) over it |
| 17 | Masks for reveals & colour | `clip-path: inset(0 0 100% 0)` to `inset(0)` instead of sliding content |
| 18 | Crossfade icons + blur | two icons in one grid cell; swap opacity with `blur(3px)` and `scale(.8)` |
| 19 | Rubber band past bounds | dragging past the end resists, then springs back |
| 20 | Reuse the same layoutId | the same element on both pages morphs (View Transitions `view-transition-name`, or Framer `layoutId`) |

**Bounce exceptions (owner's choice):** the number pop-in and the toggle keep their recipes' small overshoot.
Nothing else bounces.

## Tokens

Use tokens, never loose numbers. Copy [references/tokens.css](references/tokens.css) for a new project.

```css
--dur-1: 120ms;  /* press */
--dur-2: 220ms;  /* hover, state change */
--dur-3: 420ms;  /* page, drawer */
--dur-pop: 200ms; --dur-pop-out: 160ms; --dur-sheet: 260ms;
--ease-out: cubic-bezier(.22,1,.36,1);
--ease-in-out: cubic-bezier(.65,0,.35,1);
--ease-in: cubic-bezier(.4,0,1,1);   /* exits only */
```

## The 12 transitions.dev recipes

Install the recipe text with `npx transitions-dev add <name>` (it writes recipe .md files, not code) or
`npx skills add Jakubantalik/transitions.dev`, then adapt by hand. Classes are namespaced `.t-*`, tokens are CSS
variables. Where each goes:

| Recipe | Use on | Key tokens |
|--------|--------|-----------|
| tabs sliding | every segmented control and tab row: one pill that slides to the active tab | 250 ms, ease-out |
| number pop-in | small numbers that change: digits rise in, staggered 70 ms, slight overshoot | 500 ms, `cubic-bezier(.34,1.45,.64,1)` |
| spinning counter | **big numbers only** (totals, rates, balances): a reel per digit | 1400 ms |
| error state shake | a field, code box or alert that turns into an error: left, right, smaller overshoot | 280 ms, 6 px |
| input clear with dissolve | the × of search fields: the typed words fall and blur away | 400 ms |
| skeleton reveal | content replacing grey outlines fades in from a 2 px blur | 400 ms |
| texts reveal | a page's headline, then its sub-line, then its buttons rise in, 40 ms apart | 500 ms |
| tooltip | the name of every icon-only button, on hover/focus, pointer devices only | in 150 ms, out 50 ms |
| menu dropdown | every ⋯ menu and filter menu: opens from its corner at 0.97 | open 250 ms, close 150 ms |
| accordion | `<details>`: animate `block-size` with `interpolate-size: allow-keywords`; chevron flips | 250 ms |
| checkbox check | a chosen chip fills, then its tick draws | box 150 ms, draw 350 ms |
| toggle | the switch knob overshoots a little and settles; the track colour has its own clock | 350 ms |

## Loading

- **Skeletons are per page.** Each page has its own skeleton that matches its real layout exactly (same boxes,
  same places, same sizes), so the content lands on top of it without shifting. Never show one page's skeleton
  (e.g. the landing's) while another page loads, including on a hard reload of that page.
- After the skeleton: the skeleton-reveal recipe.
- A long wait for media (a hero video): a small loader on its poster until it plays.
- **Saving:** the change shows on screen at once; a small indicator says «در حال ذخیره…» with a loader, then
  «ذخیره شد». If the write fails, say so and keep what was typed. Never let the indicator break the save.

## Between pages

- View Transitions API: old page fades out 160 ms, new page fades in 220 ms (rule 16).
- Give the current nav item and the page title a `view-transition-name` so they move to their new place (rule 20).
  This only works if **every page puts its title in the same place and at the same size**; a page whose title sits
  elsewhere (a wider dashboard, a different header) breaks the effect. Fix the layout, not the animation.
- A page's entrance plays **once**, on the paint that opens it, not on every re-render, tab click or filter change.

## Pitfalls learned the hard way

- **Re-render kills animation.** If the app redraws with `innerHTML`, a running animation restarts or vanishes, and
  a menu "flashes like the page restarted". Open/close menus by toggling classes (`is-open`, `is-closing`) on the
  existing node, not by re-rendering; run JS-driven recipes after the last paint (debounce).
- **Numbers in RTL.** Animating digits splits them into spans; in a right-to-left page they can end up left-aligned
  or reversed after the animation. Keep each run of digits as one left-to-right piece (`direction: ltr;
  unicode-bidi: isolate`) inside the RTL text, and check the final state, not just the animation.
- **Filters left on a box.** A `filter: blur()` that stays after an animation creates a containing block and breaks
  `position: fixed` children. Use `animation-fill-mode: backwards`, not `both`, for blur-in effects.
- **Filters and selects must not reload the page or jump to the top.** Changing a filter, stroke or week updates in
  place and keeps the scroll position.
- **Floating buttons (FAB)** must stay in their corner (above the mobile nav bar). Test after every navigation and
  every re-render; a FAB that jumps to the top "sometimes" is a real bug.
- RTL direction: things "enter from the trigger" in RTL too; menus that hang on the left open from their top-left
  corner. Measure from the real layout (`offsetLeft`), not assumptions.

## Accessibility

Respect `prefers-reduced-motion: reduce`: cut durations to ~1 ms, skip exits, page cross-fades and JS recipes.
Nothing needed to understand the page may live only in motion.

## Checklist before you finish

- [ ] Entrances ease-out, exits ease-in and 20% shorter, moves ease-in-out.
- [ ] Popovers/menus start at 0.95-0.97 and open from their trigger.
- [ ] Press feedback (0.97) on every tappable thing.
- [ ] No bounce except number pop-in and toggle.
- [ ] Lists stagger 30 ms; details settle after.
- [ ] Loading uses this page's own skeleton; saving shows the indicator.
- [ ] Re-renders do not replay entrances or restart menus.
- [ ] Numbers stay right-aligned and readable after animating in RTL.
- [ ] Reduced motion respected.
- [ ] Looked at it in a real browser at phone width and desktop width.
