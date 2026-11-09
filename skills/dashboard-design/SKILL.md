---
name: dashboard-design
description: >-
  How the owner wants dashboards and app panels laid out, learned from building the jahanicoaching.ir coach panel:
  every section one box with its title inside, every list item its own grey box, whole cards clickable with hover,
  minimal text, label/value rows, consistent page titles, per-page skeletons, mobile patterns (full-screen sheets,
  FAB, ⋯ menus, filter sheet), day/night themes, no fake data. Use when designing, building or reviewing any
  dashboard, admin/coach/client panel, list page, detail page, settings page or data card, desktop or mobile.
---

# Dashboard design

Look at the live reference before designing: **https://jahanicoaching.ir** (landing, sign-up, coach panel, parent
portal). The panel there is the result of these rules. Combine with the `ux-laws`, `motion-rules` and (for Persian)
`persian-rtl-ui` skills.

## Working with the owner

- **Ask before deciding.** For anything not spelled out (which buttons move, what text goes, which colour), ask
  short questions first, with your recommendation as the first option. The owner prefers more questions over a
  wrong guess. Never make a product or visual decision on your own.
- Take words literally but check the intent: "center it" once meant *center the text*, not *move the block to the
  middle of the page*. If an instruction has two readings, ask.
- Changes may be for **one screen size only** ("فقط موبایل", "فقط دسکتاپ"). Keep the other size untouched.
- Look at the result in a real browser at phone width (~375-390 px) and desktop (~1280 px) before saying it's
  done; report what you *saw* separately from what you only tested.

## Structure

- **Every section is one box, with its title inside it.** No title floating above a box; no two boxes for one
  thing (e.g. a session name shown once above and again in a box below: merge into one).
- **Every item in a list is its own box** (a soft grey surface, slightly lighter/darker than the section box),
  in both themes: each swimmer, each session, each debtor, each note, each test result. The eye counts boxes.
- Boxes in one row have equal heights; cards of one kind have equal sizes. Content width stays comfortable: rows
  of same-size boxes, not one huge full-width slab.
- **Every page puts its title in the same place, at the same size and width**, so page-to-page transitions and the
  eye both stay anchored. The dashboard is not wider or differently headed than the other pages.
- The page date or a key count goes opposite the title, on the same row (RTL: title right, date left).
- Tabs inside a detail page sit opposite the page/person name, on one row when they fit.

## Lists and cards

- **The whole card is the click target** when it opens something (a real `<button>` or link, Enter/Space work,
  visible focus ring, `aria-label` like «جزئیات جلسه ...»), with a small, simple hover (a slightly different grey).
  Every clickable thing has a hover state; things that are not clickable don't.
- Show the minimum: a swimmer row = name (+ edit and delete icons on the end side). A workout card = title and
  metres. A test row on mobile = date, seconds and a ⋯. Drop meta lines under titles (age, level, "updated...",
  sub-totals) unless the owner asks for them; details belong in the detail view.
- Edit and delete icons sit on the end side (RTL: left), delete in red.
- A list item that summarises (e.g. a session) shows its facts in **one row next to its name**, separated and
  readable, not stacked under it.
- Multi-step content (a workout's sets) is structured: row 1 = title + description, row 2 = distance × reps;
  clickable to edit (no separate edit button per item).

## Numbers and data

- **No fake or sample numbers, ever.** Every number comes from the database. If there is no data yet, say so
  («هنوز داده‌ای نیست») or hide the number. A sample/demo area is labelled «نمونه».
- Rates and AI insights are computed from real units (attendance per session, not per day).
- Totals: label on the start side, amount + unit on the end side, one row. Money in the local currency word
  (تومان), Persian digits, thousands separators.
- Charts: one consistent chart style across the product; on phones show fewer points (e.g. last 3) and make the
  chart bigger, not denser. Remove axis clutter the owner didn't ask for.
- Long values must never overflow their box on phones (payments, session names, notes): wrap or truncate with a
  title/tooltip.

## Actions

- One primary button per box (see `ux-laws`). Secondary buttons have a border. Button groups at the bottom of a
  form or preview are centred when they stand alone.
- A primary "add" button + a «فیلتر» button + search: search on the start side, add on the end side, filter next to
  add. The filter opens a menu with every facet (group, level, stroke, distance, date range...) and a search box.
- Rare actions go into one ⋯ menu per box, **after asking** which ones. A ⋯ menu opens without re-rendering the
  page (no flash).
- Popups for add/edit live behind their button (e.g. «افزودن رکورد» opens a dialog), not as an always-open form.
- When the system is sure, do it in one step and offer undo («ثبت شد ... برگردان»); when unsure, show a preview
  and ask.
- Every saved record can be edited and deleted later (with a confirm).

## Mobile (phones)

- Dialogs and detail cards open **full screen except the bottom nav bar**, scroll to the very bottom, never half
  open.
- Bottom nav bar + a floating add button in the bottom corner (RTL: bottom-left) above it, on every page, stable.
- Fewer words: icon-only buttons where the icon is unmistakable (the AI icon), with an `aria-label` and a tooltip on
  pointer devices.
- Remove avatars and decorations when space is tight; text comes first.
- Horizontal scrollers show a hint (arrow or cut edge).
- Things that are a choice among many (age group, session) go into a ⋯ or a select, not chips spread over the page.

## Loading and saving

- Each page has its **own skeleton**, identical to its real layout, so content lands exactly on it (see
  `motion-rules`).
- Load what the first screen needs first; heavy media and code for other areas after (lazy, prefetched once idle).
- Saves show «در حال ذخیره…» then «ذخیره شد»; failures say so and keep the input.
- Work data lives in the database, never only in the browser (only UI prefs, unsaved drafts, the sign-in cookie
  may live there; nothing personal after logout).

## Themes

- Night (dark) is the default. Day (light) only when the person chooses it in settings or a header switch; never
  follow the device setting automatically.
- Use the project's fixed palette exactly. **Never "improve", swap or darken the owner's colours**; if contrast is
  a problem, say so and ask. Status colours (present green, late yellow with dark text, absent/error red) are
  added only with the owner's OK.
- Every list item is a grey box in both themes; check both themes at both widths.

## Copy

- Short, plain sentences. If a line doesn't help the user act, remove it.
- Use the owner's words for buttons and labels; for new UI text, use a UX-copy pass (e.g. the `design:ux-copy`
  skill) and keep the owner's tone.

## Done checklist

- [ ] Sections are boxes with titles inside; list items are grey boxes.
- [ ] Whole cards clickable with hover; non-clickables have no hover.
- [ ] No meta text the owner didn't ask for; no fake numbers.
- [ ] Page title in the same place as on every other page.
- [ ] One primary per box; ⋯ for rare actions (asked first); red for delete.
- [ ] Mobile: full-screen sheets above the nav bar, stable FAB, nothing overflows at 375 px.
- [ ] Own skeleton; save indicator; motion per `motion-rules`.
- [ ] Both themes checked; palette untouched.
- [ ] Seen in a browser at phone and desktop width.
