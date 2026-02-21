# تسک‌های پیاده‌سازی کامپوننت Message Bar

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/message-bar/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS — Custom Properties
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ Info: bg #f3f9fd، stroke #0078d4، link #1a86d9
  - [x] 2.1.2 متغیرهای رنگ Success: bg #f1faf1، stroke #107c10
  - [x] 2.1.3 متغیرهای رنگ Warning: bg #fff9f5، stroke #f7630c
  - [x] 2.1.4 متغیرهای رنگ Danger: bg #fdf3f4، stroke #c50f1f
  - [x] 2.1.5 متغیرهای رنگ neutral: foreground primary #222323، secondary #59595a
  - [x] 2.1.6 متغیرهای typography: font-family، sizes، weights، line-height
  - [x] 2.1.7 متغیرهای spacing: padding، gap
  - [x] 2.1.8 متغیرهای size: border، radius، icon sizes

## 3. پیاده‌سازی CSS — ساختار پایه
- [x] 3.1 `.message-bar` — flex container، border 1px solid، radius 10px، padding 8px 19px، align-items center، overflow hidden
- [x] 3.2 `.message-bar__content` — flex container، آیکن + متن، gap 13px، align-items center
- [x] 3.3 `.message-bar__icon` — container آیکن وضعیت، سایز 40px، flex-shrink 0
- [x] 3.4 `.message-bar__text` — متن پیام، فونت Regular 18px، line-height 1.8، رنگ #222323
- [x] 3.5 `.message-bar__title` — بخش بولد متن (عنصر `<strong>`)، فونت SemiBold 18px

## 4. پیاده‌سازی CSS — واریانت Info (آبی)
- [x] 4.1 `.message-bar--info` — bg #f3f9fd، border-color #0078d4
- [x] 4.2 `.message-bar__link` — flex container، align-items center، text-decoration none
- [x] 4.3 `.message-bar__link-text` — فونت SemiBold 15px، رنگ #1a86d9
- [x] 4.4 `.message-bar__link-icon` — آیکن فلش چپ، سایز 32px (inner 24px)

## 5. پیاده‌سازی CSS — واریانت Success (سبز)
- [x] 5.1 `.message-bar--success` — bg #f1faf1، border-color #107c10
- [x] 5.2 `.message-bar__close` — دکمه بستن، سایز 28px، border none، bg transparent، cursor pointer
- [x] 5.3 آیکن بستن (X): سایز inner 24px، رنگ #59595a

## 5.5. پیاده‌سازی CSS — واریانت Warning (نارنجی)
- [x] 5.5.1 `.message-bar--warning` — bg #fff9f5، border-color #f7630c
- [x] 5.5.2 آیکن وضعیت: مثلث هشدار (danger triangle)، رنگ #f7630c
- [x] 5.5.3 دکمه بستن (X) — مشترک با Success

## 5.6. پیاده‌سازی CSS — واریانت Danger (قرمز)
- [x] 5.6.1 `.message-bar--danger` — bg #fdf3f4، border-color #c50f1f
- [x] 5.6.2 آیکن وضعیت: info circle، رنگ #c50f1f
- [x] 5.6.3 دکمه بستن (X) — مشترک با Success

## 6. پیاده‌سازی CSS — RTL و Hidden
- [x] 6.1 چینش flex: آیکن وضعیت سمت راست، عمل سمت چپ (justify-content space-between)
- [x] 6.2 direction و text-align مناسب RTL
- [x] 6.3 `.message-bar--hidden` — مخفی‌سازی با انیمیشن (opacity + height transition)

## 6.5. پیاده‌سازی CSS — Responsive Breakpoints
- [x] 6.5.1 Tablet (max-width: 767px): override custom properties — فونت 15px، آیکن 34px، padding فشرده
- [x] 6.5.2 Mobile (max-width: 479px): override custom properties — فونت 14px، آیکن 28px، padding کمتر
- [x] 6.5.3 Mobile Info: flex-wrap wrap — لینک به خط دوم
- [x] 6.5.4 Mobile Success/Warning/Danger: align-items flex-start — دکمه بستن بالا
- [x] 6.5.5 max-height افزایش یافته برای حالت wrap (300px → 400px در mobile)

## 7. پیاده‌سازی JavaScript — Core
- [x] 7.1 IIFE pattern + auto-init on DOMContentLoaded
- [x] 7.2 `MessageBar.init()` — فعال‌سازی event listenerها روی همه `[data-message-bar]`
- [x] 7.3 کلیک روی `.message-bar__close`: اضافه کردن کلاس `--hidden` و مخفی کردن

## 8. پیاده‌سازی JavaScript — API
- [x] 8.1 `MessageBar.show(element)` — نمایش یک message bar (حذف کلاس `--hidden`)
- [x] 8.2 `MessageBar.hide(element)` — مخفی کردن یک message bar (اضافه کردن کلاس `--hidden`)
- [x] 8.3 `MessageBar.onClose(element, fn)` — ثبت callback برای رویداد بستن

## 9. تست و دمو
- [x] 9.1 ایجاد صفحه دمو (index.html)
  - [x] 9.1.1 نمایش واریانت Info با لینک «بیشتر بدانید»
  - [x] 9.1.2 نمایش واریانت Success با دکمه بستن
  - [x] 9.1.3 نمایش واریانت Warning با دکمه بستن
  - [x] 9.1.4 نمایش واریانت Danger با دکمه بستن
  - [x] 9.1.5 نمایش تعامل بستن پیام (دمو تعاملی)
  - [x] 9.1.6 نمایش همه واریانت‌ها کنار هم
- [x] 9.2 اضافه کردن message-bar به index اصلی پروژه
  - [x] 9.2.1 لینک CSS و JS
  - [x] 9.2.2 یک مثال ساده
