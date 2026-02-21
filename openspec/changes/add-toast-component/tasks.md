# تسک‌های پیاده‌سازی کامپوننت Toast

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/toast/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ status (success, danger, warning, neutral): foreground, background, stroke, bar
  - [x] 2.1.2 متغیرهای رنگ neutral (background, title foreground, description foreground, close icon)
  - [x] 2.1.3 متغیرهای shadow برای هر واریانت
  - [x] 2.1.4 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.5 متغیرهای radius, spacing, size
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.toast` (wrapper) — position relative, width 420px, border-radius 8px, background white, overflow clip
  - [x] 2.2.2 ساختار `.toast__dismiss` — دکمه بستن, position, cursor pointer
  - [x] 2.2.3 ساختار `.toast__inner` — flex row, gap 16px, align items center
  - [x] 2.2.4 ساختار `.toast__content` — flex column, gap 4px, padding-y 8px, text-align right
  - [x] 2.2.5 ساختار `.toast__title` — font 18px, weight 500, line-height 1.3, color #222323
  - [x] 2.2.6 ساختار `.toast__description` — font 14px, weight 400, line-height 1.5, color #59595a
  - [x] 2.2.7 ساختار `.toast__icon` — دایره رنگی, padding 12px, border-radius 360px
  - [x] 2.2.8 ساختار `.toast__progress` — position absolute bottom, left/right -2px
  - [x] 2.2.9 ساختار `.toast__progress-bar` — height 3px, border-radius 8px, animation linear
- [x] 2.3 پیاده‌سازی واریانت‌ها (State Variants)
  - [x] 2.3.1 Success: icon fg #107c10, icon bg #f1faf1, icon stroke #9fd89f, bar #107c10, shadow green
  - [x] 2.3.2 Danger: icon fg #c50f1f, icon bg #fdf3f4, icon stroke #eeacb2, bar #c50f1f, shadow red
  - [x] 2.3.3 Warning: icon fg #f7630c, icon bg #fff9f5, icon stroke #fdcfb4, bar #f7630c, shadow orange
  - [x] 2.3.4 Neutral: icon fg #454546, icon bg #f6f8fa, icon stroke #e2e4e6, bar #454546, shadow gray
- [x] 2.4 پیاده‌سازی Timer Indicator Animation
  - [x] 2.4.1 تعریف `@keyframes` برای progress bar (width: 100% → 0%)
  - [x] 2.4.2 `animation-timing-function: linear`
  - [x] 2.4.3 `animation-duration` قابل تنظیم (پیش‌فرض 5 ثانیه)
- [x] 2.5 پیاده‌سازی پشتیبانی RTL
  - [x] 2.5.1 text-align و direction صحیح
  - [x] 2.5.2 ترتیب المان‌ها: dismiss سمت راست، آیکن سمت چپ در RTL
  - [x] 2.5.3 پشتیبانی LTR با `dir="ltr"`
- [x] 2.6 افزودن transition‌های نرم

## 3. پیاده‌سازی JavaScript
- [x] 3.1 پیاده‌سازی Dismiss Button
  - [x] 3.1.1 Event listener برای کلیک روی dismiss button
  - [x] 3.1.2 توقف تایمر/انیمیشن هنگام dismiss
  - [x] 3.1.3 حذف Toast از DOM (یا callback به سیستم بالادستی)
- [x] 3.2 پیاده‌سازی Auto Dismiss (Timer)
  - [x] 3.2.1 شروع انیمیشن progress bar هنگام نمایش Toast
  - [x] 3.2.2 `animationend` event listener برای حذف خودکار
  - [x] 3.2.3 مدت زمان قابل تنظیم (data attribute یا JavaScript API)
- [x] 3.3 پیاده‌سازی Toast API
  - [x] 3.3.1 تابع init برای فعال‌سازی خودکار dismiss و timer
  - [x] 3.3.2 Cleanup event listeners هنگام حذف
  - [x] 3.3.3 تابع `Toast.show(options)` برای ایجاد دینامیک Toast با آیکن‌ها و role خودکار
  - [x] 3.3.4 آیکن‌های پیش‌فرض (ICONS) و نقش‌ها (ROLES) داخل toast.js
  - [x] 3.3.5 ساخت خودکار container در صورت نبود

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش تمام واریانت‌ها (Success, Danger, Warning, Neutral)
  - [x] 4.1.2 نمایش با و بدون description
  - [x] 4.1.3 نمایش عملکرد timer indicator
  - [x] 4.1.4 نمایش عملکرد dismiss button
- [ ] 4.2 تست واریانت‌ها
  - [ ] 4.2.1 Success — رنگ‌ها و shadow سبز
  - [ ] 4.2.2 Danger — رنگ‌ها و shadow قرمز
  - [ ] 4.2.3 Warning — رنگ‌ها و shadow نارنجی
  - [ ] 4.2.4 Neutral — رنگ‌ها و shadow خاکستری
- [ ] 4.3 تست Timer Indicator
  - [ ] 4.3.1 انیمیشن linear از full به empty
  - [ ] 4.3.2 حذف خودکار پس از اتمام تایمر
  - [ ] 4.3.3 مدت زمان قابل تنظیم
- [ ] 4.4 تست Manual Dismiss
  - [ ] 4.4.1 کلیک dismiss — توقف تایمر و حذف Toast
  - [ ] 4.4.2 Keyboard dismiss — دسترسی با Tab و Enter/Space
- [ ] 4.5 تست Description Optional
  - [ ] 4.5.1 با description — layout صحیح
  - [ ] 4.5.2 بدون description — بدون فضای خالی اضافی
- [ ] 4.6 تست RTL
  - [ ] 4.6.1 متن و ترتیب المان‌ها در RTL
  - [ ] 4.6.2 متن و ترتیب المان‌ها در LTR
- [ ] 4.7 تست دسترسی‌پذیری
  - [ ] 4.7.1 role="status" برای Success/Neutral
  - [ ] 4.7.2 role="alert" برای Danger/Warning
  - [ ] 4.7.3 dismiss button قابل دسترس با کیبورد
  - [ ] 4.7.4 Screen reader compatibility
- [ ] 4.8 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 5. مستندات
- [x] 5.1 مستندسازی CSS classes و نحوه استفاده (در index.html)
- [x] 5.2 مثال‌های کد برای سناریوهای رایج (در index.html)
- [x] 5.3 مستندسازی JavaScript API
- [x] 5.4 ایجاد README.md
