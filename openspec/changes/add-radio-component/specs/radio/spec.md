# مشخصات کامپوننت Radio

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Radio
کامپوننت Radio SHALL برای انتخاب یک گزینه از بین چند گزینه‌ی انحصاری استفاده شود. در هر گروه رادیویی، فقط یک Radio می‌تواند در حالت انتخاب‌شده باشد. این کامپوننت شامل کنترل دایره‌ای و در صورت نیاز Label متنی است.

#### Scenario: انتخاب یک گزینه انحصاری
- **زمانی که** کاربر نیاز به انتخاب یک گزینه از بین چند گزینه داشته باشد
- **آنگاه** از کامپوننت Radio استفاده شود

#### Scenario: جایگزین‌های Radio
- **زمانی که** تعداد گزینه‌ها بیش از پنج مورد باشد یا فضای کافی نباشد
- **آنگاه** از Dropdown یا Select استفاده شود
- **زمانی که** نیاز به انتخاب چندگانه باشد
- **آنگاه** از Checkbox استفاده شود

---

### Requirement: خصوصیت state (وضعیت تعاملی)
کامپوننت Radio SHALL پنج وضعیت تعاملی/سیستمی را پشتیبانی کند: Rest، Hover، Pressed، Focus و Disabled. State استایل کنترل و Label (در صورت وجود) را تعیین می‌کند.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** Radio SHALL در حالت پیش‌فرض نمایش داده شود
- **و** دایره unchecked SHALL با border #626364 نمایش داده شود
- **و** دایره checked SHALL با border و dot #26a88c نمایش داده شود

#### Scenario: حالت Hover
- **زمانی که** نشانگر روی ناحیه Radio یا Label قرار بگیرد و Radio غیرفعال نباشد
- **آنگاه** دایره unchecked SHALL با border #59595a نمایش داده شود
- **و** دایره checked SHALL با border و dot #1d836d نمایش داده شود

#### Scenario: حالت Pressed
- **زمانی که** کاربر کلیک کند یا بفشارد و Radio غیرفعال نباشد
- **آنگاه** دایره unchecked SHALL با border #4f4f50 نمایش داده شود
- **و** دایره checked SHALL با border و dot #155e4e نمایش داده شود
- **و** pressed SHALL فقط در زمان تعامل فعال باشد و بعد از رها شدن به rest یا focus برگردد

#### Scenario: حالت Focus
- **زمانی که** Radio فوکوس دریافت کند (keyboard یا click)
- **آنگاه** یک focus ring SHALL با border 1px solid #222323 و border-radius 4px روی wrapper نمایش داده شود
- **و** focus ring MUST NOT باعث تغییر اندازه layout شود

#### Scenario: حالت Disabled
- **زمانی که** Radio غیرفعال باشد
- **آنگاه** دایره SHALL با border #bbbcbe نمایش داده شود
- **و** در صورت checked بودن، dot نیز SHALL با رنگ #bbbcbe نمایش داده شود
- **و** متن Label (در صورت وجود) SHALL با رنگ #bbbcbe نمایش داده شود
- **و** هیچ state تعاملی دیگری (hover، pressed، focus) MUST NOT فعال شود
- **و** کلیک یا انتخاب MUST NOT مجاز باشد

#### Scenario: اولویت stateها
- **زمانی که** چند state همزمان فعال باشند
- **آنگاه** اولویت SHALL به ترتیب زیر باشد: disabled > pressed > focus > hover > rest

---

### Requirement: خصوصیت checked (وضعیت انتخاب)
کامپوننت Radio SHALL از وضعیت checked/unchecked پشتیبانی کند.

#### Scenario: حالت Unchecked
- **زمانی که** Radio انتخاب نشده باشد
- **آنگاه** فقط دایره بیرونی (outer circle) SHALL نمایش داده شود بدون نقطه داخلی

#### Scenario: حالت Checked
- **زمانی که** Radio انتخاب شده باشد
- **آنگاه** نشانگر داخلی (inner dot) SHALL داخل دایره Radio نمایش داده شود

#### Scenario: checked مستقل از state
- **زمانی که** Radio در حالت checked باشد
- **آنگاه** وضعیت checked SHALL مستقل از stateهای تعاملی پایدار بماند

#### Scenario: Radio Group
- **زمانی که** چند Radio با `name` مشترک در یک گروه باشند
- **آنگاه** انتخاب یکی SHALL باعث غیرفعال شدن سایر Radioهای همان گروه شود (رفتار بومی مرورگر)

---

### Requirement: خصوصیت label (برچسب متنی)
کامپوننت Radio SHALL از نمایش اختیاری Label متنی پشتیبانی کند.

#### Scenario: نمایش با Label
- **زمانی که** label فعال باشد
- **آنگاه** متن Label SHALL در کنار کنترل Radio نمایش داده شود
- **و** کلیک روی Label SHALL معادل کلیک روی خود Radio باشد

#### Scenario: نمایش بدون Label
- **زمانی که** label غیرفعال باشد
- **آنگاه** فقط کنترل دایره‌ای Radio SHALL نمایش داده شود
- **و** اندازه ناحیه قابل کلیک SHALL حداقل استاندارد دسترسی‌پذیری را رعایت کند

#### Scenario: استایل Label مطابق state
- **زمانی که** Label وجود داشته باشد
- **آنگاه** استایل متن Label SHALL با state Radio هماهنگ باشد
- **و** Label MUST NOT state مستقل داشته باشد

#### Scenario: Label در حالت Disabled
- **زمانی که** Radio در حالت disabled باشد و Label وجود داشته باشد
- **آنگاه** متن Label SHALL با رنگ disabled (#bbbcbe) نمایش داده شود

---

### Requirement: قوانین بصری کنترل (Radio Circle)
کامپوننت Radio SHALL شامل یک کنترل دایره‌ای با ساختار مشخص باشد.

#### Scenario: ساختار کنترل
- **زمانی که** Radio رندر شود
- **آنگاه** کنترل SHALL شامل دایره بیرونی (17px) و نشانگر داخلی (9px، فقط در checked) باشد

#### Scenario: رنگ‌بندی Unchecked
- **زمانی که** Radio در حالت unchecked باشد
- **آنگاه** border دایره SHALL از رنگ‌های neutral stroke استفاده کند:
  - Rest: #626364، Hover: #59595a، Pressed: #4f4f50، Disabled: #bbbcbe

#### Scenario: رنگ‌بندی Checked
- **زمانی که** Radio در حالت checked باشد
- **آنگاه** border دایره و رنگ dot SHALL از رنگ‌های brand foreground استفاده کند:
  - Rest: #26a88c، Hover: #1d836d، Pressed: #155e4e، Disabled: #bbbcbe

---

### Requirement: قوانین چیدمان (Layout Rules)
کامپوننت Radio SHALL ساختار داخلی منظم داشته باشد.

#### Scenario: ساختار بصری
- **زمانی که** Radio رندر شود
- **آنگاه** ساختار داخلی SHALL به صورت [radio control] [label (optional)] باشد (در RTL: control سمت راست، label سمت چپ)

#### Scenario: فاصله‌گذاری
- **زمانی که** Radio با Label رندر شود
- **آنگاه** gap بین المان‌ها SHALL 2px باشد
- **و** Label SHALL padding-start 8px داشته باشد

#### Scenario: تراز عمودی
- **زمانی که** کنترل و Label رندر شوند
- **آنگاه** تراز عمودی SHALL مرکزی (center) باشد

---

### Requirement: پشتیبانی RTL/LTR
کامپوننت Radio SHALL هم RTL و هم LTR را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** `dir="rtl"` باشد
- **آنگاه** کنترل SHALL در سمت راست (start) و Label در سمت چپ (end) قرار بگیرد

#### Scenario: چیدمان LTR
- **زمانی که** `dir="ltr"` باشد
- **آنگاه** کنترل SHALL در سمت چپ (start) و Label در سمت راست (end) قرار بگیرد

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Radio SHALL دسترسی‌پذیر باشد.

#### Scenario: استفاده از native radio input
- **زمانی که** Radio رندر شود
- **آنگاه** از `<input type="radio">` بومی HTML استفاده شود

#### Scenario: ناوبری با کیبورد
- **زمانی که** Radio غیرفعال نباشد
- **آنگاه** Radio SHALL با Tab قابل دسترسی و با Space قابل انتخاب باشد
- **و** در Radio Group، Arrow keys SHALL بین گزینه‌ها حرکت کند

#### Scenario: Focus Ring
- **زمانی که** Radio از طریق کیبورد فوکوس دریافت کند
- **آنگاه** focus ring SHALL قابل مشاهده باشد

#### Scenario: کنتراست رنگ
- **زمانی که** Radio رندر شود
- **آنگاه** کنترل دایره‌ای SHALL حداقل contrast ratio 3:1 با پس‌زمینه داشته باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Radio SHALL از design tokens موجود در tokens.json استفاده کند.

#### Scenario: CSS custom properties
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--radio-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: سازگاری با مرورگرها
کامپوننت Radio SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
