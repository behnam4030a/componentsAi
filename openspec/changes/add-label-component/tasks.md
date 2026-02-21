# تسک‌های پیاده‌سازی کامپوننت Label

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/label/`
- [x] 1.2 ایجاد فایل `tokens.json` با design tokens استخراج شده از Figma
- [x] 1.3 ایجاد فایل `label.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
  - [x] 2.1.1 متغیرهای رنگ (text: #222323, disabled: #bbbcbe, required: #c50f1f)
  - [x] 2.1.2 متغیرهای typography (fontFamily, fontSize, fontWeight, lineHeight)
  - [x] 2.1.3 متغیرهای spacing (gap: 4px)
- [x] 2.2 پیاده‌سازی استایل‌های پایه کامپوننت
  - [x] 2.2.1 ساختار `.label` (wrapper) — inline-flex, gap, align-items: start
  - [x] 2.2.2 ساختار `.label__text` — رنگ متن، font inheritance
  - [x] 2.2.3 ساختار `.label__required` — رنگ قرمز (danger)، flex-shrink: 0
- [x] 2.3 پیاده‌سازی سایزها (Size Variants)
  - [x] 2.3.1 Large Regular: fontSize=16px, fontWeight=400, lineHeight=1.5
  - [x] 2.3.2 Medium Regular: fontSize=14px, fontWeight=400, lineHeight=1.5
  - [x] 2.3.3 Small Regular: text=12px/1.5, asterisk=13px/1.3
  - [x] 2.3.4 Large Semibold: fontSize=16px, fontWeight=500, lineHeight=1.5
  - [x] 2.3.5 Medium Semibold: fontSize=12px, fontWeight=500, lineHeight=1.5
  - [x] 2.3.6 Small Semibold: text=12px/500/1.5, asterisk=13px/500/1.3
- [x] 2.4 پیاده‌سازی type (Font Weight)
  - [x] 2.4.1 Regular: fontWeight=400 (پیش‌فرض)
  - [x] 2.4.2 Semibold: fontWeight=500 (با `.label--semibold`)
  - [x] 2.4.3 type فقط font-weight را تغییر دهد، نه رنگ/اندازه/فاصله
- [x] 2.5 پیاده‌سازی حالت Disabled
  - [x] 2.5.1 متن و ستاره هر دو رنگ #bbbcbe
  - [x] 2.5.2 Disabled با class `.label--disabled`
- [x] 2.6 پیاده‌سازی Required Indicator
  - [x] 2.6.1 ستاره (*) با رنگ #c50f1f در حالت عادی
  - [x] 2.6.2 ستاره با رنگ #bbbcbe در حالت disabled
  - [x] 2.6.3 جایگاه ستاره: بعد از متن (end side)
- [x] 2.7 پشتیبانی RTL/LTR
  - [x] 2.7.1 در RTL: متن سمت راست، ستاره سمت چپ (end)
  - [x] 2.7.2 در LTR: متن سمت چپ، ستاره سمت راست (end)
  - [x] 2.7.3 استفاده از flexbox direction خودکار

## 3. تست و دمو
- [x] 3.1 ایجاد صفحه دمو (index.html) با مثال‌های جامع
  - [x] 3.1.1 نمایش تمام سایزها (Large, Medium, Small) در حالت Regular
  - [x] 3.1.2 نمایش تمام سایزها در حالت Semibold
  - [x] 3.1.3 نمایش حالت‌های Required و بدون Required
  - [x] 3.1.4 نمایش حالت Disabled (با و بدون Required)
  - [x] 3.1.5 نمایش ترکیب‌های مختلف (type × size × required × disabled)
- [ ] 3.2 تست تایپوگرافی
  - [ ] 3.2.1 Large Regular: 16px/400/1.5
  - [ ] 3.2.2 Medium Regular: 14px/400/1.5
  - [ ] 3.2.3 Small Regular: text=12px/400/1.5, asterisk=13px/400/1.3
  - [ ] 3.2.4 Large Semibold: 16px/500/1.5
  - [ ] 3.2.5 Medium Semibold: 12px/500/1.5
  - [ ] 3.2.6 Small Semibold: text=12px/500/1.5, asterisk=13px/500/1.3
- [ ] 3.3 تست رنگ‌ها
  - [ ] 3.3.1 متن عادی: #222323
  - [ ] 3.3.2 متن disabled: #bbbcbe
  - [ ] 3.3.3 ستاره عادی: #c50f1f
  - [ ] 3.3.4 ستاره disabled: #bbbcbe
- [ ] 3.4 تست RTL/LTR
  - [ ] 3.4.1 موقعیت صحیح ستاره در RTL (سمت چپ متن — end)
  - [ ] 3.4.2 موقعیت صحیح ستاره در LTR (سمت راست متن — end)
- [ ] 3.5 تست دسترسی‌پذیری
  - [ ] 3.5.1 استفاده از `<label>` semantics
  - [ ] 3.5.2 کنتراست رنگ (حداقل 4.5:1)
  - [ ] 3.5.3 Screen reader compatibility
- [ ] 3.6 تست سازگاری مرورگرها (Chrome, Firefox, Safari, Edge)

## 4. مستندات
- [x] 4.1 ایجاد README.md با نحوه استفاده و مثال‌ها
- [x] 4.2 مستندسازی CSS classes و API
- [x] 4.3 مستندسازی ترکیب properties (type × size × required × disabled)
