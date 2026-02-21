# مشخصات کامپوننت Label

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Label
کامپوننت Label SHALL برای نمایش برچسب متنی در کنار یا بالای فیلدها (مثل Input، Select، Checkbox و ...) استفاده شود. این کامپوننت نقش اطلاع‌رسانی دارد و رفتار تعاملی مستقل ندارد، اما ظاهر آن بسته به وضعیت‌هایی مثل required و disabled تغییر می‌کند. همچنین با متنی ساده برای دسته‌بندی اطلاعات نیز قابل استفاده می‌باشد.

#### Scenario: استفاده به عنوان برچسب فیلد
- **زمانی که** یک فیلد ورودی (Input، Select، Checkbox) نیاز به برچسب متنی داشته باشد
- **آنگاه** از کامپوننت Label استفاده شود

#### Scenario: استفاده به عنوان متن دسته‌بندی
- **زمانی که** نیاز به نمایش یک متن ساده برای دسته‌بندی اطلاعات باشد
- **آنگاه** از کامپوننت Label بدون required indicator استفاده شود

---

### Requirement: خصوصیت type (نوع فونت)
کامپوننت Label SHALL از دو نوع فونت پشتیبانی کند: Regular و Semibold. خصوصیت type فقط روی font-weight اثر می‌گذارد و MUST NOT باعث تغییر رنگ، اندازه یا فاصله‌ها شود.

#### Scenario: نوع Regular (پیش‌فرض)
- **زمانی که** هیچ modifier class اضافه نشده باشد
- **آنگاه** Label SHALL با font-weight: 400 (Regular) نمایش داده شود

#### Scenario: نوع Semibold
- **زمانی که** class `.label--semibold` اعمال شود
- **آنگاه** Label SHALL با font-weight: 500 (Medium/Semibold) نمایش داده شود
- **و** فقط font-weight SHALL تغییر کند، نه رنگ، اندازه یا فاصله‌ها

#### Scenario: Semibold برای تأکید
- **زمانی که** نیاز به تأکید بیشتر یا عناوین فرم باشد
- **آنگاه** از نوع Semibold استفاده شود، اما از نظر رفتاری تفاوتی با Regular نداشته باشد

#### Scenario: همه typeها در همه sizeها
- **زمانی که** هر type با هر size ترکیب شود
- **آنگاه** Label SHALL بدون تداخل به درستی رندر شود

---

### Requirement: خصوصیت size (اندازه تایپوگرافی)
کامپوننت Label SHALL سه سایز را پشتیبانی کند: Large، Medium و Small. Size SHALL فقط روی font-size و line-height تأثیر بگذارد.

#### Scenario: سایز Large Regular
- **زمانی که** class `.label--large` بدون `.label--semibold` اعمال شود
- **آنگاه** Label SHALL با fontSize=16px، fontWeight=400، lineHeight=1.5 نمایش داده شود

#### Scenario: سایز Medium Regular
- **زمانی که** class `.label--medium` بدون `.label--semibold` اعمال شود
- **آنگاه** Label SHALL با fontSize=14px، fontWeight=400، lineHeight=1.5 نمایش داده شود

#### Scenario: سایز Small Regular
- **زمانی که** class `.label--small` بدون `.label--semibold` اعمال شود
- **آنگاه** متن Label SHALL با fontSize=12px، fontWeight=400، lineHeight=1.5 نمایش داده شود
- **و** ستاره required (در صورت وجود) SHALL با fontSize=13px، lineHeight=1.3 نمایش داده شود

#### Scenario: سایز Large Semibold
- **زمانی که** class `.label--large.label--semibold` اعمال شود
- **آنگاه** Label SHALL با fontSize=16px، fontWeight=500، lineHeight=1.5 نمایش داده شود

#### Scenario: سایز Medium Semibold
- **زمانی که** class `.label--medium.label--semibold` اعمال شود
- **آنگاه** Label SHALL با fontSize=12px، fontWeight=500، lineHeight=1.5 نمایش داده شود

#### Scenario: سایز Small Semibold
- **زمانی که** class `.label--small.label--semibold` اعمال شود
- **آنگاه** متن Label SHALL با fontSize=12px، fontWeight=500، lineHeight=1.5 نمایش داده شود
- **و** ستاره required (در صورت وجود) SHALL با fontSize=13px، fontWeight=500، lineHeight=1.3 نمایش داده شود

---

### Requirement: خصوصیت disabled (حالت غیرفعال)
کامپوننت Label SHALL از حالت disabled پشتیبانی کند که مشخص می‌کند Label مربوط به یک فیلد غیرفعال است.

#### Scenario: حالت عادی (non-disabled)
- **زمانی که** class `.label--disabled` وجود نداشته باشد
- **آنگاه** متن Label SHALL با رنگ #222323 نمایش داده شود

#### Scenario: حالت disabled
- **زمانی که** class `.label--disabled` اعمال شود
- **آنگاه** متن Label SHALL با رنگ #bbbcbe نمایش داده شود
- **و** اگر required indicator وجود داشته باشد، آن نیز SHALL با رنگ #bbbcbe نمایش داده شود

#### Scenario: بدون state تعاملی
- **زمانی که** نشانگر ماوس روی Label قرار بگیرد یا فیلد مرتبط focus داشته باشد
- **آنگاه** رنگ Label MUST NOT تغییر کند، مگر اینکه در سیستم طراحی مشخصاً تعریف شده باشد

#### Scenario: disabled فقط بصری
- **زمانی که** Label در حالت disabled باشد
- **آنگاه** Label SHALL فقط تغییر بصری داشته باشد و هیچ تعامل‌پذیری مستقل نداشته باشد

---

### Requirement: خصوصیت required (نشانگر اجباری)
کامپوننت Label SHALL از نمایش اختیاری یک required indicator (علامت *) پشتیبانی کند.

#### Scenario: نمایش required indicator
- **زمانی که** required فعال باشد
- **آنگاه** یک ستاره (*) SHALL در کنار متن Label نمایش داده شود
- **و** رنگ ستاره SHALL در حالت عادی #c50f1f (danger) باشد

#### Scenario: عدم نمایش required indicator
- **زمانی که** required غیرفعال باشد
- **آنگاه** ستاره MUST NOT نمایش داده شود

#### Scenario: required + disabled
- **زمانی که** هم required و هم disabled فعال باشند
- **آنگاه** ستاره SHALL همچنان نمایش داده شود اما با رنگ disabled (#bbbcbe)

#### Scenario: required indicator بخشی از Label
- **زمانی که** required indicator نمایش داده شود
- **آنگاه** آن indicator SHALL بخشی از Label باشد و MUST NOT به صورت مستقل مدیریت شود

#### Scenario: required فقط بصری
- **زمانی که** required فعال باشد
- **آنگاه** این SHALL فقط یک نشانه بصری باشد و منطق اعتبارسنجی فرم را پیاده‌سازی نکند

---

### Requirement: قوانین چیدمان و ساختار داخلی (Layout Rules)
کامپوننت Label SHALL ساختار بصری منظم با flex layout داشته باشد.

#### Scenario: ساختار بصری
- **زمانی که** Label رندر شود
- **آنگاه** ساختار داخلی SHALL به صورت [label text] [required indicator (*)] باشد (متن اول، ستاره بعد از آن)

#### Scenario: فاصله بین المان‌ها
- **زمانی که** required indicator و متن هر دو وجود داشته باشند
- **آنگاه** فاصله بین آنها SHALL 4px (از design tokens) باشد

#### Scenario: تراز عمودی
- **زمانی که** required indicator و متن رندر شوند
- **آنگاه** تراز عمودی SHALL با align-items: start باشد تا indicator با بالای خط اول متن هم‌تراز شود

#### Scenario: ساختار بدون required
- **زمانی که** required غیرفعال باشد
- **آنگاه** Label SHALL فقط شامل متن باشد بدون فضای اضافی

---

### Requirement: پشتیبانی از متن راست‌به‌چپ (RTL/LTR)
کامپوننت Label SHALL هم RTL و هم LTR را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** المان والد یا خود Label `dir="rtl"` داشته باشد
- **آنگاه** متن SHALL در سمت راست (start) و required indicator در سمت چپ (end) قرار بگیرد

#### Scenario: چیدمان LTR
- **زمانی که** المان والد `dir="ltr"` داشته باشد
- **آنگاه** متن SHALL در سمت چپ (start) و required indicator در سمت راست (end) قرار بگیرد

#### Scenario: سازگاری خودکار
- **زمانی که** direction صفحه تغییر کند
- **آنگاه** جایگاه indicator SHALL به صورت خودکار (با flexbox) سازگار شود

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Label SHALL دسترسی‌پذیر باشد و با استانداردهای WCAG 2.1 سطح AA مطابقت داشته باشد.

#### Scenario: استفاده از semantic label
- **زمانی که** Label رندر شود
- **آنگاه** از `<label>` بومی HTML استفاده شود تا screen readers آن را به درستی شناسایی کنند

#### Scenario: ارتباط با فیلد
- **زمانی که** Label با یک فیلد ورودی مرتبط باشد
- **آنگاه** ارتباط SHALL از طریق `for`/`id` یا nesting در لایه پیاده‌سازی برقرار شود (خارج از scope استایل)

#### Scenario: کنتراست رنگ
- **زمانی که** Label رندر شود
- **آنگاه** متن SHALL حداقل contrast ratio 4.5:1 با پس‌زمینه داشته باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Label SHALL از design tokens موجود در tokens.json به عنوان منبع واحد حقیقت استفاده کند.

#### Scenario: ویژگی‌های سفارشی CSS
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--label-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: سازگاری با مرورگرها
کامپوننت Label SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
