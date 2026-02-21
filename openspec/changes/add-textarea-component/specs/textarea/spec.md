# مشخصات کامپوننت Textarea

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Textarea
کامپوننت Textarea SHALL برای دریافت متن چندخطی و آزاد از کاربر استفاده شود. ظاهر و رفتار آن با state و size کنترل می‌شود و در صورت نیاز می‌تواند امکان تغییر اندازه (resize) داشته باشد. تغییرات استایل در هر state SHALL همزمان روی کانتینر Textarea، متن واردشده و placeholder اعمال شود.

#### Scenario: دریافت متن چندخطی از کاربر
- **زمانی که** کاربر نیاز به وارد کردن چندین خط متن آزاد (نظر، توضیحات، پیام و ...) دارد
- **آنگاه** از کامپوننت Textarea استفاده شود

#### Scenario: عدم استفاده برای متن تک‌خطی
- **زمانی که** فقط به دریافت یک خط اطلاعات نیاز باشد
- **آنگاه** از کامپوننت Input به جای Textarea استفاده شود

---

### Requirement: وضعیت‌های تعاملی/سیستمی (State)
کامپوننت Textarea SHALL شش وضعیت تعاملی/سیستمی را پشتیبانی کند: Rest، Hover، Focused، Error، Disabled و ReadOnly. State مستقیماً استایل‌های مرزی، پس‌زمینه، رنگ متن و رنگ placeholder را تعیین می‌کند. تغییرات استایل در هر state SHALL همزمان روی container، متن واردشده و placeholder اعمال شود.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** Textarea SHALL با border #e2e4e6، background #ffffff، متن #222323 و placeholder #59595a نمایش داده شود
- **و** Accessible Indicator SHALL مخفی باشد (opacity: 0)

#### Scenario: حالت Hover
- **زمانی که** نشانگر ماوس روی Textarea قرار بگیرد و Textarea قابل تعامل باشد (نه disabled)
- **آنگاه** Textarea SHALL با border #d8dadc نمایش داده شود
- **و** Accessible Indicator SHALL قابل مشاهده با رنگ #59595a باشد

#### Scenario: حالت Focused
- **زمانی که** Textarea فوکوس دریافت کند (keyboard یا click) و cursor داخل فیلد باشد
- **آنگاه** Textarea SHALL با border #e2e4e6، background #ffffff و shadow focused (0px 2px 3px 1px rgba(42,187,156,0.2)) نمایش داده شود
- **و** Accessible Indicator SHALL قابل مشاهده با رنگ #2abb9c باشد

#### Scenario: حالت Error
- **زمانی که** ورودی نامعتبر باشد یا خطا داشته باشد
- **آنگاه** Textarea SHALL با outer border #c50f1f، inner border #e2e4e6، background #fdf3f4 نمایش داده شود
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: حالت Disabled
- **زمانی که** Textarea غیرفعال باشد
- **آنگاه** Textarea SHALL با border #dddfe1، متن و placeholder #bbbcbe نمایش داده شود
- **و** هیچ state تعاملی دیگری (hover/focused) نSHALL فعال شود
- **و** تایپ و تغییر مقدار نSHALL امکان‌پذیر باشد
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: حالت ReadOnly
- **زمانی که** Textarea فقط‌خواندنی باشد
- **آنگاه** Textarea SHALL بدون border، با background #f6f8fa نمایش داده شود
- **و** امکان focus و انتخاب متن SHALL مجاز باشد
- **و** تغییر مقدار توسط کاربر نSHALL مجاز باشد
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: اولویت stateها در صورت همپوشانی
- **زمانی که** چند state همزمان فعال باشند
- **آنگاه** اولویت SHALL به ترتیب زیر باشد: disabled > error > focused > hover > rest

#### Scenario: Error + Focused ترکیبی
- **زمانی که** Textarea در حالت Error باشد و همزمان فوکوس داشته باشد
- **آنگاه** استایل ترکیبی "error + focused" SHALL اعمال شود (اگر تعریف شده)
- **و** در غیر این صورت error SHALL اولویت داشته باشد و فوکوس حداقلی باقی بماند

---

### Requirement: سایزهای مختلف (Size Variants)
کامپوننت Textarea SHALL سه سایز را پشتیبانی کند: Large، Medium و Small. Size SHALL روی min-height (یا ارتفاع پیش‌فرض)، padding داخلی، font-size و line-height متن واردشده، و font-size و line-height placeholder تأثیر بگذارد.

#### Scenario: استفاده از CSS classes برای Size
- **زمانی که** توسعه‌دهنده سایز Textarea را مشخص کند
- **آنگاه** از CSS class مربوطه استفاده شود: `textarea--large`، `textarea--medium`، `textarea--small`

#### Scenario: سایز Large
- **زمانی که** class `textarea--large` اعمال شود
- **آنگاه** Textarea SHALL min-height=72px، paddingX=16px، paddingY=8px، fontSize=14px و lineHeight=2 داشته باشد

#### Scenario: سایز Medium
- **زمانی که** class `textarea--medium` اعمال شود
- **آنگاه** Textarea SHALL min-height=64px، paddingX=12px، paddingY=8px، fontSize=14px و lineHeight=2 داشته باشد

#### Scenario: سایز Small
- **زمانی که** class `textarea--small` اعمال شود
- **آنگاه** Textarea SHALL min-height=36px، paddingX=8px، paddingY=8px، fontSize=12px و lineHeight=1.5 داشته باشد

#### Scenario: همه stateها در همه sizeها
- **زمانی که** هر state با هر size ترکیب شود
- **آنگاه** Textarea SHALL بدون تداخل به درستی رندر شود

#### Scenario: Size فقط بر ابعاد تأثیر دارد
- **زمانی که** Size تغییر کند
- **آنگاه** رفتار State SHALL بدون تغییر باقی بماند

---

### Requirement: قابلیت تغییر اندازه (Resize Handler)
کامپوننت Textarea SHALL از قابلیت اختیاری تغییر اندازه توسط کاربر پشتیبانی کند.

#### Scenario: Resize فعال (resizeHandler = true)
- **زمانی که** resizeHandler فعال باشد
- **آنگاه** امکان resize برای کاربر SHALL فعال باشد (طبق رفتار تعریف‌شده در سیستم طراحی، فقط عمودی)
- **و** هندل resize SHALL قابل مشاهده باشد

#### Scenario: Resize غیرفعال (resizeHandler = false)
- **زمانی که** resizeHandler غیرفعال باشد
- **آنگاه** resize برای کاربر SHALL غیرفعال باشد
- **و** اندازه SHALL توسط layout کنترل شود

#### Scenario: Resize در حالت Disabled
- **زمانی که** Textarea در حالت Disabled باشد
- **آنگاه** resize نSHALL قابل استفاده باشد حتی اگر resizeHandler = true باشد

#### Scenario: Resize تأثیری بر استایل State ندارد
- **زمانی که** resizeHandler فعال یا غیرفعال باشد
- **آنگاه** فعال/غیرفعال بودن resize نSHALL استایل stateها (رنگ‌ها/بوردر) را تغییر دهد

---

### Requirement: قوانین چیدمان و ساختار داخلی (Layout Rules)
کامپوننت Textarea SHALL ساختار داخلی مناسب برای نمایش متن چندخطی داشته باشد.

#### Scenario: فیلد چندخطی
- **زمانی که** Textarea رندر شود
- **آنگاه** Textarea SHALL یک فیلد چندخطی باشد و امکان نمایش چند خط متن را داشته باشد

#### Scenario: padding و typography هماهنگ با size
- **زمانی که** size تغییر کند
- **آنگاه** padding و typography SHALL با size هماهنگ باشد

#### Scenario: پشتیبانی از RTL/LTR
- **زمانی که** Textarea رندر شود
- **آنگاه** جهت نوشتار (RTL/LTR) SHALL رعایت شود

#### Scenario: ساختار داخلی
- **زمانی که** Textarea رندر شود
- **آنگاه** ساختار داخلی SHALL به صورت [textarea field] [resize handler] باشد
- **و** resize handler SHALL در گوشه پایین-چپ (در RTL) قرار داشته باشد

---

### Requirement: Accessible Indicator (خط پایینی)
کامپوننت Textarea SHALL یک خط پایینی (1.5px) داشته باشد که بر اساس state تغییر وضعیت دهد.

#### Scenario: Indicator در حالت Rest
- **زمانی که** Textarea در حالت Rest باشد
- **آنگاه** Indicator SHALL مخفی باشد (opacity: 0)

#### Scenario: Indicator در حالت Hover
- **زمانی که** Textarea در حالت Hover باشد
- **آنگاه** Indicator SHALL قابل مشاهده با رنگ #59595a باشد

#### Scenario: Indicator در حالت Focused
- **زمانی که** Textarea در حالت Focused باشد
- **آنگاه** Indicator SHALL قابل مشاهده با رنگ #2abb9c باشد

#### Scenario: Indicator در حالت Error/Disabled/ReadOnly
- **زمانی که** Textarea در حالت Error، Disabled یا ReadOnly باشد
- **آنگاه** Indicator SHALL مخفی باشد

---

### Requirement: متن واردشده و Placeholder (Typography)
کامپوننت Textarea SHALL استایل متن واردشده و placeholder را بر اساس state و size تعیین کند. قوانین Typography و Placeholder مشابه کامپوننت Input هستند.

#### Scenario: استایل متن واردشده در حالت عادی
- **زمانی که** Textarea در حالت Rest، Hover یا Focused باشد
- **آنگاه** متن واردشده SHALL با رنگ #222323 نمایش داده شود

#### Scenario: استایل placeholder در حالت عادی
- **زمانی که** Textarea خالی باشد و در حالت Rest، Hover یا Focused باشد
- **آنگاه** placeholder SHALL با رنگ #59595a نمایش داده شود

#### Scenario: استایل در حالت Disabled
- **زمانی که** Textarea در حالت Disabled باشد
- **آنگاه** متن واردشده و placeholder هر دو SHALL با رنگ #bbbcbe نمایش داده شوند

#### Scenario: استایل در حالت ReadOnly
- **زمانی که** Textarea در حالت ReadOnly باشد
- **آنگاه** رنگ/شدت متن SHALL مطابق توکن‌های همان state تغییر کند

#### Scenario: متن با مقدار موجود
- **زمانی که** Textarea مقدار داشته باشد
- **آنگاه** placeholder نSHALL نمایش داده شود (رفتار بومی مرورگر)
- **و** قوانین رنگ state SHALL برای متن ورودی برقرار باشد

#### Scenario: تغییر همزمان state روی تمام عناصر
- **زمانی که** state تغییر کند
- **آنگاه** تغییر SHALL همزمان روی container، متن واردشده و placeholder اعمال شود (مثلا هنگام رفتن از rest به focused یا error)

#### Scenario: تایپوگرافی مطابق Size
- **زمانی که** Size برابر Large یا Medium باشد
- **آنگاه** font-size SHALL 14px و line-height SHALL 2 باشد
- **زمانی که** Size برابر Small باشد
- **آنگاه** font-size SHALL 12px و line-height SHALL 1.5 باشد

#### Scenario: فونت
- **زمانی که** Textarea رندر شود
- **آنگاه** فونت SHALL Peyda(FaNum) با وزن 400 باشد

---

### Requirement: پشتیبانی از متن راست‌به‌چپ (RTL)
کامپوننت Textarea SHALL متن راست‌به‌چپ (RTL) را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** المان والد یا خود Textarea `dir="rtl"` داشته باشد
- **آنگاه** Textarea SHALL چیدمان RTL داشته باشد:
- متن از سمت راست شروع شود
- resize handler در گوشه پایین-چپ باشد

#### Scenario: چیدمان LTR
- **زمانی که** المان والد `dir="ltr"` داشته باشد
- **آنگاه** Textarea SHALL چیدمان LTR داشته باشد:
- متن از سمت چپ شروع شود
- resize handler در گوشه پایین-راست باشد

---

### Requirement: رفتار تعاملی (Behavior)
کامپوننت Textarea SHALL رفتارهای تعاملی مشخص داشته باشد.

#### Scenario: فعال‌سازی Focused
- **زمانی که** Textarea فوکوس دریافت کند (keyboard یا click)
- **آنگاه** حالت Focused SHALL فعال شود

#### Scenario: Hover فقط در حالت قابل تعامل
- **زمانی که** نشانگر ماوس روی Textarea قرار بگیرد
- **آنگاه** حالت Hover SHALL فقط اگر Textarea غیرفعال نباشد فعال شود

#### Scenario: Error یک state منطقی
- **زمانی که** اعتبارسنجی یا منطق فرم خطا تشخیص دهد
- **آنگاه** حالت Error SHALL فعال شود و نSHALL وابسته به hover یا focus باشد

#### Scenario: ReadOnly اجازه focus
- **زمانی که** Textarea در حالت ReadOnly باشد
- **آنگاه** امکان focus و انتخاب متن SHALL مجاز باشد اما تغییر مقدار نSHALL مجاز باشد

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Textarea SHALL دسترسی‌پذیر باشد و با استانداردهای WCAG 2.1 سطح AA مطابقت داشته باشد.

#### Scenario: استفاده از native textarea
- **زمانی که** Textarea رندر شود
- **آنگاه** از `<textarea>` بومی HTML استفاده شود تا screen readers آن را به درستی شناسایی کنند

#### Scenario: حالت Error با ARIA
- **زمانی که** Textarea در حالت Error باشد
- **آنگاه** `aria-invalid="true"` SHALL روی textarea تنظیم شود

#### Scenario: برچسب دسترسی‌پذیر
- **زمانی که** Textarea بدون label خارجی باشد
- **آنگاه** `aria-label` SHALL ارائه شود

#### Scenario: قابلیت ناوبری با کیبورد
- **زمانی که** Textarea غیرفعال نباشد
- **آنگاه** Textarea SHALL با Tab قابل دسترسی و با تایپ قابل استفاده باشد

#### Scenario: کنتراست رنگ
- **زمانی که** Textarea در هر ترکیب state/size رندر شود
- **آنگاه** متن SHALL حداقل contrast ratio 4.5:1 و placeholder حداقل 3:1 با پس‌زمینه داشته باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Textarea SHALL از design tokens موجود در tokens.json به عنوان منبع واحد حقیقت استفاده کند.

#### Scenario: ویژگی‌های سفارشی CSS
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--textarea-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: عملکرد
کامپوننت Textarea SHALL سبک و با عملکرد خوب باشد.

#### Scenario: اندازه CSS
- **زمانی که** کامپوننت bundle شود
- **آنگاه** اندازه CSS SHALL کمتر از 6KB فشرده‌نشده باشد

---

### Requirement: سازگاری با مرورگرها
کامپوننت Textarea SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
