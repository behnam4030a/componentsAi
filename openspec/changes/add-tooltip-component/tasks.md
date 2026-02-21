# تسک‌های پیاده‌سازی کامپوننت Tooltip

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/tooltip/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ: background (#364455), text (#ffffff)
  - [x] 2.1.2 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.3 متغیرهای radius, spacing, size
- [x] 2.2 پیاده‌سازی استایل‌های پایه
  - [x] 2.2.1 ساختار `.tooltip` (wrapper) — position relative, display inline-flex
  - [x] 2.2.2 ساختار `.tooltip__bubble` — position absolute, background, color, padding, border-radius, opacity 0
  - [x] 2.2.3 ساختار `.tooltip__arrow` — مثلث CSS با border
- [x] 2.3 پیاده‌سازی Position Variants
  - [x] 2.3.1 `.tooltip--top` — bubble بالای trigger, arrow پایین
  - [x] 2.3.2 `.tooltip--bottom` — bubble پایین trigger, arrow بالا
  - [x] 2.3.3 `.tooltip--right` — bubble سمت راست trigger, arrow سمت چپ
  - [x] 2.3.4 `.tooltip--left` — bubble سمت چپ trigger, arrow سمت راست
- [x] 2.4 پیاده‌سازی Visible State
  - [x] 2.4.1 `.tooltip--visible` — opacity 1
- [x] 2.5 پیاده‌سازی پشتیبانی RTL
  - [x] 2.5.1 text-align و direction صحیح
  - [x] 2.5.2 پشتیبانی LTR با `dir="ltr"`
- [x] 2.6 افزودن transition نرم (opacity)

## 3. پیاده‌سازی JavaScript
- [x] 3.1 پیاده‌سازی Auto-init
  - [x] 3.1.1 یافتن تمام المان‌های `[data-tooltip]`
  - [x] 3.1.2 ساخت خودکار bubble و arrow از متن `data-tooltip`
  - [x] 3.1.3 تنظیم `role="tooltip"` و `aria-describedby`
- [x] 3.2 پیاده‌سازی Show/Hide
  - [x] 3.2.1 Event listener برای `mouseenter` → نمایش
  - [x] 3.2.2 Event listener برای `mouseleave` → مخفی
  - [x] 3.2.3 Event listener برای `focusin` → نمایش
  - [x] 3.2.4 Event listener برای `focusout` → مخفی
  - [x] 3.2.5 تأخیر قابل تنظیم با `data-tooltip-delay`
- [x] 3.3 پیاده‌سازی Tooltip API
  - [x] 3.3.1 تابع `Tooltip.init(element)` برای فعال‌سازی تکی
  - [x] 3.3.2 تابع `Tooltip.initAll()` برای فعال‌سازی همه
  - [x] 3.3.3 متد `show()` / `hide()` برای کنترل دستی
  - [x] 3.3.4 متد `destroy()` برای cleanup
  - [x] 3.3.5 متد `setText()` برای تغییر متن

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش هر ۴ جهت (Top, Bottom, Right, Left)
  - [x] 4.1.2 نمایش روی آیکن info
  - [x] 4.1.3 نمایش ترکیب دکمه و آیکن (مطابق Figma)
  - [x] 4.1.4 نمایش با تأخیر سفارشی
- [ ] 4.2 تست جهت‌ها
  - [ ] 4.2.1 Top — bubble بالا, arrow پایین
  - [ ] 4.2.2 Bottom — bubble پایین, arrow بالا
  - [ ] 4.2.3 Right — bubble راست, arrow چپ
  - [ ] 4.2.4 Left — bubble چپ, arrow راست
- [ ] 4.3 تست رفتار
  - [ ] 4.3.1 نمایش هنگام hover
  - [ ] 4.3.2 مخفی شدن هنگام خروج mouse
  - [ ] 4.3.3 نمایش هنگام focus
  - [ ] 4.3.4 مخفی شدن هنگام blur
  - [ ] 4.3.5 تأخیر نمایش
- [ ] 4.4 تست RTL
  - [ ] 4.4.1 متن فارسی در RTL
  - [ ] 4.4.2 متن انگلیسی در LTR
- [ ] 4.5 تست دسترسی‌پذیری
  - [ ] 4.5.1 role="tooltip" و aria-describedby
  - [ ] 4.5.2 قابل دسترس با کیبورد (focus)
  - [ ] 4.5.3 Screen reader compatibility
- [ ] 4.6 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 5. مستندات
- [x] 5.1 مستندسازی CSS classes و نحوه استفاده (در index.html)
- [x] 5.2 مثال‌های کد برای سناریوهای رایج (در index.html)
- [x] 5.3 مستندسازی JavaScript API
- [x] 5.4 ایجاد README.md
