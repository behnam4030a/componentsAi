# تسک‌های پیاده‌سازی کامپوننت Textarea

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/textarea/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `textarea.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ neutral (foreground: placeholder, text, disabled)
  - [x] 2.1.2 متغیرهای رنگ neutral (background: rest, readonly)
  - [x] 2.1.3 متغیرهای رنگ neutral (stroke: rest, hover, disabled, accessible rest/hover/selected)
  - [x] 2.1.4 متغیرهای رنگ danger (background, stroke)
  - [x] 2.1.5 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.6 متغیرهای radius, shadow, spacing, size
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.textarea` (wrapper) — position relative, width, border-radius, overflow clip
  - [x] 2.2.2 ساختار `.textarea__container` — flex, border, background, padding, border-radius
  - [x] 2.2.3 ساختار `.textarea__field` — reset browser defaults, flex-grow, font, color, placeholder, multi-line, text-align right
  - [x] 2.2.4 ساختار `.textarea__indicator` — bottom line (1.5px), position absolute
- [x] 2.3 پیاده‌سازی سایزهای Textarea (Size Variants)
  - [x] 2.3.1 Large: min-height=72px, paddingX=16px, paddingY=8px, fontSize=14px, lineHeight=2
  - [x] 2.3.2 Medium: min-height=64px, paddingX=12px, paddingY=8px, fontSize=14px, lineHeight=2
  - [x] 2.3.3 Small: min-height=36px, paddingX=8px, paddingY=8px, fontSize=12px, lineHeight=1.5
- [x] 2.4 پیاده‌سازی حالت‌های تعاملی (State)
  - [x] 2.4.1 Rest: border #e2e4e6, background #ffffff, indicator hidden
  - [x] 2.4.2 Hover: border #d8dadc, indicator visible (#59595a)
  - [x] 2.4.3 Focused: border #e2e4e6, shadow focused, indicator visible (#2abb9c)
  - [x] 2.4.4 Error: outer border #c50f1f, inner border #e2e4e6, background #fdf3f4, indicator hidden
  - [x] 2.4.5 Disabled: border #dddfe1, text/placeholder #bbbcbe, no interaction, indicator hidden
  - [x] 2.4.6 ReadOnly: no border, background #f6f8fa, indicator hidden
- [x] 2.5 پیاده‌سازی اولویت stateها با CSS specificity
  - [x] 2.5.1 disabled > error > focused > hover > rest
  - [x] 2.5.2 Disabled جلوگیری از hover/focused
  - [x] 2.5.3 Error + Focused ترکیبی
- [x] 2.6 پیاده‌سازی استایل‌های همزمان state روی تمام عناصر
  - [x] 2.6.1 تغییر رنگ container (border, background, shadow) در هر state
  - [x] 2.6.2 تغییر رنگ text (textarea value) در هر state
  - [x] 2.6.3 تغییر رنگ placeholder در هر state
  - [x] 2.6.4 تغییر وضعیت indicator در هر state
- [x] 2.7 پیاده‌سازی پشتیبانی RTL
  - [x] 2.7.1 text-align و direction صحیح
  - [x] 2.7.2 موقعیت resize handler (توسط مرورگر مدیریت می‌شود)
  - [x] 2.7.3 پشتیبانی LTR با `dir="ltr"`
- [x] 2.8 افزودن transition‌های نرم برای تغییرات state

## 3. Resize Handler
- [x] 3.1 پیاده‌سازی resize handler
  - [x] 3.1.1 با resizeHandler: `resize: vertical` فعال با کلاس `textarea--resizable`
  - [x] 3.1.2 بدون resizeHandler: `resize: none` (پیش‌فرض)
  - [x] 3.1.3 در حالت disabled: resize غیرفعال حتی اگر resizeHandler = true
  - [x] 3.1.4 resize نباید استایل stateها را تغییر دهد

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش تمام سایزها (Large, Medium, Small) در حالت Rest
  - [x] 4.1.2 نمایش تمام stateها (Rest, Hover, Focused, Error, Disabled, ReadOnly)
  - [x] 4.1.3 نمایش با و بدون resize handler
  - [x] 4.1.4 نمایش با متن واردشده و placeholder
- [ ] 4.2 تست حالت‌های تعاملی (State)
  - [ ] 4.2.1 Rest, Hover, Focused — بررسی تغییرات بصری
  - [ ] 4.2.2 Error — border قرمز، background صورتی
  - [ ] 4.2.3 Disabled — عدم تعامل، رنگ‌های کمرنگ، resize غیرفعال
  - [ ] 4.2.4 ReadOnly — قابل انتخاب، غیرقابل ویرایش
  - [ ] 4.2.5 اولویت stateها: disabled > error > focused > hover > rest
- [ ] 4.3 تست سایزها
  - [ ] 4.3.1 Large: ابعاد و فونت صحیح
  - [ ] 4.3.2 Medium: ابعاد و فونت صحیح
  - [ ] 4.3.3 Small: ابعاد و فونت صحیح
  - [ ] 4.3.4 بررسی تأثیر size روی min-height, padding, font
- [ ] 4.4 تست Resize Handler
  - [ ] 4.4.1 resize فعال (عمودی) با handler قابل مشاهده
  - [ ] 4.4.2 resize غیرفعال و handler مخفی
  - [ ] 4.4.3 resize غیرفعال در حالت disabled
- [ ] 4.5 تست RTL
  - [ ] 4.5.1 متن از سمت راست در RTL
  - [ ] 4.5.2 متن از سمت چپ در LTR
  - [ ] 4.5.3 موقعیت resize handler صحیح
- [ ] 4.6 تست Accessible Indicator
  - [ ] 4.6.1 مخفی در Rest
  - [ ] 4.6.2 قابل مشاهده در Hover (#59595a)
  - [ ] 4.6.3 قابل مشاهده در Focused (#2abb9c)
  - [ ] 4.6.4 مخفی در Error/Disabled/ReadOnly
- [ ] 4.7 تست ناوبری کیبورد
  - [ ] 4.7.1 Tab برای ورود به textarea
  - [ ] 4.7.2 تایپ متن چندخطی (Enter برای خط جدید)
  - [ ] 4.7.3 Shift+Tab برای خروج
- [ ] 4.8 تست دسترسی‌پذیری
  - [ ] 4.8.1 `aria-invalid` برای Error state
  - [ ] 4.8.2 کنتراست رنگ (حداقل 4.5:1)
  - [ ] 4.8.3 Screen reader compatibility
- [ ] 4.9 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 5. مستندات
- [x] 5.1 مستندسازی CSS classes و نحوه استفاده (در index.html)
- [x] 5.2 مثال‌های کد برای سناریوهای رایج (در index.html)
- [x] 5.3 مستندسازی نحوه set کردن Error state با JavaScript
