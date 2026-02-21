# مشخصات کامپوننت Tag

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Tag
کامپوننت Tag SHALL برای نمایش اطلاعات کوتاه، وضعیت‌ها، دسته‌بندی‌ها یا مقادیر انتخاب‌شده استفاده شود. Tag یک عنصر سبک و غیرمسدودکننده است که می‌تواند صرفا نمایشی باشد یا امکان تعامل محدود داشته باشد.

#### Scenario: نمایش اطلاعات کوتاه
- **زمانی که** نیاز به نمایش وضعیت، دسته‌بندی یا مقدار انتخاب‌شده باشد
- **آنگاه** از کامپوننت Tag استفاده شود

#### Scenario: حذف تگ
- **زمانی که** کاربر بخواهد یک مقدار انتخاب‌شده را حذف کند
- **آنگاه** از Tag با dismiss=true استفاده شود

---

### Requirement: خصوصیت state (وضعیت تعاملی)
کامپوننت Tag SHALL چهار وضعیت تعاملی/سیستمی را پشتیبانی کند: Rest، Hover، Focus و Disabled.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** Tag SHALL در حالت پیش‌فرض نمایش داده شود

#### Scenario: حالت Hover
- **زمانی که** نشانگر روی Tag قرار بگیرد و Tag غیرفعال نباشد
- **آنگاه** رنگ پس‌زمینه (Filled) یا border و متن (Outline) SHALL تغییر کند

#### Scenario: حالت Focus
- **زمانی که** Tag فوکوس دریافت کند و Tag غیرفعال نباشد
- **آنگاه** یک focus ring SHALL با border 1px solid #222323 نمایش داده شود
- **و** focus ring MUST NOT باعث تغییر اندازه یا layout Tag شود

#### Scenario: حالت Disabled
- **زمانی که** Tag غیرفعال باشد
- **آنگاه** رنگ‌ها SHALL به نسخه غیرفعال تبدیل شوند (متن #bbbcbe)
- **و** هیچ state تعاملی دیگری (hover، focus) MUST NOT فعال شود
- **و** تمام عناصر داخلی (متن، آیکن، dismiss) SHALL استایل disabled داشته باشند

#### Scenario: اولویت stateها
- **زمانی که** چند state همزمان فعال باشند
- **آنگاه** اولویت SHALL به ترتیب زیر باشد: disabled > focus > hover > rest

---

### Requirement: خصوصیت radius (شکل گوشه‌ها)
کامپوننت Tag SHALL دو شکل گوشه را پشتیبانی کند.

#### Scenario: حالت Rounded
- **زمانی که** radius=rounded باشد
- **آنگاه** Tag SHALL با border-radius 8px نمایش داده شود

#### Scenario: حالت Circular
- **زمانی که** radius=circular باشد
- **آنگاه** Tag SHALL با border-radius 360px (pill-like) نمایش داده شود

#### Scenario: استقلال radius از سایر خصوصیات
- **زمانی که** radius تغییر کند
- **آنگاه** MUST NOT روی padding، اندازه متن یا رفتار stateها اثر بگذارد

---

### Requirement: خصوصیت size (ابعاد)
کامپوننت Tag SHALL سه سایز را پشتیبانی کند.

#### Scenario: سایز Small
- **زمانی که** size=small باشد
- **آنگاه** Tag SHALL با ارتفاع 24px، padding افقی 8px، font-size 13px و line-height 1.3 نمایش داده شود
- **و** اندازه icon wrapper SHALL 18px باشد

#### Scenario: سایز Medium
- **زمانی که** size=medium باشد
- **آنگاه** Tag SHALL با ارتفاع 32px، padding افقی 8px، font-size 14px و line-height 1.5 نمایش داده شود
- **و** اندازه icon wrapper SHALL 18px باشد

#### Scenario: سایز Large
- **زمانی که** size=large باشد
- **آنگاه** Tag SHALL با ارتفاع 37px، padding افقی 12px، font-size 16px و line-height 1.5 نمایش داده شود
- **و** اندازه icon wrapper SHALL 22px باشد

#### Scenario: سازگاری size با سایر خصوصیات
- **زمانی که** size تغییر کند
- **آنگاه** همه stateها و styleها SHALL در همه sizeها قابل استفاده باشند

---

### Requirement: خصوصیت style (نوع نمایش بصری)
کامپوننت Tag SHALL دو استایل بصری را پشتیبانی کند.

#### Scenario: استایل Filled
- **زمانی که** style=filled باشد
- **آنگاه** Tag SHALL دارای پس‌زمینه رنگی باشد
- **و** border SHALL 2px solid سفید (#ffffff) باشد
- **و** متن و آیکن‌ها SHALL با کنتراست مناسب روی پس‌زمینه نمایش داده شوند

#### Scenario: استایل Outline
- **زمانی که** style=outline باشد
- **آنگاه** Tag SHALL بدون پس‌زمینه و با border 1px solid رنگی نمایش داده شود
- **و** رنگ متن و آیکن SHALL با رنگ border هماهنگ باشد

---

### Requirement: خصوصیت color (پالت رنگی)
کامپوننت Tag SHALL چهار پالت رنگی را پشتیبانی کند.

#### Scenario: رنگ Gray
- **زمانی که** color=gray باشد
- **آنگاه** Tag SHALL از رنگ‌های خنثی استفاده کند (Filled bg: #f6f8fa، text: #222323)

#### Scenario: رنگ Green
- **زمانی که** color=green باشد
- **آنگاه** Tag SHALL از رنگ‌های موفقیت استفاده کند (Filled bg: #f1faf1، text: #107c10)

#### Scenario: رنگ Orange
- **زمانی که** color=orange باشد
- **آنگاه** Tag SHALL از رنگ‌های هشدار استفاده کند (Filled bg: #fff9f5، text: #f7630c)

#### Scenario: رنگ Red
- **زمانی که** color=red باشد
- **آنگاه** Tag SHALL از رنگ‌های خطر استفاده کند (Filled bg: #fdf3f4، text: #c50f1f)

#### Scenario: رنگ ترکیبی (color × style × state)
- **زمانی که** Tag رندر شود
- **آنگاه** استایل نهایی رنگ (پس‌زمینه، بوردر، متن، آیکن) SHALL از ترکیب color با style و state به‌دست آید

#### Scenario: رنگ در حالت Disabled
- **زمانی که** Tag در حالت disabled باشد
- **آنگاه** رنگ‌ها SHALL به نسخه غیرفعال یکسان تبدیل شوند (Filled: bg #e7e9eb، Outline: border #e7e9eb، متن #bbbcbe)

---

### Requirement: خصوصیت dismiss (امکان حذف)
کامپوننت Tag SHALL از نمایش دکمه حذف پشتیبانی کند.

#### Scenario: dismiss فعال
- **زمانی که** dismiss=true باشد
- **آنگاه** یک dismiss icon (×) SHALL در Tag نمایش داده شود
- **و** کلیک روی آیکن SHALL منطق حذف را فعال کند (منطق حذف خارج از کامپوننت)

#### Scenario: dismiss غیرفعال
- **زمانی که** dismiss=false باشد
- **آنگاه** هیچ عنصر حذف‌کننده‌ای MUST NOT نمایش داده شود

#### Scenario: dismiss در حالت Disabled
- **زمانی که** Tag در حالت disabled باشد و dismiss=true باشد
- **آنگاه** dismiss icon SHALL نمایش داده شود اما قابل تعامل نباشد

#### Scenario: رنگ dismiss icon
- **زمانی که** dismiss icon نمایش داده شود
- **آنگاه** رنگ آیکن SHALL از قوانین رنگ Tag (بر اساس color، style و state) تبعیت کند

---

### Requirement: خصوصیت focus (فوکوس‌پذیری)
کامپوننت Tag SHALL از قابلیت فوکوس‌پذیری اختیاری پشتیبانی کند.

#### Scenario: فوکوس فعال
- **زمانی که** focus=true باشد
- **آنگاه** Tag SHALL فوکوس‌پذیر باشد (tabindex="0") و focus ring نمایش داده شود

#### Scenario: فوکوس غیرفعال
- **زمانی که** focus=false باشد
- **آنگاه** Tag MUST NOT فوکوس‌پذیر باشد و state focus فعال نخواهد شد

#### Scenario: فوکوس به عنوان overlay state
- **زمانی که** فوکوس فعال باشد
- **آنگاه** focus ring SHALL همزمان با rest یا hover قابل نمایش باشد
- **و** MUST NOT رنگ متن و آیکن‌ها را override کند
- **و** MUST NOT باعث تغییر اندازه یا layout شود

#### Scenario: فوکوس در حالت Disabled
- **زمانی که** Tag در حالت disabled باشد
- **آنگاه** فوکوس MUST NOT نمایش داده شود

---

### Requirement: خصوصیت icon (نمایش آیکن)
کامپوننت Tag SHALL از نمایش آیکن اختیاری پشتیبانی کند.

#### Scenario: آیکن فعال
- **زمانی که** icon=true باشد
- **آنگاه** یک آیکن SHALL در کنار متن Tag نمایش داده شود (سمت start، قبل از متن)

#### Scenario: آیکن غیرفعال
- **زمانی که** icon=false باشد
- **آنگاه** Tag SHALL فقط شامل متن باشد (به‌جز dismiss icon در صورت فعال بودن)

#### Scenario: اندازه آیکن
- **زمانی که** آیکن نمایش داده شود
- **آنگاه** اندازه آیکن wrapper SHALL از mapping سایز Tag تبعیت کند (Large: 22px، Medium/Small: 18px)

#### Scenario: رنگ آیکن
- **زمانی که** آیکن نمایش داده شود
- **آنگاه** رنگ آیکن SHALL دقیقا مانند رنگ متن Tag باشد (از ترکیب color، style و state)

---

### Requirement: قوانین رنگ Filled Style
استایل Filled SHALL رنگ‌بندی مشخص برای هر ترکیب color × state داشته باشد.

#### Scenario: رنگ‌بندی Filled — Rest
- **زمانی که** Tag در حالت rest باشد
- **آنگاه** Filled SHALL پس‌زمینه رنگی + border 2px solid #ffffff داشته باشد:
  - Gray: bg #f6f8fa، text #222323
  - Green: bg #f1faf1، text #107c10
  - Orange: bg #fff9f5، text #f7630c
  - Red: bg #fdf3f4، text #c50f1f

#### Scenario: رنگ‌بندی Filled — Hover
- **زمانی که** Tag در حالت hover باشد
- **آنگاه** Filled SHALL پس‌زمینه تیره‌تر داشته باشد:
  - Gray: bg #f1f3f5
  - Green: bg #e7f2e7
  - Orange: bg #feefe7
  - Red: bg #f9e7e9

#### Scenario: رنگ‌بندی Filled — Focus
- **زمانی که** Tag در حالت focus باشد
- **آنگاه** Filled SHALL border 1px solid #222323 داشته باشد (جایگزین border سفید)

#### Scenario: رنگ‌بندی Filled — Disabled
- **زمانی که** Tag در حالت disabled باشد
- **آنگاه** Filled SHALL bg #e7e9eb، بدون border قابل مشاهده، و text #bbbcbe داشته باشد

---

### Requirement: قوانین رنگ Outline Style
استایل Outline SHALL رنگ‌بندی مشخص برای هر ترکیب color × state داشته باشد.

#### Scenario: رنگ‌بندی Outline — Rest
- **زمانی که** Tag در حالت rest باشد
- **آنگاه** Outline SHALL بدون پس‌زمینه + border 1px solid رنگی داشته باشد:
  - Gray: border #e2e4e6، text #222323
  - Green: border #9fd89f، text #107c10
  - Orange: border #fdcfb4، text #f7630c
  - Red: border #eeacb2، text #c50f1f

#### Scenario: رنگ‌بندی Outline — Hover
- **زمانی که** Tag در حالت hover باشد
- **آنگاه** Outline SHALL border تیره‌تر و متن تیره‌تر (برای رنگ‌های غیر gray) داشته باشد:
  - Gray: border #e2e4e6، text #222323 (بدون تغییر)
  - Green: border #107c10، text #0c5e0c
  - Orange: border #f7630c، text #bc4b09
  - Red: border #c50f1f، text #960b18

#### Scenario: رنگ‌بندی Outline — Focus
- **زمانی که** Tag در حالت focus باشد
- **آنگاه** Outline SHALL border 1px solid #222323 داشته باشد

#### Scenario: رنگ‌بندی Outline — Disabled
- **زمانی که** Tag در حالت disabled باشد
- **آنگاه** Outline SHALL border 1px solid #e7e9eb و text #bbbcbe داشته باشد

---

### Requirement: قوانین چیدمان (Layout Rules)
کامپوننت Tag SHALL ساختار flexbox با تراز مرکزی داشته باشد.

#### Scenario: ساختار کلی
- **زمانی که** Tag رندر شود
- **آنگاه** ساختار SHALL به صورت [icon (optional)] [text] [dismiss icon (optional)] باشد
- **و** تراز عمودی همه عناصر SHALL centered باشد
- **و** فاصله بین عناصر SHALL 4px (gap) باشد

#### Scenario: سازگاری RTL/LTR
- **زمانی که** جهت نمایش تغییر کند
- **آنگاه** چیدمان عناصر SHALL با جهت متن سازگار باشد

---

### Requirement: پشتیبانی RTL/LTR
کامپوننت Tag SHALL هم RTL و هم LTR را پشتیبانی کند.

#### Scenario: چیدمان RTL
- **زمانی که** `dir="rtl"` باشد
- **آنگاه** icon در سمت راست (start)، text در وسط و dismiss در سمت چپ (end) باشد

#### Scenario: چیدمان LTR
- **زمانی که** `dir="ltr"` باشد
- **آنگاه** icon در سمت چپ (start)، text در وسط و dismiss در سمت راست (end) باشد

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Tag SHALL دسترسی‌پذیر باشد.

#### Scenario: فوکوس‌پذیری با کیبورد
- **زمانی که** Tag فوکوس‌پذیر باشد (focus=true)
- **آنگاه** Tag SHALL با Tab قابل دسترسی باشد

#### Scenario: dismiss button accessibility
- **زمانی که** dismiss=true باشد
- **آنگاه** dismiss button SHALL با keyboard قابل فعال‌سازی باشد
- **و** aria-label مناسب داشته باشد

#### Scenario: کنتراست رنگ
- **زمانی که** Tag رندر شود
- **آنگاه** کنتراست رنگ متن روی پس‌زمینه SHALL حداقل 4.5:1 باشد (WCAG AA)

---

### Requirement: یکپارچگی با Design Token
کامپوننت Tag SHALL از design tokens موجود در tokens.json استفاده کند.

#### Scenario: CSS custom properties
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties با پیشوند `--tag-` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده CSS custom property را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: سازگاری با مرورگرها
کامپوننت Tag SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند
