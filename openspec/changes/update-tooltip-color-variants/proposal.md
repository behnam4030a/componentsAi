# Change: Add Color Variants to Tooltip Component

## Why
طرح Figma شامل ۷ نوع رنگ مختلف برای تولتیپ است (Primary, Secondary, Success, Danger, Warning, Info, Dark) علاوه بر رنگ پیش‌فرض تیره (#364455). این variant ها امکان انتقال معنای معنایی از طریق رنگ تولتیپ را فراهم می‌کنند.

## What Changes
- افزودن ۷ کلاس modifier رنگی به CSS تولتیپ (`.tooltip--primary` تا `.tooltip--dark`)
- افزودن پشتیبانی از attribute جدید `data-tooltip-variant` در JavaScript
- افزودن متد `setVariant()` برای تغییر variant در زمان اجرا
- بروزرسانی tokens.json با تعریف رنگ‌ها مطابق Figma variables
- بروزرسانی صفحه دمو با نمایش تمام variant ها

## Figma Sources
- Page 201:266 — Overview (default + primary tooltip)
- Page 2021:739 — Tooltip 1: 4 positions (default dark color)
- Page 2021:1279 — Tooltip 2: 7 color variants

## Color Variants (from Figma Variables)

| Variant | Figma Variable | Color | Text |
|---------|---------------|-------|------|
| default | — | #364455 | #ffffff |
| primary | color/shared/lavender/primary | #7160e8 | #ffffff |
| secondary | color/neutral/grey_48 | #7b7c7d | #ffffff |
| success | color/shared/green/tint_30 | #54b054 | #ffffff |
| danger | color/shared/cranberry/tint_10 | #cc2635 | #ffffff |
| warning | color/shared/orange/tint_20 | #f98845 | #ffffff |
| info | color/shared/blue/tint_20 | #3595de | #ffffff |
| dark | color/neutral/black | #000000 | #ffffff |

## Impact
- Affected specs: tooltip (existing capability)
- Affected code:
  - `components/tooltip/tokens.json` (modified)
  - `components/tooltip/tooltip.css` (modified)
  - `components/tooltip/tooltip.js` (modified)
  - `components/tooltip/index.html` (modified)
