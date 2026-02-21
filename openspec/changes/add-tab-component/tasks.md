# تسک‌های پیاده‌سازی کامپوننت Tab

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/tab/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ: container-bg, active-text, inactive-text, brand
  - [x] 2.1.2 متغیرهای typography: font-family, font-size, line-height, font-weight-active, font-weight-inactive
  - [x] 2.1.3 متغیرهای spacing: container-padding-x, container-gap, item-padding-x, item-padding-y
  - [x] 2.1.4 متغیرهای size: container-height, filled-active-height, icon-size, badge-size, underline-border-width
  - [x] 2.1.5 متغیرهای radius: container, filled-active
- [x] 2.2 پیاده‌سازی Container
  - [x] 2.2.1 `.tab__list` — flex row, ارتفاع 48px, padding-x 24px, gap 12px, radius 8px
  - [x] 2.2.2 پس‌زمینه سفید (#ffffff) برای نوع underline
  - [x] 2.2.3 align-items center
- [x] 2.3 پیاده‌سازی Tab Items
  - [x] 2.3.1 `.tab__item` — padding 12px/16px, فونت 13px Regular (400), رنگ #59595a
  - [x] 2.3.2 `.tab__item--active` (underline) — فونت Medium (500), رنگ #222323, border-bottom 2px #26a88c
  - [x] 2.3.3 cursor pointer, transition نرم
- [x] 2.4 پیاده‌سازی Filled Variant
  - [x] 2.4.1 `.tab--filled .tab__list` — بدون پس‌زمینه سفید
  - [x] 2.4.2 `.tab--filled .tab__item--active` — پس‌زمینه #26a88c, رنگ سفید, ارتفاع 38px, radius 8px
- [x] 2.5 پیاده‌سازی Icon Support
  - [x] 2.5.1 `.tab__icon` — سایز 20px, فاصله 10px از متن
  - [x] 2.5.2 رنگ آیکن مطابق رنگ متن (فعال/غیرفعال)
- [x] 2.6 پیاده‌سازی Badge Support
  - [x] 2.6.1 `.tab__badge` — فونت سایز 15px, فاصله 5px از متن
  - [x] 2.6.2 رنگ badge مطابق رنگ متن (فعال/غیرفعال)
- [x] 2.7 پیاده‌سازی Tab Panels
  - [x] 2.7.1 `.tab__panel` — display none
  - [x] 2.7.2 `.tab__panel--active` — display block
- [x] 2.8 پیاده‌سازی RTL Support
  - [x] 2.8.1 چینش آیتم‌ها از راست به چپ
  - [x] 2.8.2 آیکن و badge در جهت صحیح

## 3. پیاده‌سازی JavaScript
- [x] 3.1 پیاده‌سازی Tab Switching
  - [x] 3.1.1 کلیک روی تب: فعال کردن تب و نمایش پنل مرتبط
  - [x] 3.1.2 حذف کلاس active از تب و پنل قبلی
  - [x] 3.1.3 اضافه کردن کلاس active به تب و پنل جدید
- [x] 3.2 پیاده‌سازی JavaScript API
  - [x] 3.2.1 `Tab.activate(groupId, index)` — فعال کردن تب با index
  - [x] 3.2.2 `Tab.init(element)` — فعال‌سازی یک تب جدید
  - [x] 3.2.3 `Tab.initAll()` — فعال‌سازی همه تب‌ها
  - [x] 3.2.4 `Tab.onChange(groupId, fn)` — callback تغییر تب
- [x] 3.3 پیاده‌سازی Keyboard Support
  - [x] 3.3.1 Arrow Right/Left برای جابجایی بین تب‌ها
  - [x] 3.3.2 Home/End برای رفتن به اولین/آخرین تب
  - [x] 3.3.3 Enter/Space برای فعال کردن تب
- [x] 3.4 پیاده‌سازی ARIA Attributes
  - [x] 3.4.1 `role="tablist"` روی container
  - [x] 3.4.2 `role="tab"` روی هر آیتم
  - [x] 3.4.3 `role="tabpanel"` روی هر پنل
  - [x] 3.4.4 `aria-selected="true/false"` روی تب‌ها
  - [x] 3.4.5 `aria-controls` و `aria-labelledby` اتصال تب به پنل
  - [x] 3.4.6 `tabindex` مدیریت (0 برای فعال، -1 برای غیرفعال)
- [x] 3.5 Auto-init
  - [x] 3.5.1 فعال‌سازی خودکار هنگام DOMContentLoaded
  - [x] 3.5.2 IIFE pattern مطابق سایر کامپوننت‌ها

## 4. تست و دمو
- [x] 4.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 4.1.1 نمایش تب underline (متن ساده)
  - [x] 4.1.2 نمایش تب filled (pill)
  - [x] 4.1.3 نمایش تب با آیکن
  - [x] 4.1.4 نمایش تب با badge
  - [x] 4.1.5 نمایش تب با پنل‌های محتوا
- [x] 4.2 اضافه کردن tab به index اصلی پروژه
  - [x] 4.2.1 لینک CSS و JS تب
  - [x] 4.2.2 یک مثال ساده از تب
