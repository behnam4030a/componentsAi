# تسک‌های پیاده‌سازی کامپوننت Input

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/input/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `input.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ neutral (foreground: placeholder, text, disabled)
  - [x] 2.1.2 متغیرهای رنگ neutral (background: rest, readonly)
  - [x] 2.1.3 متغیرهای رنگ neutral (stroke: rest, hover, secondary, disabled, focused, selected)
  - [x] 2.1.4 متغیرهای رنگ danger (background, stroke)
  - [x] 2.1.5 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.6 متغیرهای radius, shadow, spacing, size
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.input` (wrapper) — position relative, width, border-radius
  - [x] 2.2.2 ساختار `.input__container` — flexbox, alignment, border, background, padding
  - [x] 2.2.3 ساختار `.input__field` — reset browser defaults, flex-grow, font, color, placeholder
  - [x] 2.2.4 ساختار `.input__icon` — flex-shrink, centering, size, color inheritance
  - [x] 2.2.5 ساختار `.input__divider` — vertical line, height based on size
  - [x] 2.2.6 ساختار `.input__indicator` — bottom line (1.5px), position absolute
- [x] 2.3 پیاده‌سازی سایزهای Input (Size Variants)
  - [x] 2.3.1 Large: height=45px, paddingX=16px, fontSize=14px, lineHeight=2, icon=20px, divider=16px
  - [x] 2.3.2 Medium: height=37px, paddingX=12px, fontSize=14px, lineHeight=2, icon=20px, divider=12px
  - [x] 2.3.3 Small: height=24px, paddingX=8px, fontSize=12px, lineHeight=1.5, icon=16px, divider=8px
- [x] 2.4 پیاده‌سازی حالت‌های تعاملی (State)
  - [x] 2.4.1 Rest: border #e2e4e6, background #ffffff, indicator hidden
  - [x] 2.4.2 Hover: border #d8dadc, cursor pointer, indicator visible (#c0c1c3)
  - [x] 2.4.3 Focused: border #f6f8fa, shadow focused, indicator visible (#2abb9c)
  - [x] 2.4.4 Error: border #c50f1f, background #fdf3f4, shadow error, indicator hidden
  - [x] 2.4.5 Disabled: border #dddfe1, text/placeholder/icon #bbbcbe, no interaction, indicator hidden
  - [x] 2.4.6 ReadOnly: no border, background #f6f8fa, indicator hidden
- [x] 2.5 پیاده‌سازی اولویت stateها با CSS specificity
  - [x] 2.5.1 disabled > error > focused > hover > rest
  - [x] 2.5.2 Disabled جلوگیری از hover/focused
  - [x] 2.5.3 Error + Focused ترکیبی (اگر تعریف شده)
- [x] 2.6 پیاده‌سازی استایل‌های همزمان state روی تمام عناصر
  - [x] 2.6.1 تغییر رنگ container (border, background, shadow) در هر state
  - [x] 2.6.2 تغییر رنگ text (input value) در هر state
  - [x] 2.6.3 تغییر رنگ placeholder در هر state
  - [x] 2.6.4 تغییر رنگ آیکن‌ها در هر state
  - [x] 2.6.5 تغییر وضعیت indicator در هر state
- [x] 2.7 پیاده‌سازی پشتیبانی RTL
  - [x] 2.7.1 موقعیت‌یابی آیکن‌ها با flexbox (RTL: before=راست، after=چپ)
  - [x] 2.7.2 text-align و direction صحیح
  - [x] 2.7.3 پشتیبانی LTR با `dir="ltr"`
- [x] 2.8 افزودن transition‌های نرم برای تغییرات state

## 3. آیکن‌ها و Divider
- [x] 3.1 پیاده‌سازی slot آیکن before (input__icon--before)
  - [x] 3.1.1 اندازه mapping: Large/Medium=20px, Small=16px
  - [x] 3.1.2 رنگ آیکن مطابق state (color inheritance)
- [x] 3.2 پیاده‌سازی slot آیکن after (input__icon--after)
  - [x] 3.2.1 اندازه ثابت 16px (طبق Figma)
  - [x] 3.2.2 رنگ آیکن مطابق state
- [x] 3.3 پیاده‌سازی divider عمودی
  - [x] 3.3.1 فقط بین beforeTextIcon و متن
  - [x] 3.3.2 ارتفاع وابسته به size: Large=16px, Medium=12px, Small=8px

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش تمام سایزها (Large, Medium, Small) در حالت Rest
  - [x] 4.1.2 نمایش تمام stateها (Rest, Hover, Focused, Error, Disabled, ReadOnly)
  - [x] 4.1.3 نمایش ترکیب‌های مختلف آیکن (بدون آیکن, فقط before, فقط after, هر دو)
  - [x] 4.1.4 نمایش با متن واردشده و placeholder
- [ ] 4.2 تست حالت‌های تعاملی (State)
  - [ ] 4.2.1 Rest, Hover, Focused — بررسی تغییرات بصری
  - [ ] 4.2.2 Error — border قرمز، background صورتی، shadow قرمز
  - [ ] 4.2.3 Disabled — عدم تعامل، رنگ‌های کمرنگ
  - [ ] 4.2.4 ReadOnly — قابل انتخاب، غیرقابل ویرایش
  - [ ] 4.2.5 اولویت stateها: disabled > error > focused > hover > rest
- [ ] 4.3 تست سایزها
  - [ ] 4.3.1 Large: ابعاد و فونت صحیح
  - [ ] 4.3.2 Medium: ابعاد و فونت صحیح
  - [ ] 4.3.3 Small: ابعاد و فونت صحیح
  - [ ] 4.3.4 بررسی تأثیر size روی height, padding, font, icon, divider
- [ ] 4.4 تست آیکن‌ها
  - [ ] 4.4.1 آیکن before با divider
  - [ ] 4.4.2 آیکن after
  - [ ] 4.4.3 هر دو آیکن همزمان
  - [ ] 4.4.4 بدون آیکن
  - [ ] 4.4.5 تغییر رنگ آیکن مطابق state
- [ ] 4.5 تست RTL
  - [ ] 4.5.1 موقعیت صحیح آیکن‌ها در RTL (before=راست, after=چپ)
  - [ ] 4.5.2 موقعیت صحیح آیکن‌ها در LTR (before=چپ, after=راست)
- [ ] 4.6 تست Accessible Indicator
  - [ ] 4.6.1 مخفی در Rest
  - [ ] 4.6.2 قابل مشاهده در Hover (#c0c1c3)
  - [ ] 4.6.3 قابل مشاهده در Focused (#2abb9c)
  - [ ] 4.6.4 مخفی در Error/Disabled/ReadOnly
- [ ] 4.7 تست ناوبری کیبورد
  - [ ] 4.7.1 Tab برای ورود به input
  - [ ] 4.7.2 تایپ متن
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
