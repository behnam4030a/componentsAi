## ADDED Requirements

### Requirement: Message Bar Detailed Type
سیستم باید (SHALL) نوع Detailed را برای message bar پشتیبانی کند:
- عنوان: فونت Medium 16px، line-height 1.3
- توضیحات: فونت Regular 13px، line-height 1.3
- فاصله بین عنوان و توضیحات: 4px
- دکمه بستن (X)
- فعال‌سازی با modifier class `.message-bar--detailed`

### Requirement: Message Bar Auto-Dismiss
سیستم باید (SHALL) امکان بسته شدن خودکار message bar را پس از طی زمان مشخص فراهم کند:
- فعال‌سازی با attribute `data-auto-dismiss` با مقدار زمان (millisecond)
- پس از سپری شدن زمان، message bar مخفی شود
- در صورت بستن دستی قبل از تایمر، تایمر لغو شود

### Requirement: Message Bar Positioning
سیستم باید (SHALL) موقعیت نمایش message bar را قابل تنظیم کند:
- دسکتاپ: پیش‌فرض پایین صفحه سمت راست
- موبایل (<768px): پایین صفحه با تمام عرض و مارجین از اطراف
- موقعیت قابل تنظیم با `position` option در هرکجای صفحه

### Requirement: Message Bar Programmatic Creation
سیستم باید (SHALL) API `MessageBar.create(options)` را ارائه دهد:
- `options.type`: نوع واریانت ('info', 'success', 'warning', 'danger')
- `options.title`: عنوان پیام
- `options.description`: توضیحات (اختیاری — فعال‌سازی حالت Detailed)
- `options.autoDismiss`: زمان بسته شدن خودکار (ms) (اختیاری)
- `options.link`: آبجکت `{text, href}` برای لینک (اختیاری — فعال‌سازی حالت Actionable)
- `options.position`: موقعیت نمایش (اختیاری، پیش‌فرض: `'bottom-right'`)
- `options.container`: المان container (اختیاری — نمایش inline)

## MODIFIED Requirements

### Requirement: Message Bar Component Structure
سیستم باید (SHALL) کامپوننت Message Bar را در سه نوع اصلی ارائه دهد:
- **Dismissible**: فقط پیام + دکمه بستن (X)
- **Actionable**: پیام + لینک «بیشتر بدانید» (متن پیشفرض قابل تغییر)
- **Detailed**: عنوان + توضیحات + دکمه بستن

رنگ message barها کاملا نسبت به موضوع پیام قابل تغییر می‌باشد.

### Requirement: Message Bar JavaScript API
سیستم باید (SHALL) API زیر را از طریق شیء global `MessageBar` ارائه دهد:
- `MessageBar.init()` — فعال‌سازی event listenerها
- `MessageBar.show(element)` — نمایش message bar
- `MessageBar.hide(element)` — مخفی کردن message bar
- `MessageBar.onClose(element, fn)` — ثبت callback بستن
- `MessageBar.create(options)` — ساخت message bar از طریق JS
