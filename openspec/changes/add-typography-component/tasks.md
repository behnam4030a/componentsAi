# تسک‌های پیاده‌سازی کامپوننت Typography

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/typography/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS — Custom Properties
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیر font-family: `'Peyda(FaNum)', sans-serif`
  - [x] 2.1.2 متغیرهای Display: size 58px, weight 700, line-height 75px
  - [x] 2.1.3 متغیرهای Large Title: size 40px, weight 600, line-height 52px
  - [x] 2.1.4 متغیرهای Heading 1-6: sizes 32-16px, weights 700-500, line-height 1.3
  - [x] 2.1.5 متغیرهای Body Large: size 16px, weights 400/500, line-heights 2/1.5
  - [x] 2.1.6 متغیرهای Body Medium: size 14px, weights 400/500, line-heights 2/1.5
  - [x] 2.1.7 متغیرهای Body Small: size 12px, weights 400/500, line-heights 2/1.5
  - [x] 2.1.8 متغیرهای Caption: size 13px, weights 400/500, line-height 1.3
  - [x] 2.1.9 متغیرهای Button: sizes 14/12px, weight 500, line-height 1.4

## 3. پیاده‌سازی CSS — کلاس پایه
- [x] 3.1 `.typo` — font-family، letter-spacing: 0، text-align: right، direction: rtl

## 4. پیاده‌سازی CSS — Display & Title
- [x] 4.1 `.typo--display` — font-size 58px، font-weight 700، line-height 75px
- [x] 4.2 `.typo--large-title` — font-size 40px، font-weight 600، line-height 52px

## 5. پیاده‌سازی CSS — Headings
- [x] 5.1 `.typo--heading-1` — font-size 32px، font-weight 700، line-height 1.3
- [x] 5.2 `.typo--heading-2` — font-size 28px، font-weight 600، line-height 1.3
- [x] 5.3 `.typo--heading-3` — font-size 24px، font-weight 600، line-height 1.3
- [x] 5.4 `.typo--heading-4` — font-size 20px، font-weight 600، line-height 1.3
- [x] 5.5 `.typo--heading-5` — font-size 18px، font-weight 500، line-height 1.3
- [x] 5.6 `.typo--heading-6` — font-size 16px، font-weight 500، line-height 1.3

## 6. پیاده‌سازی CSS — Body Large
- [x] 6.1 `.typo--body-large-200` — font-size 16px، font-weight 400، line-height 2
- [x] 6.2 `.typo--body-large-150` — font-size 16px، font-weight 400، line-height 1.5
- [x] 6.3 `.typo--body-large-emp` — font-size 16px، font-weight 500، line-height 1.5

## 7. پیاده‌سازی CSS — Body Medium
- [x] 7.1 `.typo--body-medium-200` — font-size 14px، font-weight 400، line-height 2
- [x] 7.2 `.typo--body-medium-150` — font-size 14px، font-weight 400، line-height 1.5
- [x] 7.3 `.typo--body-medium-emp` — font-size 14px، font-weight 500، line-height 1.5

## 8. پیاده‌سازی CSS — Body Small
- [x] 8.1 `.typo--body-small-200` — font-size 12px، font-weight 400، line-height 2
- [x] 8.2 `.typo--body-small-150` — font-size 12px، font-weight 400، line-height 1.5
- [x] 8.3 `.typo--body-small-emp` — font-size 12px، font-weight 500، line-height 1.5

## 9. پیاده‌سازی CSS — Caption
- [x] 9.1 `.typo--caption` — font-size 13px، font-weight 400، line-height 1.3
- [x] 9.2 `.typo--caption-emp` — font-size 13px، font-weight 500، line-height 1.3

## 10. پیاده‌سازی CSS — Button
- [x] 10.1 `.typo--button-large` — font-size 14px، font-weight 500، line-height 1.4
- [x] 10.2 `.typo--button-medium` — font-size 14px، font-weight 500، line-height 1.4
- [x] 10.3 `.typo--button-small` — font-size 12px، font-weight 500، line-height 1.4

## 11. پیاده‌سازی CSS — RTL/LTR Support
- [x] 11.1 پشتیبانی از `[dir="ltr"]` برای text-align: left

## 12. دمو و ادغام
- [x] 12.1 ایجاد صفحه دمو (`index.html`) با نمایش تمام 22 استایل
  - [x] 12.1.1 بخش Display & Title
  - [x] 12.1.2 بخش Headings (1-6)
  - [x] 12.1.3 بخش Body (Large, Medium, Small با variant های 200, 150, emp)
  - [x] 12.1.4 بخش Caption و Caption Emphasis
  - [x] 12.1.5 بخش Button (Large, Medium, Small)
  - [x] 12.1.6 جدول مرجع (Style, Weight, Size, Line Height)
- [x] 12.2 اضافه کردن typography.css به `/index.html` اصلی پروژه
- [x] 12.3 اضافه کردن link به typography.css در تمام دمو صفحات کامپوننت‌های موجود
