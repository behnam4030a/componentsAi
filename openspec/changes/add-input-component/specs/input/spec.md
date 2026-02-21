# مشخصات کامپوننت Input

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Input
کامپوننت Input SHALL برای دریافت داده‌های متنی کوتاه و آزاد از کاربر استفاده شود. ظاهر و رفتار آن با state و size کنترل می‌شود.

#### Scenario: دریافت متن کوتاه از کاربر
- **زمانی که** کاربر نیاز به وارد کردن متن کوتاه (نام، ایمیل، جستجو و ...) دارد
- **آنگاه** از کامپوننت Input استفاده شود

#### Scenario: عدم استفاده برای متن چندخطی
- **زمانی که** نیاز به جمع‌آوری بیش از یک خط اطلاعات باشد
- **آنگاه** از کامپوننت Textarea به جای Input استفاده شود

---

### Requirement: وضعیت‌های تعاملی/سیستمی (State)
کامپوننت Input SHALL شش وضعیت تعاملی/سیستمی را پشتیبانی کند: Rest، Hover، Focused، Error، Disabled و ReadOnly. State مستقیماً استایل‌های مرزی، پس‌زمینه، رنگ متن، رنگ placeholder و رنگ آیکن‌ها را تعیین می‌کند. تغییرات استایل در هر state SHALL همزمان روی container، متن واردشده، placeholder و آیکن‌ها اعمال شود.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** Input SHALL با border #e2e4e6، background #ffffff، متن #222323 و placeholder #59595a نمایش داده شود
- **و** Accessible Indicator SHALL مخفی باشد (opacity: 0)

#### Scenario: حالت Hover
- **زمانی که** نشانگر ماوس روی Input قرار بگیرد و Input قابل تعامل باشد (نه disabled)
- **آنگاه** Input SHALL با border #d8dadc، cursor pointer نمایش داده شود
- **و** Accessible Indicator SHALL قابل مشاهده با رنگ #c0c1c3 باشد

#### Scenario: حالت Focused
- **زمانی که** Input فوکوس دریافت کند (keyboard یا click) و cursor داخل فیلد باشد
- **آنگاه** Input SHALL با border #f6f8fa، background #ffffff و shadow focused (0px 2px 3px 1px rgba(42,187,156,0.2)) نمایش داده شود
- **و** Accessible Indicator SHALL قابل مشاهده با رنگ #2abb9c باشد

#### Scenario: حالت Error
- **زمانی که** ورودی نامعتبر باشد یا خطا داشته باشد
- **آنگاه** Input SHALL با border #c50f1f، background #fdf3f4 و shadow error (0px 0px 3px 1px rgba(197,15,31,0.2)) نمایش داده شود
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: حالت Disabled
- **زمانی که** Input غیرفعال باشد
- **آنگاه** Input SHALL با border #dddfe1، متن/placeholder/آیکن‌ها #bbbcbe نمایش داده شود
- **و** هیچ state تعاملی دیگری (hover/focused) نSHALL فعال شود
- **و** کلیک و تایپ نSHALL امکان‌پذیر باشد
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: حالت ReadOnly
- **زمانی که** Input فقط‌خواندنی باشد
- **آنگاه** Input SHALL بدون border، با background #f6f8fa نمایش داده شود
- **و** امکان focus و انتخاب متن SHALL مجاز باشد
- **و** تغییر مقدار توسط کاربر نSHALL مجاز باشد
- **و** Accessible Indicator SHALL مخفی باشد

#### Scenario: اولویت stateها در صورت همپوشانی
- **زمانی که** چند state همزمان فعال باشند
- **آنگاه** اولویت SHALL به ترتیب زیر باشد: disabled > error > focused > hover > rest

#### Scenario: Error + Focused ترکیبی
- **زمانی که** Input در حالت Error باشد و همزمان فوکوس داشته باشد
- **آنگاه** استایل error SHALL اولویت داشته باشد

---

### Requirement: سایزهای مختلف (Size Variants)
کامپوننت Input SHALL سه سایز را پشتیبانی کند: Large، Medium و Small. Size SHALL روی ارتفاع، padding افقی، font-size، line-height، فاصله (gap) بین آیکن و متن، اندازه آیکن‌ها و ارتفاع divider تأثیر بگذارد.

#### Scenario: استفاده از CSS classes برای Size
- **زمانی که** توسعه‌دهنده سایز Input را مشخص کند
- **آنگاه** از CSS class مربوطه استفاده شود: `input--large`، `input--medium`، `input--small`

#### Scenario: سایز Large
- **زمانی که** class `input--large` اعمال شود
- **آنگاه** Input SHALL height=45px، paddingX=16px، fontSize=14px، lineHeight=2، icon before=20px، icon after=16px و divider=16px داشته باشد

#### Scenario: سایز Medium
- **زمانی که** class `input--medium` اعمال شود
- **آنگاه** Input SHALL height=37px، paddingX=12px، fontSize=14px، lineHeight=2، icon before=20px، icon after=16px و divider=12px داشته باشد

#### Scenario: سایز Small
- **زمانی که** class `input--small` اعمال شود
- **آنگاه** Input SHALL height=24px، paddingX=8px، fontSize=12px، lineHeight=1.5، icon before=16px، icon after=16px و divider=8px داشته باشد

#### Scenario: همه stateها در همه sizeها
- **زمانی که** هر state با هر size ترکیب شود
- **آنگاه** Input SHALL بدون تداخل به درستی رندر شود

#### Scenario: Size فقط بر ابعاد تأثیر دارد
- **زمانی که** Size تغییر کند
- **آنگاه** رفتار State SHALL بدون تغییر باقی بماند

---

### Requirement: آیکن قبل از متن (beforeTextIcon)
کامپوننت Input SHALL از نمایش اختیاری یک آیکن قبل از متن پشتیبانی کند. آیکن باید با Icon Component رندر شود.

#### Scenario: نمایش آیکن before
- **زمانی که** `beforeTextIcon` فعال باشد
- **آنگاه** یک آیکن SHALL در سمت قبل از متن (start) داخل Input نمایش داده شود
- **و** یک divider عمودی SHALL بین آیکن و فیلد متن نمایش داده شود

#### Scenario: موقعیت آیکن before در RTL
- **زمانی که** direction برابر RTL باشد
- **آنگاه** آیکن before SHALL در سمت راست Input نمایش داده شود

#### Scenario: موقعیت آیکن before در LTR
- **زمانی که** direction برابر LTR باشد
- **آنگاه** آیکن before SHALL در سمت چپ Input نمایش داده شود

#### Scenario: اندازه آیکن before مطابق Size
- **زمانی که** Size برابر Large یا Medium باشد
- **آنگاه** آیکن before SHALL 20px باشد
- **زمانی که** Size برابر Small باشد
- **آنگاه** آیکن before SHALL 16px باشد

#### Scenario: رنگ آیکن before مطابق State
- **زمانی که** State تغییر کند
- **آنگاه** رنگ آیکن before SHALL از قوانین رنگ state تبعیت کند (مشابه رنگ placeholder)

---

### Requirement: آیکن بعد از متن (afterTextIcon)
کامپوننت Input SHALL از نمایش اختیاری یک آیکن بعد از متن پشتیبانی کند. آیکن باید با Icon Component رندر شود.

#### Scenario: نمایش آیکن after
- **زمانی که** `afterTextIcon` فعال باشد
- **آنگاه** یک آیکن SHALL در سمت بعد از متن (end) داخل Input نمایش داده شود

#### Scenario: موقعیت آیکن after در RTL
- **زمانی که** direction برابر RTL باشد
- **آنگاه** آیکن after SHALL در سمت چپ Input نمایش داده شود

#### Scenario: موقعیت آیکن after در LTR
- **زمانی که** direction برابر LTR باشد
- **آنگاه** آیکن after SHALL در سمت راست Input نمایش داده شود

#### Scenario: اندازه آیکن after
- **زمانی که** آیکن after نمایش داده شود
- **آنگاه** اندازه آن SHALL 16px باشد (ثابت در همه sizeها)

#### Scenario: رنگ آیکن after مطابق State
- **زمانی که** State تغییر کند
- **آنگاه** رنگ آیکن after SHALL از قوانین رنگ state تبعیت کند (مشابه رنگ placeholder)

---

### Requirement: قوانین چیدمان و ساختار داخلی (Layout Rules)
کامپوننت Input SHALL ساختار داخلی منظم با تراز عمودی مرکزی داشته باشد.

#### Scenario: ساختار داخلی
- **زمانی که** Input رندر شود
- **آنگاه** ساختار داخلی SHALL به صورت [beforeIcon] [divider] [text input area] [afterIcon] باشد

#### Scenario: تراز عمودی
- **زمانی که** آیکن‌ها و متن رندر شوند
- **آنگاه** تمام عناصر SHALL در مرکز عمودی تراز باشند

#### Scenario: padding و gap وابسته به size
- **زمانی که** size تغییر کند
- **آنگاه** padding افقی و gap بین عناصر SHALL متناسب با size تغییر کند

#### Scenario: وجود مستقل آیکن‌ها
- **زمانی که** آیکن‌ها مشخص شوند
- **آنگاه** هیچکدام، یکی، یا هر دو آیکن SHALL بتوانند مستقلاً وجود داشته باشند

#### Scenario: Divider فقط با beforeTextIcon
- **زمانی که** beforeTextIcon وجود داشته باشد
- **آنگاه** یک divider عمودی SHALL بین آیکن before و فیلد متن نمایش داده شود
- **و** ارتفاع divider SHALL مطابق size باشد: Large=16px، Medium=12px، Small=8px

#### Scenario: Divider بدون beforeTextIcon
- **زمانی که** beforeTextIcon وجود نداشته باشد
- **آنگاه** divider SHALL نمایش داده نشود

---

### Requirement: Accessible Indicator (خط پایینی)
کامپوننت Input SHALL یک خط پایینی (1.5px) داشته باشد که بر اساس state تغییر وضعیت دهد.

#### Scenario: Indicator در حالت Rest
- **زمانی که** Input در حالت Rest باشد
- **آنگاه** Indicator SHALL مخفی باشد (opacity: 0)

#### Scenario: Indicator در حالت Hover
- **زمانی که** Input در حالت Hover باشد
- **آنگاه** Indicator SHALL قابل مشاهده با رنگ #c0c1c3 باشد

#### Scenario: Indicator در حالت Focused
- **زمانی که** Input در حالت Focused باشد
- **آنگاه** Indicator SHALL قابل مشاهده با رنگ #2abb9c باشد

#### Scenario: Indicator در حالت Error/Disabled/ReadOnly
- **زمانی که** Input در حالت Error، Disabled یا ReadOnly باشد
- **آنگاه** Indicator SHALL مخفی باشد

---

### Requirement: متن واردشده و Placeholder (Typography)
کامپوننت Input SHALL استایل متن واردشده و placeholder را بر اساس state و size تعیین کند.

#### Scenario: استایل متن واردشده در حالت عادی
- **زمانی که** Input در حالت Rest، Hover یا Focused باشد
- **آنگاه** متن واردشده SHALL با رنگ #222323 نمایش داده شود

#### Scenario: استایل placeholder در حالت عادی
- **زمانی که** Input خالی باشد و در حالت Rest، Hover یا Focused باشد
- **آنگاه** placeholder SHALL با رنگ #59595a نمایش داده شود

#### Scenario: استایل در حالت Disabled
- **زمانی که** Input در حالت Disabled باشد
- **آنگاه** متن واردشده و placeholder هر دو SHALL با رنگ #bbbcbe نمایش داده شوند

#### Scenario: متن با مقدار موجود
- **زمانی که** Input مقدار داشته باشد
- **آنگاه** placeholder نSHALL نمایش داده شود (رفتار بومی مرورگر)
- **و** قوانین رنگ state SHALL برای متن ورودی برقرار باشد

#### Scenario: تایپوگرافی مطابق Size
- **زمانی که** Size برابر Large یا Medium باشد
- **آنگاه** font-size SHALL 14px و line-height SHALL 2 باشد
- **زمانی که** Size برابر Small باشد
- **آنگاه** font-size SHALL 12px و line-height SHALL 1.5 باشد

#### Scenario: فونت
- **زمانی که** Input رندر شود
- **آنگاه** فونت SHALL Peyda(FaNum) با وزن 400 باشد

---

### Requirement: پشتیبانی از متن راست‌به‌چپ (RTL)
کامپوننت Input SHALL متن راست‌به‌چپ (RTL) را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** المان والد یا خود Input `dir="rtl"` داشته باشد
- **آنگاه** Input SHALL چیدمان RTL داشته باشد:
- آیکن before در سمت راست (start)
- فیلد متن در وسط
- آیکن after در سمت چپ (end)

#### Scenario: چیدمان LTR
- **زمانی که** المان والد `dir="ltr"` داشته باشد
- **آنگاه** Input SHALL چیدمان LTR داشته باشد:
- آیکن before در سمت چپ (start)
- فیلد متن در وسط
- آیکن after در سمت راست (end)

---

### Requirement: رفتار تعاملی (Behavior)
کامپوننت Input SHALL رفتارهای تعاملی مشخص داشته باشد.

#### Scenario: فعال‌سازی Focused
- **زمانی که** Input فوکوس دریافت کند (keyboard یا click)
- **آنگاه** حالت Focused SHALL فعال شود

#### Scenario: Hover فقط در حالت قابل تعامل
- **زمانی که** نشانگر ماوس روی Input قرار بگیرد
- **آنگاه** حالت Hover SHALL فقط اگر Input غیرفعال نباشد فعال شود

#### Scenario: Error یک state منطقی
- **زمانی که** اعتبارسنجی یا منطق فرم خطا تشخیص دهد
- **آنگاه** حالت Error SHALL فعال شود (نه صرفاً بر اساس تعامل کاربر)

#### Scenario: ReadOnly اجازه focus
- **زمانی که** Input در حالت ReadOnly باشد
- **آنگاه** امکان focus و انتخاب متن SHALL مجاز باشد اما تغییر مقدار نSHALL مجاز باشد

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Input SHALL دسترسی‌پذیر باشد و با استانداردهای WCAG 2.1 سطح AA مطابقت داشته باشد.

#### Scenario: استفاده از native input
- **زمانی که** Input رندر شود
- **آنگاه** از `<input>` بومی HTML استفاده شود تا screen readers آن را به درستی شناسایی کنند

#### Scenario: حالت Error با ARIA
- **زمانی که** Input در حالت Error باشد
- **آنگاه** `aria-invalid="true"` SHALL روی input تنظیم شود

#### Scenario: برچسب دسترسی‌پذیر
- **زمانی که** Input بدون label خارجی باشد
- **آنگاه** `aria-label` SHALL ارائه شود

#### Scenario: قابلیت ناوبری با کیبورد
- **زمانی که** Input غیرفعال نباشد
- **آنگاه** Input SHALL با Tab قابل دسترسی و با تایپ قابل استفاده باشد

#### Scenario: کنتراست رنگ
- **زمانی که** Input در هر ترکیب state/size رندر شود
- **آنگاه** متن SHALL حداقل contrast ratio 4.5:1 و placeholder حداقل 3:1 با پس‌زمینه داشته باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Input SHALL از design tokens موجود در tokens.json به عنوان منبع واحد حقیقت استفاده کند.

#### Scenario: ویژگی‌های سفارشی CSS
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--input-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: عملکرد
کامپوننت Input SHALL سبک و با عملکرد خوب باشد.

#### Scenario: اندازه CSS
- **زمانی که** کامپوننت bundle شود
- **آنگاه** اندازه CSS SHALL کمتر از 8KB فشرده‌نشده باشد

---

### Requirement: سازگاری با مرورگرها
کامپوننت Input SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
