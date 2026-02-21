# Change: Add Free-Input Mode to Tagify Select

## Why
در حال حاضر کامپوننت Tagify فقط به کاربر اجازه می‌دهد از آیتم‌های از پیش تعریف‌شده در dropdown انتخاب کند. نیاز است کاربر بتواند با تایپ کردن مستقیم در trigger، تگ‌های دلخواه خود را نیز اضافه کند (مشابه رفتار input‌های tag در سیستم‌های مدیریت محتوا).

## What Changes
- افزودن حالت `data-free-input="true"` به نوع Tagify که یک inline text input در trigger نمایش می‌دهد
- با فشار دادن Enter یا کاما (`,`) در inline input، تگ جدید ایجاد می‌شود
- با فشار دادن Backspace در inline input خالی، آخرین تگ حذف می‌شود
- Inline input placeholder را از `data-placeholder` می‌گیرد
- dropdown همچنان برای انتخاب آیتم‌های از پیش تعریف‌شده کار می‌کند (اگر وجود داشته باشد)
- تگ‌های free-input مقداری برابر با متن وارد شده دارند (اگر `data-value` نداشته باشند)
- API: `getValue()` مقادیر هر دو نوع تگ (predefined + free-input) را برمی‌گرداند

## Impact
- Affected specs: `add-select-component` → requirement "Select Types" و "Tag System"
- Affected code: `components/select/select.js`, `components/select/select.css`, `components/select/index.html`, `components/select/README.md`
