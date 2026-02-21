# تسک‌های پیاده‌سازی کامپوننت Radio

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/radio/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `radio.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ brand (foreground: rest, hover, pressed)
  - [x] 2.1.2 متغیرهای رنگ neutral (foreground: rest, disabled — stroke: rest, hover, pressed)
  - [x] 2.1.3 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.4 متغیرهای radius, spacing, size, transition
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.radio` (wrapper label) — inline-flex, align-items: center, gap, border-radius, cursor
  - [x] 2.2.2 ساختار `.radio__input` — visually hidden (position absolute, clip rect)
  - [x] 2.2.3 ساختار `.radio__label` — font, color, padding
  - [x] 2.2.4 ساختار `.radio__box` — flex container, centering, size 25px
  - [x] 2.2.5 ساختار `.radio__circle` — border 1px solid, border-radius 50%, size 17px
  - [x] 2.2.6 ساختار `.radio__dot` — border-radius 50%, size 9px, scale(0) default
- [x] 2.3 پیاده‌سازی حالت‌های Unchecked
  - [x] 2.3.1 Rest: border #626364
  - [x] 2.3.2 Hover: border #59595a
  - [x] 2.3.3 Pressed: border #4f4f50
  - [x] 2.3.4 Disabled: border #bbbcbe, label color #bbbcbe
- [x] 2.4 پیاده‌سازی حالت‌های Checked
  - [x] 2.4.1 Rest: border #26a88c, dot #26a88c, dot scale(1)
  - [x] 2.4.2 Hover: border #1d836d, dot #1d836d
  - [x] 2.4.3 Pressed: border #155e4e, dot #155e4e
  - [x] 2.4.4 Disabled: border #bbbcbe, dot #bbbcbe, label color #bbbcbe
- [x] 2.5 پیاده‌سازی Focus Ring
  - [x] 2.5.1 focus-visible: border 1px solid #222323 روی wrapper
  - [x] 2.5.2 بدون تغییر layout (transparent border default)
  - [x] 2.5.3 fallback برای مرورگرهای بدون :has() با @supports
- [x] 2.6 پیاده‌سازی اولویت stateها
  - [x] 2.6.1 disabled > pressed > focus > hover > rest
  - [x] 2.6.2 Disabled جلوگیری از hover/pressed/focus
- [x] 2.7 پیاده‌سازی Label
  - [x] 2.7.1 نمایش label متنی در کنار کنترل
  - [x] 2.7.2 رنگ label مطابق state (disabled → #bbbcbe)
  - [x] 2.7.3 بدون label: فقط کنترل دایره‌ای
- [x] 2.8 پشتیبانی RTL/LTR
  - [x] 2.8.1 در RTL: control سمت راست (start)، label سمت چپ (end)
  - [x] 2.8.2 در LTR: control سمت چپ (start)، label سمت راست (end)
- [x] 2.9 افزودن transition‌های نرم

## 3. تست و دمو
- [x] 3.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 3.1.1 نمایش تمام stateها — Unchecked (Rest, Hover, Pressed, Disabled, Focus)
  - [x] 3.1.2 نمایش تمام stateها — Checked
  - [x] 3.1.3 نمایش با و بدون Label
  - [x] 3.1.4 نمایش Radio Group (چند گزینه با name مشترک)
- [ ] 3.2 تست حالت‌های تعاملی
  - [ ] 3.2.1 Rest, Hover, Pressed — بررسی تغییرات بصری
  - [ ] 3.2.2 Focus — focus ring صحیح
  - [ ] 3.2.3 Disabled — عدم تعامل، رنگ‌های کمرنگ
  - [ ] 3.2.4 اولویت stateها: disabled > pressed > focus > hover > rest
- [ ] 3.3 تست Checked/Unchecked
  - [ ] 3.3.1 نمایش/مخفی شدن inner dot
  - [ ] 3.3.2 تغییر رنگ‌ها در حالت checked
  - [ ] 3.3.3 Radio Group: فقط یک انتخاب
- [ ] 3.4 تست RTL/LTR
  - [ ] 3.4.1 موقعیت صحیح control (start) و label (end) در RTL
  - [ ] 3.4.2 موقعیت صحیح control (start) و label (end) در LTR
- [ ] 3.5 تست دسترسی‌پذیری
  - [ ] 3.5.1 ناوبری با Tab
  - [ ] 3.5.2 انتخاب با Space/Enter
  - [ ] 3.5.3 Arrow keys در Radio Group
  - [ ] 3.5.4 Screen reader compatibility
  - [ ] 3.5.5 کنتراست رنگ (حداقل 3:1 برای non-text)
- [ ] 3.6 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 4. مستندات
- [x] 4.1 ایجاد README.md با نحوه استفاده و مثال‌ها
- [x] 4.2 مستندسازی CSS classes و API
- [x] 4.3 مستندسازی نحوه ساخت Radio Group
