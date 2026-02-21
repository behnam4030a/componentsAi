# تسک‌های پیاده‌سازی کامپوننت Switch

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/switch/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `switch.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ brand (background: rest, hover, pressed — stroke: primary, secondary — foreground)
  - [x] 2.1.2 متغیرهای رنگ neutral (background: primary, secondary rest/hover/pressed, disabled — stroke: rest, disabled — foreground: primary, secondary, disabled)
  - [x] 2.1.3 متغیرهای radius (full, container)
  - [x] 2.1.4 متغیرهای size (wrapper, track, circle, icon)
  - [x] 2.1.5 متغیرهای spacing (wrapperPadding, trackPadding) و transition
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.switch` (wrapper label) — inline-flex, border transparent, border-radius 4px, cursor pointer
  - [x] 2.2.2 ساختار `.switch__input` — visually hidden
  - [x] 2.2.3 ساختار `.switch__track` — flex, border 1px solid, border-radius full, position relative
  - [x] 2.2.4 ساختار `.switch__thumb` — دایره 22px, position absolute, border 1px solid, border-radius full, transition
  - [x] 2.2.5 ساختار `.switch__icon` — 14px, آیکن checkmark/X با inline SVG
- [x] 2.3 پیاده‌سازی حالت‌های Unchecked Track
  - [x] 2.3.1 Rest: bg #ffffff, border #e2e4e6
  - [x] 2.3.2 Hover: bg #f6f8fa, border #e2e4e6
  - [x] 2.3.3 Pressed: bg #dddfe1, border #e2e4e6
  - [x] 2.3.4 Disabled: bg #f6f8fa, border #dddfe1
- [x] 2.4 پیاده‌سازی حالت‌های Checked Track
  - [x] 2.4.1 Rest: bg #26a88c, border #eaf8f5
  - [x] 2.4.2 Hover: bg #22967d, border #eaf8f5
  - [x] 2.4.3 Pressed: bg #19705e, border #eaf8f5
  - [x] 2.4.4 Disabled: bg #f6f8fa, border #dddfe1
- [x] 2.5 پیاده‌سازی Thumb
  - [x] 2.5.1 Unchecked: bg #ffffff, border #e2e4e6, position start (right: -2px در RTL)
  - [x] 2.5.2 Checked: bg #ffffff, border #26a88c, position end (right: calc(100% - 20px) در RTL)
  - [x] 2.5.3 Disabled: bg #e7e9eb, border #dddfe1
  - [x] 2.5.4 Transition حرکت Thumb با right/left properties
- [x] 2.6 پیاده‌سازی آیکن‌ها
  - [x] 2.6.1 آیکن checkmark (checked) — رنگ #26a88c با inline SVG
  - [x] 2.6.2 آیکن X (unchecked) — رنگ #59595a با inline SVG
  - [x] 2.6.3 آیکن disabled — رنگ #bbbcbe
- [x] 2.7 پیاده‌سازی Focus Ring
  - [x] 2.7.1 focus-visible: border 1px solid #222323 روی wrapper با :has(:focus-visible)
  - [x] 2.7.2 بدون تغییر layout (transparent border default → solid در focus)
  - [x] 2.7.3 Non-exclusive: همزمان با rest/hover/pressed
  - [x] 2.7.4 fallback برای مرورگرهای بدون :has() با :focus-within
- [x] 2.8 پیاده‌سازی اولویت stateها
  - [x] 2.8.1 disabled > pressed > focus > hover > rest (با CSS specificity)
  - [x] 2.8.2 Disabled جلوگیری از hover/pressed/focus با :not(:disabled)
- [x] 2.9 پشتیبانی RTL/LTR
  - [x] 2.9.1 Thumb position با physical properties (right/left) — RTL default، LTR override با [dir="ltr"]
  - [x] 2.9.2 آیکن جهت‌دار نیست (checkmark و X متقارن)
- [x] 2.10 افزودن transition‌های نرم (background-color, border-color, right, left)

## 3. تست و دمو
- [x] 3.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 3.1.1 نمایش تمام stateها — Unchecked (Rest, Hover, Pressed, Disabled, Focus)
  - [x] 3.1.2 نمایش تمام stateها — Checked
  - [x] 3.1.3 نمایش ماتریس state × checked
  - [x] 3.1.4 نمایش با Label جداگانه
- [ ] 3.2 تست حالت‌های تعاملی
  - [ ] 3.2.1 Rest, Hover, Pressed — بررسی تغییرات بصری Track
  - [ ] 3.2.2 Focus — focus ring صحیح (non-exclusive)
  - [ ] 3.2.3 Disabled — عدم تعامل، رنگ‌های disabled
  - [ ] 3.2.4 اولویت stateها: disabled > pressed > focus > hover > rest
- [ ] 3.3 تست Checked/Unchecked
  - [ ] 3.3.1 حرکت Thumb بین on/off
  - [ ] 3.3.2 تغییر رنگ Track و آیکن
  - [ ] 3.3.3 Toggle با کلیک
- [ ] 3.4 تست RTL/LTR
  - [ ] 3.4.1 موقعیت صحیح Thumb در RTL
  - [ ] 3.4.2 موقعیت صحیح Thumb در LTR
- [ ] 3.5 تست دسترسی‌پذیری
  - [ ] 3.5.1 ناوبری با Tab
  - [ ] 3.5.2 Toggle با Space
  - [ ] 3.5.3 role="switch" صحیح
  - [ ] 3.5.4 Screen reader compatibility
  - [ ] 3.5.5 کنتراست رنگ
- [ ] 3.6 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 4. مستندات
- [x] 4.1 ایجاد README.md با نحوه استفاده و مثال‌ها
- [x] 4.2 مستندسازی CSS classes و API
- [x] 4.3 مستندسازی نحوه استفاده با Label جداگانه
