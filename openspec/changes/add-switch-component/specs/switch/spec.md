# مشخصات کامپوننت Switch

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Switch
کامپوننت Switch SHALL برای تغییر فوری بین دو حالت روشن/خاموش استفاده شود. سوئیچ به کاربران امکان می‌دهد بین دو گزینه منحصر به فرد متقابل یک گزینه را انتخاب کنند و فعال کردن سوئیچ باعث تغییر فوری می‌شود.

#### Scenario: تغییر فوری بین دو حالت
- **زمانی که** کاربر نیاز به فعال/غیرفعال کردن فوری یک تنظیم داشته باشد
- **آنگاه** از کامپوننت Switch استفاده شود

#### Scenario: جایگزین Switch
- **زمانی که** قبل از اعمال تغییر به یک مرحله ارسال نیاز باشد
- **آنگاه** از Checkbox استفاده شود
- **زمانی که** نیاز به مشخص کردن وضعیت نامشخص (indeterminate) باشد
- **آنگاه** از Checkbox استفاده شود

---

### Requirement: خصوصیت state (وضعیت تعاملی)
کامپوننت Switch SHALL پنج وضعیت تعاملی/سیستمی را پشتیبانی کند: Rest، Hover، Pressed، Focus و Disabled. State استایل Track، Thumb و در صورت وجود focus ring را تعیین می‌کند.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** Switch SHALL در حالت پیش‌فرض نمایش داده شود

#### Scenario: حالت Hover
- **زمانی که** نشانگر روی Switch قرار بگیرد و Switch غیرفعال نباشد
- **آنگاه** رنگ Track SHALL تغییر کند (Checked: #22967d، Unchecked: #f6f8fa)

#### Scenario: حالت Pressed
- **زمانی که** کاربر کلیک کند یا بفشارد و Switch غیرفعال نباشد
- **آنگاه** رنگ Track SHALL تغییر کند (Checked: #19705e، Unchecked: #dddfe1)
- **و** pressed SHALL فقط در زمان تعامل فعال باشد و بعد از رها شدن به rest یا focus برگردد

#### Scenario: حالت Focus
- **زمانی که** Switch فوکوس دریافت کند (keyboard یا click)
- **آنگاه** یک focus ring SHALL با border 1px solid #222323 و border-radius 4px روی wrapper نمایش داده شود
- **و** focus ring MUST NOT باعث تغییر اندازه layout شود
- **و** focus ring MUST NOT رنگ یا موقعیت Track و Thumb را override کند

#### Scenario: حالت Disabled
- **زمانی که** Switch غیرفعال باشد
- **آنگاه** Track SHALL با رنگ #f6f8fa و border #dddfe1 نمایش داده شود
- **و** Thumb SHALL با bg #e7e9eb و border #dddfe1 نمایش داده شود
- **و** آیکن SHALL با رنگ #bbbcbe نمایش داده شود
- **و** هیچ state تعاملی دیگری (hover، pressed، focus) MUST NOT فعال شود
- **و** تغییر مقدار checked توسط کاربر MUST NOT مجاز باشد

#### Scenario: اولویت stateها
- **زمانی که** چند state همزمان فعال باشند
- **آنگاه** اولویت SHALL به ترتیب زیر باشد: disabled > pressed > focus > hover > rest

---

### Requirement: خصوصیت checked (وضعیت روشن/خاموش)
کامپوننت Switch SHALL از وضعیت checked/unchecked پشتیبانی کند.

#### Scenario: حالت Checked (روشن)
- **زمانی که** Switch روشن باشد (checked=true)
- **آنگاه** Thumb SHALL در موقعیت روشن (on — سمت end) قرار بگیرد
- **و** Track SHALL با رنگ brand نمایش داده شود
- **و** آیکن checkmark SHALL داخل Thumb نمایش داده شود

#### Scenario: حالت Unchecked (خاموش)
- **زمانی که** Switch خاموش باشد (checked=false)
- **آنگاه** Thumb SHALL در موقعیت خاموش (off — سمت start) قرار بگیرد
- **و** Track SHALL با رنگ neutral نمایش داده شود
- **و** آیکن X SHALL داخل Thumb نمایش داده شود

#### Scenario: checked مستقل از state
- **زمانی که** Switch در هر state تعاملی باشد
- **آنگاه** وضعیت checked SHALL مستقل از stateهای تعاملی پایدار بماند

#### Scenario: Toggle با کلیک
- **زمانی که** کاربر روی هر نقطه از Switch کلیک کند و Switch غیرفعال نباشد
- **آنگاه** مقدار checked SHALL تغییر کند

---

### Requirement: رفتار فوکوس (Focus Behavior — Non-Exclusive)
فوکوس در کامپوننت Switch SHALL یک state تعاملی مستقل و غیر انحصاری باشد.

#### Scenario: ترکیب فوکوس با سایر stateها
- **زمانی که** Switch فوکوس داشته باشد
- **آنگاه** فوکوس SHALL همزمان با rest، hover و pressed فعال باشد
- **و** ترکیب‌های rest+focus، hover+focus و pressed+focus SHALL معتبر باشند

#### Scenario: فوکوس در حالت Disabled
- **زمانی که** Switch در حالت disabled باشد
- **آنگاه** فوکوس MUST NOT نمایش داده شود

#### Scenario: focus ring به عنوان لایه بصری
- **زمانی که** focus ring نمایش داده شود
- **آنگاه** focus ring SHALL فقط یک لایه بصری اضافه باشد
- **و** MUST NOT رنگ یا موقعیت Track و Thumb را override کند
- **و** MUST NOT باعث تغییر اندازه یا جابجایی layout شود

---

### Requirement: قوانین بصری Track
Track پس‌زمینه اصلی Switch SHALL با ساختار مشخص باشد.

#### Scenario: رنگ‌بندی Track در حالت Checked
- **زمانی که** Switch در حالت checked باشد
- **آنگاه** Track SHALL از رنگ‌های brand استفاده کند:
  - Rest: bg #26a88c، border #eaf8f5
  - Hover: bg #22967d، border #eaf8f5
  - Pressed: bg #19705e، border #eaf8f5
  - Disabled: bg #f6f8fa، border #dddfe1

#### Scenario: رنگ‌بندی Track در حالت Unchecked
- **زمانی که** Switch در حالت unchecked باشد
- **آنگاه** Track SHALL از رنگ‌های neutral استفاده کند:
  - Rest: bg #ffffff، border #e2e4e6
  - Hover: bg #f6f8fa، border #e2e4e6
  - Pressed: bg #dddfe1، border #e2e4e6
  - Disabled: bg #f6f8fa، border #dddfe1

#### Scenario: تفاوت on/off در Disabled
- **زمانی که** Switch در حالت disabled باشد
- **آنگاه** تفاوت بین on/off SHALL همچنان قابل تشخیص باشد

---

### Requirement: قوانین بصری Thumb
Thumb عنصر متحرک داخل Track SHALL با ساختار مشخص باشد.

#### Scenario: موقعیت Thumb
- **زمانی که** Switch رندر شود
- **آنگاه** موقعیت Thumb SHALL فقط به checked وابسته باشد
- **و** Checked: Thumb سمت end (چپ در RTL، راست در LTR)
- **و** Unchecked: Thumb سمت start (راست در RTL، چپ در LTR)

#### Scenario: رنگ‌بندی Thumb
- **زمانی که** Switch در حالت عادی باشد
- **آنگاه** Thumb SHALL با bg #ffffff نمایش داده شود
- **و** border Checked: #26a88c، border Unchecked: #e2e4e6
- **و** در حالت Disabled: bg #e7e9eb، border #dddfe1

#### Scenario: حرکت Thumb با Transition
- **زمانی که** مقدار checked تغییر کند
- **آنگاه** حرکت Thumb SHALL با transition نرم انجام شود

#### Scenario: آیکن داخل Thumb
- **زمانی که** Switch در حالت checked باشد
- **آنگاه** آیکن checkmark SHALL با رنگ brand (#26a88c) نمایش داده شود
- **زمانی که** Switch در حالت unchecked باشد
- **آنگاه** آیکن X SHALL با رنگ neutral (#59595a) نمایش داده شود
- **زمانی که** Switch در حالت disabled باشد
- **آنگاه** آیکن SHALL با رنگ #bbbcbe نمایش داده شود

---

### Requirement: قوانین چیدمان (Layout Rules)
کامپوننت Switch SHALL ساختار مستقل بدون Label داخلی داشته باشد.

#### Scenario: Switch مستقل
- **زمانی که** Switch رندر شود
- **آنگاه** Switch SHALL یک کامپوننت مستقل بدون Label داخلی باشد
- **و** در صورت نیاز به Label، از کامپوننت Label جداگانه کنار Switch استفاده شود

#### Scenario: اندازه ثابت
- **زمانی که** Switch رندر شود
- **آنگاه** Wrapper SHALL 56px × 36px با padding 8px باشد
- **و** Track SHALL با ارتفاع 20px و border-radius full (360px) باشد
- **و** Thumb SHALL 22px × 22px با border-radius full (360px) باشد
- **و** آیکن SHALL 14px × 14px باشد

---

### Requirement: پشتیبانی RTL/LTR
کامپوننت Switch SHALL هم RTL و هم LTR را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** `dir="rtl"` باشد
- **آنگاه** Thumb در حالت unchecked SHALL سمت راست (start) باشد
- **و** Thumb در حالت checked SHALL سمت چپ (end) باشد

#### Scenario: چیدمان LTR
- **زمانی که** `dir="ltr"` باشد
- **آنگاه** Thumb در حالت unchecked SHALL سمت چپ (start) باشد
- **و** Thumb در حالت checked SHALL سمت راست (end) باشد

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Switch SHALL دسترسی‌پذیر باشد.

#### Scenario: استفاده از native checkbox با role="switch"
- **زمانی که** Switch رندر شود
- **آنگاه** از `<input type="checkbox" role="switch">` بومی HTML استفاده شود

#### Scenario: ناوبری با کیبورد
- **زمانی که** Switch غیرفعال نباشد
- **آنگاه** Switch SHALL با Tab قابل دسترسی و با Space قابل toggle باشد

#### Scenario: Focus Ring
- **زمانی که** Switch از طریق کیبورد فوکوس دریافت کند
- **آنگاه** focus ring SHALL قابل مشاهده باشد

#### Scenario: حالت checked در accessibility
- **زمانی که** Switch رندر شود
- **آنگاه** حالت checked SHALL از طریق aria-checked یا معادل بومی آن قابل دسترسی باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Switch SHALL از design tokens موجود در tokens.json استفاده کند.

#### Scenario: CSS custom properties
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--switch-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: سازگاری با مرورگرها
کامپوننت Switch SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
