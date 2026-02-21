# تسک‌های پیاده‌سازی Tagify Free-Input

## 1. CSS
- [x] 1.1 افزودن استایل `.select__tag-input` — inline text input درون trigger
  - flex: 1, min-width: 60px, border: none, background: transparent, font inherit, outline: none
  - placeholder color: همان `--select-color-placeholder`

## 2. JavaScript
- [x] 2.1 خواندن `data-free-input` در `createInstance` و تنظیم `isFreeInput` flag
- [x] 2.2 ایجاد `<input type="text" class="select__tag-input">` در `renderTrigger` برای tagify free-input
  - قرار گرفتن inline input بعد از تگ‌ها، قبل از chevron
  - placeholder از `data-placeholder` — فقط وقتی هیچ تگی انتخاب نشده
- [x] 2.3 پیاده‌سازی تابع `addFreeTag(text)`:
  - trim کردن متن
  - جلوگیری از تگ خالی یا تکراری
  - فراخوانی `selectValue(text)` با مقدار متن
- [x] 2.4 Event listener روی inline input:
  - `keydown`: Enter → `addFreeTag` + پاک کردن input | کاما → `addFreeTag` + پاک کردن input | Backspace (خالی) → حذف آخرین تگ
  - `click`: `e.stopPropagation()` تا dropdown باز نشود
  - `focus`: اضافه کردن `select--active` به wrapper
- [x] 2.5 در `onTriggerClick`: اگر `isFreeInput` باشد و کلیک روی trigger اما نه روی تگ/دکمه‌ها، فوکوس به inline input بدهد (بدون toggle dropdown)
- [x] 2.6 در `close()`: اگر `isFreeInput`، فوکوس به inline input بدهد نه trigger اصلی

## 3. HTML Demo
- [x] 3.1 افزودن مثال tagify free-input در `index.html` با `data-free-input="true"`

## 4. مستندات
- [x] 4.1 بروزرسانی `README.md`: توضیح `data-free-input`, رفتار Enter/کاما/Backspace
