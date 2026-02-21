# تسک‌های بروزرسانی کامپوننت Table — Mobile Card Layout

## 1. بروزرسانی Design Tokens
- [x] 1.1 اضافه کردن توکن‌های موبایل به `tokens.json`
- [x] 1.2 اضافه کردن CSS custom properties موبایل به `:root` در `table.css`

## 2. بروزرسانی HTML — ساختار کارتی موبایل
- [x] 2.1 اضافه کردن `data-label` attributes به سلول‌های `<td>` برای نمایش label در موبایل
- [x] 2.2 اضافه کردن ردیف «انتخاب همه» + دکمه «فعالیت گروهی» بالای جدول
- [x] 2.3 اضافه کردن دکمه «بارگذاری گروهی» در هدر (دسکتاپ + موبایل) — قبلاً وجود داشت

## 3. پیاده‌سازی CSS — هدر موبایل
- [x] 3.1 Responsive header: عنوان + تعداد در یک ردیف
- [x] 3.2 دکمه‌ها full-width و کنار هم
- [x] 3.3 فیلتر + جستجو در یک ردیف

## 4. پیاده‌سازی CSS — کارت موبایل
- [x] 4.1 تبدیل `<table>` به لیست کارت‌ها با CSS (`display: block` + `data-label`)
- [x] 4.2 هدر کارت: checkbox + کد اختصاصی + دکمه ⋮
- [x] 4.3 بدنه کارت: key-value ردیف‌ها با divider
- [x] 4.4 Progress bar در کارت (عرض ۱۰۰px)
- [x] 4.5 Status tag در کارت
- [x] 4.6 حالت Selected: border-inline-start سبز + checkbox سبز

## 5. پیاده‌سازی CSS — فوتر موبایل
- [x] 5.1 Pagination در موبایل (دکمه‌های شماره صفحه + prev/next)
- [x] 5.2 دکمه «ردیف در هر صفحه» full-width

## 6. بروزرسانی JavaScript
- [x] 6.1 Selection/deselection در حالت کارتی
- [x] 6.2 Select All در حالت موبایل
- [x] 6.3 Pagination و Search سازگار با کارت‌ها
- [x] 6.4 Action bar در موبایل
- [x] 6.5 Row action menu (⋮) در کارت‌ها — CSS visibility:visible

## 7. بروزرسانی دمو صفحه
- [x] 7.1 بروزرسانی `index.html` با ساختار HTML جدید
- [x] 7.2 اضافه کردن دکمه «بارگذاری گروهی» به هدر — قبلاً وجود داشت
- [x] 7.3 تست حالت موبایل و دسکتاپ
