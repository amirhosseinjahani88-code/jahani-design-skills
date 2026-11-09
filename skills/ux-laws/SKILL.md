---
name: ux-laws
description: >-
  Five UX laws the owner applies to every user-facing screen: Fitts (44 px targets), Hick (rare actions behind one
  ⋯ menu, asked first), Jakob (familiar patterns), proximity (a heading hugs its own content) and Von Restorff (one
  primary button per box). Use when designing or changing any screen, form, menu, dialog, card or button layout,
  and when reviewing a UI. Internal admin tools may be exempt; ask.
---

# UX laws

Apply all five on every user-facing screen (landing, sign-in, the app, any client portal). Internal admin screens
are exempt unless the owner says otherwise. When a law and a request seem to conflict, ask.

## 1. Fitts: easy to hit

- Nothing tappable under **44 × 44 px** (icon buttons included: pad the hit area, not the icon).
- Primary actions where the thumb is on phones: a floating add button sits bottom corner (in RTL: bottom-left),
  above the bottom nav bar, and stays there on every page and after every re-render.
- A whole card or row is the target when it opens something, not a small link inside it.

## 2. Hick: fewer choices on screen

- Each box shows only the main action as a button. Rarely used or secondary actions (export, template, clear,
  save as draft, save to library, choose a group...) go behind **one ⋯ menu** on that box.
- **Ask the owner before moving any button into a ⋯ menu**, with the exact list of what would move and what stays.
  Do not decide alone.
- A ⋯ menu also tells the user "this card is clickable / has more": on mobile, a card that opens details gets a ⋯
  hint even when the whole card is the target.
- Filters live in one «فیلتر» button that opens a filter menu (a mega-menu on desktop, a bottom sheet on mobile),
  not as rows of chips on the page.
- Cut text. Remove helper lines, meta lines and repeated labels the user does not need to act. If a sentence
  explains something obvious, delete it.

## 3. Jakob: behave like every other app

- A menu opens under (or next to) its button; Esc and a tap outside close it; focus returns to the button.
- Dialogs have their title at the top and an × close at the top; on mobile they are bottom sheets or full screen.
- Search on one side, the main add button on the other (RTL: search right, «افزودن» left), filter next to add.
- Destructive actions ask to confirm and say exactly what will be lost («پرداخت‌ها، حضور و رکوردهای او هم برای
  همیشه پاک می‌شود»).
- Disabled features that are coming: visible but disabled, with a «به‌زودی» badge. Never a button that errors after
  the click.
- Things that scroll sideways show an arrow or a cut-off edge so the user knows to swipe.

## 4. Proximity: what belongs together sits together

- A heading sits closer to its own content than to the box above it. Better: the heading lives **inside** the box
  with its content (every section = one box with its title in it).
- A label and its value share one row: label on the start side, value on the end side (RTL: label right, number and
  unit left).
- Related controls form one row (e.g. «انتخاب جلسه» field + present / late / absent buttons in one row).
- Equal things look equal: boxes in one row have the same height; buttons in one group have the same size.

## 5. Von Restorff: one thing stands out

- **One primary (filled, accent) button per box.** Everything else is secondary (outlined, with a border) or ghost.
- Menu items are never accent-coloured. Destructive items and icons (delete, trash) are **red**, on every screen size.
- Only the item that needs attention gets a colour (e.g. in an insights list only "low attendance" is red; the rest
  stay neutral). Many colours = no signal.
- AI actions are recognisable by one consistent AI icon; on phones the AI button can be the icon alone.

## Review checklist

- [ ] Every tappable thing ≥ 44 × 44 px.
- [ ] One primary button per box; destructive in red; no accent menu items.
- [ ] Rare actions in one ⋯ (moved only after asking).
- [ ] Menus/dialogs close with Esc, outside tap and ×.
- [ ] Headings inside or right above their own box; label/value on one row.
- [ ] No text the user doesn't need.
- [ ] Coming-soon features disabled with «به‌زودی», never failing after a click.
