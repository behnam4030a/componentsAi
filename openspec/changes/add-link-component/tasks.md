# تسک‌های پیاده‌سازی کامپوننت Link

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `components/link/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma

## 2. پیاده‌سازی CSS — Custom Properties
- [x] 2.1 ایجاد CSS custom properties در `:root`
  - [x] 2.1.1 `--link-color`: #0078d4
  - [x] 2.1.2 `--link-text-decoration`: underline

## 3. پیاده‌سازی CSS — کلاس `.link`
- [x] 3.1 color از `--link-color`
- [x] 3.2 text-decoration از `--link-text-decoration`
- [x] 3.3 cursor: pointer

## 4. دمو و ادغام
- [x] 4.1 ایجاد صفحه دمو (`index.html`)
  - [x] 4.1.1 لینک دادن typography.css در صفحه دمو
  - [x] 4.1.2 نمایش لینک بزرگ: `<a class="typo typo--body-large-200 link">`
  - [x] 4.1.3 نمایش لینک متوسط: `<a class="typo typo--body-medium-200 link">`
  - [x] 4.1.4 نمایش مثال کد HTML
- [x] 4.2 اضافه کردن link.css به `index.html` اصلی پروژه
