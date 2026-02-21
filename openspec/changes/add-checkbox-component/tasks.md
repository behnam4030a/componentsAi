# تسک‌های پیاده‌سازی کامپوننت Checkbox

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/checkbox/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `checkbox.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ brand (background: rest, hover, pressed)
  - [x] 2.1.2 متغیرهای رنگ neutral (foreground, stroke, disabled)
  - [x] 2.1.3 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.4 متغیرهای radius, spacing, size
- [x] 2.2 پیاده‌سازی استایل‌های مخفی‌سازی native checkbox (visually-hidden)
- [x] 2.3 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.3.1 ساختار `.checkbox` (label wrapper) — flexbox, alignment, gap, cursor
  - [x] 2.3.2 ساختار `.checkbox__box` (boxholder) — اندازه, padding, centering
  - [x] 2.3.3 ساختار `.checkbox__inner` (باکس داخلی) — border-radius, border
  - [x] 2.3.4 ساختار `.checkbox__icon` — اندازه آیکون, centering
  - [x] 2.3.5 ساختار `.checkbox__label` — typography, color
- [x] 2.4 پیاده‌سازی سایزهای Checkbox (Size Variants)
  - [x] 2.4.1 Large: boxholder=16px, padding=6px, fontSize=14px
  - [x] 2.4.2 Medium: boxholder=16px, padding=4px, fontSize=12px
- [x] 2.5 پیاده‌سازی وضعیت‌های منطقی (Status)
  - [x] 2.5.1 Unchecked: باکس خالی با border (neutral stroke)
  - [x] 2.5.2 Checked: باکس پر با رنگ brand و آیکون checkmark سفید
  - [x] 2.5.3 Indeterminate: باکس پر با رنگ brand و آیکون minus سفید
- [x] 2.6 پیاده‌سازی حالت‌های تعاملی (State) برای Unchecked
  - [x] 2.6.1 Rest: border `#626364`
  - [x] 2.6.2 Hover: border `#59595a`
  - [x] 2.6.3 Pressed: border `#4f4f50`
  - [x] 2.6.4 Disabled: border `#dddfe1`، cursor: not-allowed
- [x] 2.7 پیاده‌سازی حالت‌های تعاملی (State) برای Checked/Indeterminate
  - [x] 2.7.1 Rest: background `#26a88c`، آیکون سفید
  - [x] 2.7.2 Hover: background `#22967d`
  - [x] 2.7.3 Pressed: background `#19705e`
  - [x] 2.7.4 Disabled: بدون background، border `#dddfe1`، آیکون `#bbbcbe`
- [x] 2.8 پیاده‌سازی حالت Focus
  - [x] 2.8.1 Focus ring: 1px solid `#222323` روی container خارجی
  - [x] 2.8.2 Focus ring با border-radius=4px (container radius)
  - [x] 2.8.3 فقط در keyboard navigation (`:focus-visible` با :has + fallback)
  - [x] 2.8.4 Focus بدون layout shift (transparent border by default)
  - [x] 2.8.5 Focus مستقل از Status — در هر سه وضعیت نمایش داده می‌شود
- [x] 2.9 اطمینان از عدم فعال شدن hover/pressed در حالت Disabled (با `:not(:disabled)`)
- [x] 2.10 پیاده‌سازی پشتیبانی RTL
  - [x] 2.10.1 Label در سمت راست box (RTL default طبق Figma)
  - [x] 2.10.2 پشتیبانی LTR با `dir="ltr"`
- [x] 2.11 افزودن transition‌های نرم برای تغییرات state

## 3. آیکون‌ها
- [x] 3.1 ایجاد SVG آیکون Checkmark (تیک) — inline، 10x10
- [x] 3.2 ایجاد SVG آیکون Minus (خط) — inline، 10x10
- [x] 3.3 اطمینان از استفاده `currentColor` برای رنگ آیکون‌ها

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش تمام ترکیبات Status × Size (6 ترکیب)
  - [x] 4.1.2 نمایش تمام حالت‌های State (Rest, Disabled)
  - [x] 4.1.3 نمایش با و بدون Label
  - [x] 4.1.4 نمایش Indeterminate state با مثال JavaScript
- [ ] 4.2 تست وضعیت‌های منطقی (Status)
  - [ ] 4.2.1 تست Unchecked → Checked → Unchecked toggle
  - [ ] 4.2.2 تست Indeterminate visual state
  - [ ] 4.2.3 تست اینکه Indeterminate مستقل از Checked/Unchecked مدیریت می‌شود
- [ ] 4.3 تست حالت‌های تعاملی (State)
  - [ ] 4.3.1 Rest, Hover, Pressed — بررسی تغییرات بصری
  - [ ] 4.3.2 Disabled — عدم تغییر Status، عدم فعال شدن hover/pressed/focus
- [ ] 4.4 تست سایزها
  - [ ] 4.4.1 Large: ابعاد و فونت صحیح
  - [ ] 4.4.2 Medium: ابعاد و فونت صحیح
  - [ ] 4.4.3 بررسی اینکه Size فقط بر ابعاد تأثیر دارد، نه رفتار
- [ ] 4.5 تست Label
  - [ ] 4.5.1 کلیک روی Label تغییر Status
  - [ ] 4.5.2 Checkbox بدون Label
  - [ ] 4.5.3 بررسی سایز فونت Label مطابق Size (14px/12px)
- [ ] 4.6 تست RTL
  - [ ] 4.6.1 موقعیت صحیح Label نسبت به Box
- [ ] 4.7 تست مدیریت Focus
  - [ ] 4.7.1 Focus ring در ناوبری کیبورد (Tab)
  - [ ] 4.7.2 عدم focus ring در کلیک موس
  - [ ] 4.7.3 Focus ring بدون layout shift
  - [ ] 4.7.4 Focus مستقل از Status
- [ ] 4.8 تست ناوبری کیبورد
  - [ ] 4.8.1 Toggle با Space
  - [ ] 4.8.2 ناوبری با Tab/Shift+Tab
- [ ] 4.9 تست دسترسی‌پذیری
  - [ ] 4.9.1 `aria-checked="mixed"` برای Indeterminate
  - [ ] 4.9.2 کنتراست رنگ (حداقل 4.5:1)
  - [ ] 4.9.3 Screen reader compatibility
- [ ] 4.10 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 5. مستندات
- [x] 5.1 مستندسازی CSS classes و نحوه استفاده (در index.html)
- [x] 5.2 مستندسازی نحوه تنظیم Indeterminate با JavaScript (در index.html)
- [x] 5.3 مثال‌های کد برای سناریوهای رایج (در index.html)
