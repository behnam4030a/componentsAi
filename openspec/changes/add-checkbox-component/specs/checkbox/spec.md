# مشخصات کامپوننت Checkbox

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Checkbox
کامپوننت Checkbox SHALL به کاربران امکان انتخاب چندین گزینه از یک گروه یا روشن/خاموش کردن یک گزینه را بدهد. Checkbox نیاز به یک مرحله ارسال (submit) دارد و تغییر فوری ایجاد نمی‌کند.

#### Scenario: انتخاب چندگانه از گروه
- **زمانی که** کاربر نیاز به انتخاب چند گزینه از یک مجموعه دارد
- **آنگاه** از کامپوننت Checkbox برای هر گزینه استفاده شود

#### Scenario: روشن/خاموش کردن یک گزینه
- **زمانی که** کاربر نیاز به فعال یا غیرفعال کردن یک تنظیم دارد و نتیجه فوری مورد نظر نیست
- **آنگاه** از Checkbox استفاده شود

#### Scenario: عدم استفاده به جای Radio Button
- **زمانی که** کاربر باید فقط یک گزینه از میان چند گزینه انتخاب کند
- **آنگاه** از Radio Button یا Dropdown به جای Checkbox استفاده شود

#### Scenario: عدم استفاده به جای Switch
- **زمانی که** نیاز به تغییر با اثر فوری باشد (بدون مرحله ارسال)
- **آنگاه** از Switch به جای Checkbox استفاده شود

---

### Requirement: وضعیت منطقی انتخاب (Status)
کامپوننت Checkbox SHALL سه وضعیت منطقی را پشتیبانی کند: Unchecked، Checked و Indeterminate. Status مستقیماً به مقدار داده (value) متصل است.

#### Scenario: وضعیت Unchecked
- **زمانی که** Checkbox انتخاب نشده باشد
- **آنگاه** باکس SHALL خالی با border نمایش داده شود (بدون پس‌زمینه رنگی، بدون آیکون)

#### Scenario: وضعیت Checked
- **زمانی که** Checkbox به‌طور کامل انتخاب شده باشد
- **آنگاه** باکس SHALL با پس‌زمینه رنگ brand و آیکون checkmark (تیک) سفید نمایش داده شود

#### Scenario: وضعیت Indeterminate
- **زمانی که** در سناریوی Select All، برخی آیتم‌های زیرمجموعه انتخاب شده باشند اما نه همه
- **آنگاه** باکس SHALL با پس‌زمینه رنگ brand و آیکون minus (خط) سفید نمایش داده شود

#### Scenario: Indeterminate یک حالت بصری است
- **زمانی که** Checkbox در وضعیت Indeterminate باشد
- **آنگاه** این وضعیت SHALL به عنوان یک حالت بصری در نظر گرفته شود و به‌تنهایی مقدار نهایی داده نباشد (neither true nor false)

#### Scenario: مدیریت جداگانه Indeterminate
- **زمانی که** وضعیت Checkbox مدیریت شود
- **آنگاه** Indeterminate SHALL جدا از Checked و Unchecked مدیریت شود (با JavaScript property `indeterminate`)

---

### Requirement: حالت‌های تعاملی (State)
کامپوننت Checkbox SHALL پنج حالت تعاملی را پشتیبانی کند: Rest، Hover، Pressed، Focused و Disabled. State بر ظاهر کامپوننت تأثیر می‌گذارد، نه بر مقدار داده.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی از سوی کاربر رخ ندهد
- **آنگاه** Checkbox SHALL در حالت پیش‌فرض با رنگ‌های rest نمایش داده شود

#### Scenario: حالت Hover
- **زمانی که** نشانگر ماوس روی Checkbox قرار بگیرد (Mouse Enter)
- **آنگاه** Checkbox SHALL رنگ‌های حالت hover را نمایش دهد
- Unchecked: border تیره‌تر (`#59595a`)
- Checked/Indeterminate: background تیره‌تر (`#22967d`)

#### Scenario: حالت Pressed
- **زمانی که** کاربر دکمه ماوس را نگه داشته باشد (Mouse Down)
- **آنگاه** Checkbox SHALL رنگ‌های حالت pressed را نمایش دهد
- Unchecked: border تیره‌تر (`#4f4f50`)
- Checked/Indeterminate: background تیره‌تر (`#19705e`)

#### Scenario: حالت Focused
- **زمانی که** Checkbox از طریق کیبورد (Tab) یا ابزارهای دسترس‌پذیری در فوکوس قرار بگیرد
- **آنگاه** Checkbox SHALL حلقه فوکوس خارجی (1px solid `#222323` با border-radius 4px) نمایش دهد
- **و** این حلقه SHALL در هر سه وضعیت Status (Unchecked، Checked، Indeterminate) نمایش داده شود

#### Scenario: حالت Disabled
- **زمانی که** Checkbox غیرفعال باشد
- **آنگاه** Checkbox SHALL بصری کمرنگ باشد:
- Unchecked: border `#dddfe1`
- Checked/Indeterminate: بدون background، border `#dddfe1`، آیکون `#bbbcbe`
- **و** هیچ‌یک از Hover، Pressed و Focused نباید فعال شوند
- **و** امکان تغییر Status وجود نداشته باشد

#### Scenario: Disabled غالب بر تمام حالت‌ها
- **زمانی که** Checkbox در حالت Disabled باشد و کاربر hover یا click کند
- **آنگاه** هیچ تغییر بصری SHALL رخ ندهد و Status تغییر نکند

---

### Requirement: سایزهای مختلف (Size Variants)
کامپوننت Checkbox SHALL دو سایز را پشتیبانی کند: Large و Medium. Size فقط بر ابعاد بصری تأثیر دارد و تأثیری بر رفتار ندارد.

#### Scenario: استفاده از CSS classes برای Size
- **زمانی که** توسعه‌دهنده سایز Checkbox را مشخص کند
- **آنگاه** از CSS class مربوطه استفاده شود: `checkbox--large`، `checkbox--medium`

#### Scenario: سایز Large
- **زمانی که** class `checkbox--large` اعمال شود
- **آنگاه** Checkbox SHALL boxholder=28px، box padding=6px، fontSize label=14px و icon=10px داشته باشد

#### Scenario: سایز Medium
- **زمانی که** class `checkbox--medium` اعمال شود
- **آنگاه** Checkbox SHALL boxholder=24px، box padding=4px، fontSize label=12px و icon=10px داشته باشد

#### Scenario: Size فقط بر ابعاد تأثیر دارد
- **زمانی که** Size تغییر کند
- **آنگاه** رفتار State و Status SHALL بدون تغییر باقی بماند

---

### Requirement: برچسب توضیحی (Label)
کامپوننت Checkbox SHALL از یک Label اختیاری پشتیبانی کند که در کنار باکس نمایش داده شود.

#### Scenario: نمایش Label
- **زمانی که** Label ارائه شده باشد
- **آنگاه** متن Label SHALL در کنار باکس Checkbox نمایش داده شود با فاصله 8px (paddingStart)

#### Scenario: کلیک روی Label تغییر Status
- **زمانی که** کاربر روی Label کلیک کند
- **آنگاه** Status Checkbox SHALL تغییر کند (مانند کلیک مستقیم روی باکس)

#### Scenario: Checkbox بدون Label
- **زمانی که** Label ارائه نشده باشد
- **آنگاه** Checkbox SHALL فقط با باکس بدون متن رندر شود و `aria-label` برای دسترسی‌پذیری الزامی باشد

#### Scenario: اندازه فونت Label مطابق Size
- **زمانی که** Size برابر Large باشد
- **آنگاه** فونت Label SHALL 14px باشد
- **زمانی که** Size برابر Medium باشد
- **آنگاه** فونت Label SHALL 12px باشد

#### Scenario: Label فقط نقش توضیحی دارد
- **زمانی که** Label وجود داشته باشد
- **آنگاه** Label SHALL صرفاً نقش توضیحی داشته باشد و مقدار داده‌ای مستقلی ایجاد نکند

---

### Requirement: پشتیبانی از متن راست‌به‌چپ (RTL)
کامپوننت Checkbox SHALL متن راست‌به‌چپ (RTL) را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** المان والد یا خود Checkbox `dir="rtl"` داشته باشد
- **آنگاه** Label SHALL در سمت راست (start) و Box در سمت چپ (end) قرار بگیرد — مطابق طراحی Figma

#### Scenario: چیدمان LTR
- **زمانی که** المان والد `dir="ltr"` داشته باشد
- **آنگاه** Box SHALL در سمت چپ (start) و Label در سمت راست (end) قرار بگیرد

---

### Requirement: مدیریت فوکوس
کامپوننت Checkbox SHALL نشانگر فوکوس قابل مشاهده برای ناوبری کیبورد ارائه دهد. فوکوس SHALL مستقل از Status و State باشد.

#### Scenario: حلقه فوکوس در ناوبری کیبورد
- **زمانی که** Checkbox از طریق کیبورد (Tab) فوکوس بگیرد
- **آنگاه** Checkbox SHALL حلقه فوکوس (1px solid `#222323`، border-radius 4px) نمایش دهد

#### Scenario: عدم نمایش حلقه فوکوس با کلیک موس
- **زمانی که** Checkbox از طریق کلیک موس فوکوس بگیرد
- **آنگاه** حلقه فوکوس نSHALL نمایش داده شود (`:focus-visible`)

#### Scenario: فوکوس مستقل از Status
- **زمانی که** Checkbox در هر وضعیت Status (Unchecked، Checked، Indeterminate) فوکوس بگیرد
- **آنگاه** حلقه فوکوس SHALL یکسان نمایش داده شود

#### Scenario: فوکوس بدون layout shift
- **زمانی که** حلقه فوکوس نمایش داده شود
- **آنگاه** حلقه SHALL خارج از مرز کامپوننت رندر شود تا جابجایی چیدمان ایجاد نکند

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Checkbox SHALL دسترسی‌پذیر باشد و با استانداردهای WCAG 2.1 سطح AA مطابقت داشته باشد.

#### Scenario: استفاده از native checkbox
- **زمانی که** Checkbox رندر شود
- **آنگاه** از `<input type="checkbox">` بومی HTML استفاده شود تا screen readers آن را به درستی شناسایی کنند

#### Scenario: حالت Indeterminate با ARIA
- **زمانی که** Checkbox در وضعیت Indeterminate باشد
- **آنگاه** `aria-checked="mixed"` SHALL روی input تنظیم شود

#### Scenario: برچسب دسترسی‌پذیر
- **زمانی که** Label متنی ارائه شده باشد
- **آنگاه** Checkbox SHALL نام دسترسی‌پذیر از طریق `<label>` wrapper داشته باشد
- **زمانی که** Label وجود نداشته باشد
- **آنگاه** `aria-label` SHALL ارائه شود

#### Scenario: قابلیت ناوبری با کیبورد
- **زمانی که** Checkbox غیرفعال نباشد
- **آنگاه** Checkbox SHALL با Space قابل toggle و با Tab قابل ناوبری باشد

#### Scenario: کنتراست رنگ
- **زمانی که** Checkbox در هر ترکیب Status/State رندر شود
- **آنگاه** متن Label و آیکون‌ها SHALL حداقل contrast ratio 4.5:1 با پس‌زمینه داشته باشند

---

### Requirement: یکپارچگی با Design Token
کامپوننت Checkbox SHALL از design tokens موجود در tokens.json به عنوان منبع واحد حقیقت استفاده کند.

#### Scenario: ویژگی‌های سفارشی CSS
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--checkbox-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: عملکرد
کامپوننت Checkbox SHALL سبک و با عملکرد خوب باشد.

#### Scenario: اندازه CSS
- **زمانی که** کامپوننت bundle شود
- **آنگاه** اندازه CSS SHALL کمتر از 5KB فشرده‌نشده باشد

---

### Requirement: سازگاری با مرورگرها
کامپوننت Checkbox SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
