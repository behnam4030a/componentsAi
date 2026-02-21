# تسک‌های پیاده‌سازی کامپوننت Table

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/table/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS — ساختار پایه
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ: primary-text, secondary-text, brand, stroke, light-bg, hover-bg
  - [x] 2.1.2 متغیرهای typography: font-family, sizes (20px, 14px, 13px), weights (400, 500, 600)
  - [x] 2.1.3 متغیرهای spacing: cell-padding, header-padding, gaps
  - [x] 2.1.4 متغیرهای size: row-height, header-height, checkbox, tag, pagination-btn, progress
  - [x] 2.1.5 متغیرهای radius: table, checkbox, tag, button, progress
  - [x] 2.1.6 متغیرهای shadow و border

## 3. پیاده‌سازی CSS — Tile Header
- [x] 3.1 `.table__header` — flex container، padding 16px 24px، gap 24px، bg سفید
- [x] 3.2 `.table__title-section` — عنوان SemiBold 20px + نقطه جداکننده + تعداد Regular 13px
- [x] 3.3 `.table__actions` — دکمه‌های عملیات سمت چپ
- [x] 3.4 `.table__btn--primary` — دکمه سبز bg #26a88c، border #1d836d، ارتفاع 45px، radius 8px، shadow inset
- [x] 3.5 `.table__btn--secondary` — دکمه سفید border #e2e4e6، ارتفاع 45px، radius 8px
- [x] 3.6 `.table__divider` — خط جداکننده عمودی 30px

## 4. پیاده‌سازی CSS — Search Box
- [x] 4.1 `.table__search` — ارتفاع 45px، bg سفید، border #e2e4e6، radius 8px
- [x] 4.2 آیکن جستجو 20px + placeholder «جستجو...» فونت Regular 14px #59595a

## 5. پیاده‌سازی CSS — Table Head
- [x] 5.1 `.table__row--head` — ارتفاع 55px، bg سفید، border-bottom 1px #e2e4e6
- [x] 5.2 `.table__cell` (در head) — padding 16px، فونت Regular 13px #59595a، gap 8px با آیکن
- [x] 5.3 `.table__cell--checkbox` — عرض ~52px برای ستون چک‌باکس

## 6. پیاده‌سازی CSS — Table Body
- [x] 6.1 `.table__row` — ارتفاع 60px، bg سفید، border-bottom 1px #e2e4e6
- [x] 6.2 `.table__cell` (در body) — padding 16px، فونت Regular 14px #222323
- [x] 6.3 حالت هاور: `.table__row:hover` — bg #f6f8fa + خط سبز عمودی 3px
- [x] 6.4 حالت انتخاب: `.table__row--selected` — checkbox checked
- [x] 6.5 آیکن سه‌نقطه: نمایش فقط هنگام هاور

## 7. پیاده‌سازی CSS — Checkbox
- [x] 7.1 `.table__checkbox` — سایز 28px، border 1px #626364، radius 4px
- [x] 7.2 حالت checked: bg #26a88c، آیکن سفید

## 8. پیاده‌سازی CSS — Status Tag
- [x] 8.1 `.table__tag` — ارتفاع 32px، bg #f6f8fa، border 2px سفید، radius 8px، padding 0 8px
- [x] 8.2 فونت Regular 14px #222323

## 9. پیاده‌سازی CSS — Progress Bar
- [x] 9.1 `.table__progress` — متن + نوار، gap 4px
- [x] 9.2 `.table__progress-bar` — عرض 120px، ارتفاع 3px، bg #e2e4e6، radius 360px
- [x] 9.3 `.table__progress-fill` — bg #26a88c، عرض متناسب

## 10. پیاده‌سازی CSS — Pagination
- [x] 10.1 `.table__pagination` — flex، justify-content space-between، padding 16px 24px
- [x] 10.2 `.table__page-btn` — 37×37px، radius 8px، border 1px #e2e4e6، shadow
- [x] 10.3 `.table__page-btn--active` — bg #26a88c، متن سفید، border #1d836d
- [x] 10.4 `.table__page-size` — «۱۰ ردیف در هر صفحه» سمت راست

## 11. پیاده‌سازی CSS — Action Bar
- [x] 11.1 `.table__action-bar` — bg #222323، padding 12px 24px، hidden by default
- [x] 11.2 `.table__action-bar--visible` — display flex
- [x] 11.3 `.table__action-count` — تعداد انتخاب شده، فونت Regular 14px سفید
- [x] 11.4 `.table__action-btn` — آیکن + متن سفید، فونت Regular 13px

## 12. پیاده‌سازی CSS — RTL Support
- [x] 12.1 چینش آیتم‌ها از راست به چپ
- [x] 12.2 ستون چک‌باکس سمت راست
- [x] 12.3 خط سبز هاور سمت چپ (border-left در RTL = border-inline-start)
- [x] 12.4 دکمه‌های toolbar سمت چپ، عنوان سمت راست

## 13. پیاده‌سازی JavaScript — Row Selection
- [x] 13.1 کلیک روی چک‌باکس ردیف: toggle انتخاب + اضافه/حذف کلاس `--selected`
- [x] 13.2 چک‌باکس header: انتخاب/لغو انتخاب همه ردیف‌ها
- [x] 13.3 نمایش/مخفی کردن Action Bar بر اساس تعداد ردیف‌های انتخاب شده
- [x] 13.4 به‌روزرسانی شمارنده ردیف‌های انتخاب شده

## 14. پیاده‌سازی JavaScript — Pagination
- [x] 14.1 نمایش/مخفی ردیف‌ها بر اساس صفحه فعال
- [x] 14.2 ساخت دکمه‌های شماره صفحه (با ... برای صفحات میانی)
- [x] 14.3 دکمه‌های ناوبری (اول، قبل، بعد، آخر)
- [x] 14.4 تغییر تعداد ردیف در هر صفحه

## 15. پیاده‌سازی JavaScript — Search
- [x] 15.1 فیلتر ردیف‌ها بر اساس متن جستجو (client-side)
- [x] 15.2 به‌روزرسانی پیجینیشن بعد از فیلتر

## 16. پیاده‌سازی JavaScript — API
- [x] 16.1 `Table.init(element)` — فعال‌سازی یک جدول
- [x] 16.2 `Table.initAll()` — فعال‌سازی همه جدول‌ها
- [x] 16.3 `Table.getSelected(tableId)` — دریافت ردیف‌های انتخاب شده
- [x] 16.4 `Table.selectAll(tableId)` — انتخاب همه
- [x] 16.5 `Table.deselectAll(tableId)` — لغو انتخاب همه
- [x] 16.6 `Table.goToPage(tableId, page)` — رفتن به صفحه
- [x] 16.7 `Table.onSelect(tableId, fn)` — callback انتخاب
- [x] 16.8 `Table.onPageChange(tableId, fn)` — callback تغییر صفحه
- [x] 16.9 Auto-init هنگام DOMContentLoaded + IIFE pattern

## 17. تست و دمو
- [x] 17.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 17.1.1 جدول کامل با toolbar، search، header، body، pagination
  - [x] 17.1.2 نمایش حالت‌های hover، selected، action bar
  - [x] 17.1.3 نمایش تگ وضعیت و نوار پیشرفت
- [x] 17.2 اضافه کردن table به index اصلی پروژه
  - [x] 17.2.1 لینک CSS و JS جدول
  - [x] 17.2.2 یک مثال ساده از جدول
