# تسک‌های پیاده‌سازی

## 1. راه‌اندازی و ساختار
- [x] 1.1 ایجاد دایرکتوری `/components/button/`
- [x] 1.2 ایجاد فایل `button.css` برای استایل‌های کامپوننت

## 2. پیاده‌سازی CSS
- [x] 2.1 ایجاد CSS custom properties از tokens.json
- [x] 2.2 پیاده‌سازی استایل‌های پایه دکمه (فقط ساختار، بدون رنگ‌های مخصوص type)
- [x] 2.3 پیاده‌سازی انواع دکمه (Primary، AI، Secondary، Subtle، Outline، Transparent)
  - [x] 2.3.1 اطمینان از اینکه type فقط روی رنگ‌ها، پس‌زمینه‌ها، borderها و سایه‌ها تأثیر می‌گذارد (نه ساختار)
  - [x] 2.3.2 بررسی اینکه همه typeها در همه sizeها کار می‌کنند
- [x] 2.4 پیاده‌سازی سایزهای دکمه (Large، Medium، Small)
  - [x] 2.4.1 Height، padding، font-size، line-height
  - [x] 2.4.2 Gap آیکن-متن (وابسته به size)
- [x] 2.5 پیاده‌سازی استایل‌های state (Rest، Hover، Pressed، Selected)
  - [x] 2.5.1 Hover با `:hover` pseudo-class
  - [x] 2.5.2 Pressed با `:active` pseudo-class
  - [x] 2.5.3 Selected با `.btn--selected` class
  - [x] 2.5.4 Disabled با `.btn--disabled` class
- [x] 2.6 پیاده‌سازی افکت‌های سایه برای هر type
- [x] 2.7 پیاده‌سازی استایل‌های focus ring
  - [x] 2.7.1 Focus ring خارج از مرز (بدون layout shift)
  - [x] 2.7.2 استایل‌های focus متفاوت برای Primary/AI در مقابل بقیه
  - [x] 2.7.3 فقط در keyboard navigation (`:focus-visible`)
- [x] 2.8 پیاده‌سازی پشتیبانی RTL با CSS logical properties
  - [x] 2.8.1 موقعیت‌یابی آیکن برای RTL/LTR
- [x] 2.9 افزودن انیمیشن‌های transition (تغییرات state نرم)
- [x] 2.10 پیاده‌سازی استایل‌های دکمه icon-only (padding مساوی)

## 3. تست
- [x] 3.1 ایجاد صفحه دمو (index.html) با مثال‌ها
- [ ] 3.2 تست همه انواع دکمه (6 نوع)
  - [ ] 3.2.1 بررسی اینکه type فقط روی استایل تأثیر می‌گذارد، نه ساختار
  - [ ] 3.2.2 تست همه typeها در همه sizeها
- [ ] 3.3 تست همه سایزهای دکمه (3 سایز)
  - [ ] 3.3.1 بررسی تغییرات height، padding، font، gap، icon size
- [ ] 3.4 تست همه stateها (4 حالت)
  - [ ] 3.4.1 Rest، Hover، Pressed، Selected
  - [ ] 3.4.2 Disabled
- [ ] 3.5 تست متن RTL
  - [ ] 3.5.1 موقعیت‌یابی آیکن در RTL
- [ ] 3.6 تست مدیریت focus
  - [ ] 3.6.1 Focus ring در ناوبری صفحه‌کلید (Tab)
  - [ ] 3.6.2 عدم focus ring در کلیک موس
  - [ ] 3.6.3 Focus ring بدون ایجاد layout shift
- [ ] 3.7 تست ناوبری صفحه‌کلید
  - [ ] 3.7.1 فعال‌سازی با کلید Enter
  - [ ] 3.7.2 فعال‌سازی با کلید Space
  - [ ] 3.7.3 ناوبری با Tab
- [ ] 3.8 تست دسترسی‌پذیری
  - [ ] 3.8.1 کنتراست رنگ (حداقل 4.5:1)
  - [ ] 3.8.2 نام دسترسی‌پذیر
- [ ] 3.9 تست سازگاری با مرورگرها (Chrome، Firefox، Safari، Edge)
- [ ] 3.10 تست پشتیبانی از لینک‌ها
  - [ ] 3.10.1 تست styling برای لینک‌ها در همه types و sizes
  - [ ] 3.10.2 تست حفظ href در لینک‌ها

## 4. مستندات
- [x] 4.1 ایجاد مثال‌های استفاده در صفحه دمو
- [ ] 4.2 مستندسازی CSS classes و نحوه استفاده
