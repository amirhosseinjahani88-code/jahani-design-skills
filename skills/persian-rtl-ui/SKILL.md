---
name: persian-rtl-ui
description: >-
  Building Persian (Farsi), right-to-left interfaces the way the owner wants: RTL layout and mirroring, Persian
  digits and number runs that stay readable (also while animating), toman/rial money, Jalali (Shamsi) dates with
  Persian weekday names, Persian fonts, plain short Persian copy and word choices. Use for any UI with Persian text,
  RTL layout, Iranian money or Jalali dates, and when reading Iranian receipts or SMS flows.
---

# Persian RTL UI

## Layout

- `<html lang="fa" dir="rtl">`. Use logical CSS properties everywhere (`margin-inline-start`, `inset-inline-end`,
  `padding-inline`, `text-align: start`), never `left/right` for layout.
- "Start" is the right side. Title right, its action/date/number left. Search right, add button left. Edit/delete
  icons left. A floating add button bottom-left.
- Icons that point a direction (back, next, chevrons) are mirrored; logos, media controls and checkmarks are not.
- Animations and menus follow RTL too: measure positions from the real layout; menus on the left open from their
  top-left corner.
- "Center it" usually means *center the text*; don't move the block unless asked. Ask if unsure.

## Numbers

- Show Persian digits (۰۱۲۳۴۵۶۷۸۹) in the UI; accept Persian, Arabic and Latin digits in every input
  (normalise before parsing) and Persian separators (٬ , ،) in amounts: «۵۰۰٬۰۰۰» is 500000.
- Each run of digits (with its separators, %, :) is one left-to-right piece: `direction: ltr; unicode-bidi:
  isolate`. Check the final layout after number animations: digits must not end up left-aligned in a right-aligned
  line or reversed.
- Times like ۰۶:۰۰, dates like ۱۴۰۵/۰۸/۱۷, phone numbers: keep them LTR inside RTL text.

## Money

- Show **تومان** (toman). Iranian bank receipts and some gateways use **ریال** (rial): 1 toman = 10 rial. When
  reading a receipt (OCR/AI), read the printed number *and* its unit, assume rial unless it says toman, convert, show
  both to the person, and let them correct the amount; warn on suspiciously small amounts.
- Payment gateways may want rial: convert at the boundary only.
- Format: `۲٬۵۰۰٬۰۰۰ تومان` (Persian digits, thousands separators). Never dollars in the UI.

## Dates

- Jalali (Shamsi) calendar for everything the user sees; ISO (Gregorian) in the database and API. One conversion
  function, tested.
- Day pickers show full weekday names («شنبه», not «ش»).
- "Today" is the Tehran day (Asia/Tehran), not UTC (they differ between 20:30 and 24:00 UTC).

## Type

- A Persian-first font (e.g. Dana, Vazirmatn) with a system fallback; check the licence before shipping a font.
- Slightly larger body size and line height than Latin UIs; never letter-spacing on Persian.

## Copy

- Plain, short, everyday Persian; no formal or bookish phrasing; no machine-translated tone. Every user-facing
  string is Persian (plan or brand names may stay English if the owner says so).
- Word choices the owner fixed: «جدید» not «تازه»; «ثبت‌نام» not «ساخت حساب»; «پیام یادآوری» not «کپی پیام
  یادآوری»; «حضور و غیاب» for the attendance action; «به‌زودی» for coming features.
- No punctuation in big display headlines unless asked.
- Use ZWNJ (نیم‌فاصله) correctly: «می‌شود», «یادداشت‌ها», «ثبت‌نام» (not «می شود», «یادداشتها»).
- Errors say what happened and what to do, in one short sentence: «شماره درست نیست. مثل ۰۹۱۲۳۴۵۶۷۸۹ بنویسید.»

## Iranian specifics

- Phone numbers: accept 09…, +989…, 00989…, 989… (any digits, spaces, dashes); store as 09xxxxxxxxx; refuse foreign
  numbers for SMS (they cost far more).
- Code (OTP) inputs: six square boxes, auto-fill (`autocomplete="one-time-code"`), auto-submit when full.
- Consent: no pre-ticked boxes; prefer a line under the submit button («با ثبت‌نام، قوانین و حریم خصوصی را
  می‌پذیرید») when the owner chooses that.

## Replying to a Persian-speaking owner

Answer in Persian, short and plain. Keep code, paths and commands in LTR blocks so they don't scramble.
