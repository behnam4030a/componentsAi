## ADDED Requirements

### Requirement: Message Bar Component Structure
سیستم باید (SHALL) کامپوننت Message Bar را به صورت یک نوار افقی با ساختار زیر ارائه دهد:
- آیکن وضعیت (سمت راست در RTL)
- متن پیام شامل عنوان بولد + توضیحات
- عمل (لینک یا دکمه بستن — سمت چپ در RTL)

#### Scenario: Render Info message bar
- **WHEN** یک عنصر با کلاس `.message-bar.message-bar--info` در DOM وجود دارد
- **THEN** نوار پیام آبی با آیکن info، متن پیام و لینک «بیشتر بدانید» نمایش داده شود

#### Scenario: Render Success message bar
- **WHEN** یک عنصر با کلاس `.message-bar.message-bar--success` در DOM وجود دارد
- **THEN** نوار پیام سبز با آیکن check circle، متن پیام و دکمه بستن (X) نمایش داده شود

#### Scenario: Render Warning message bar
- **WHEN** یک عنصر با کلاس `.message-bar.message-bar--warning` در DOM وجود دارد
- **THEN** نوار پیام نارنجی با آیکن مثلث هشدار، متن پیام و دکمه بستن (X) نمایش داده شود

#### Scenario: Render Danger message bar
- **WHEN** یک عنصر با کلاس `.message-bar.message-bar--danger` در DOM وجود دارد
- **THEN** نوار پیام قرمز با آیکن info circle، متن پیام و دکمه بستن (X) نمایش داده شود

### Requirement: Message Bar Info Variant Styling
واریانت Info باید (SHALL) با مشخصات زیر نمایش داده شود:
- پس‌زمینه: `#f3f9fd`
- بوردر: `1px solid #0078d4`
- border-radius: `10px`
- padding: `8px 19px`
- آیکن وضعیت: info circle، container `40px`، inner `24px`
- متن: فونت `Peyda(FaNum)` — عنوان `SemiBold 18px`، توضیحات `Regular 18px`، line-height `1.8`، رنگ `#222323`
- لینک: فونت `SemiBold 15px`، رنگ `#1a86d9`، با آیکن فلش چپ (container `32px`، inner `24px`)

#### Scenario: Info variant visual appearance
- **WHEN** message bar با واریانت info رندر می‌شود
- **THEN** پس‌زمینه آبی روشن (#f3f9fd) با بوردر آبی (#0078d4) و radius 10px نمایش یابد
- **AND** آیکن info circle در سمت راست و لینک آبی با فلش در سمت چپ باشد

### Requirement: Message Bar Success Variant Styling
واریانت Success باید (SHALL) با مشخصات زیر نمایش داده شود:
- پس‌زمینه: `#f1faf1`
- بوردر: `1px solid #107c10`
- border-radius: `10px`
- padding: `8px 19px`
- آیکن وضعیت: check circle، container `40px`، inner `24px`
- متن: فونت `Peyda(FaNum)` — عنوان `SemiBold 18px`، توضیحات `Regular 18px`، line-height `1.8`، رنگ `#222323`
- دکمه بستن: container `28px`، آیکن X inner `24px`، رنگ `#59595a`

#### Scenario: Success variant visual appearance
- **WHEN** message bar با واریانت success رندر می‌شود
- **THEN** پس‌زمینه سبز روشن (#f1faf1) با بوردر سبز (#107c10) و radius 10px نمایش یابد
- **AND** آیکن check circle در سمت راست و دکمه بستن X در سمت چپ باشد

### Requirement: Message Bar Warning Variant Styling
واریانت Warning باید (SHALL) با مشخصات زیر نمایش داده شود:
- پس‌زمینه: `#fff9f5`
- بوردر: `1px solid #f7630c`
- border-radius: `10px`
- padding: `8px 19px`
- آیکن وضعیت: danger triangle (مثلث هشدار)، container `40px`، inner `24px`
- متن: فونت `Peyda(FaNum)` — عنوان `SemiBold 18px`، توضیحات `Regular 18px`، line-height `1.8`، رنگ `#222323`
- دکمه بستن: container `28px`، آیکن X inner `24px`، رنگ `#59595a`

#### Scenario: Warning variant visual appearance
- **WHEN** message bar با واریانت warning رندر می‌شود
- **THEN** پس‌زمینه نارنجی روشن (#fff9f5) با بوردر نارنجی (#f7630c) و radius 10px نمایش یابد
- **AND** آیکن مثلث هشدار در سمت راست و دکمه بستن X در سمت چپ باشد

### Requirement: Message Bar Danger Variant Styling
واریانت Danger باید (SHALL) با مشخصات زیر نمایش داده شود:
- پس‌زمینه: `#fdf3f4`
- بوردر: `1px solid #c50f1f`
- border-radius: `10px`
- padding: `8px 19px`
- آیکن وضعیت: info circle، container `40px`، inner `24px`
- متن: فونت `Peyda(FaNum)` — عنوان `SemiBold 18px`، توضیحات `Regular 18px`، line-height `1.8`، رنگ `#222323`
- دکمه بستن: container `28px`، آیکن X inner `24px`، رنگ `#59595a`

#### Scenario: Danger variant visual appearance
- **WHEN** message bar با واریانت danger رندر می‌شود
- **THEN** پس‌زمینه قرمز روشن (#fdf3f4) با بوردر قرمز (#c50f1f) و radius 10px نمایش یابد
- **AND** آیکن info circle در سمت راست و دکمه بستن X در سمت چپ باشد

### Requirement: Message Bar Close Behavior
سیستم باید (SHALL) امکان بستن message bar را فراهم کند:
- کلیک روی دکمه بستن (X) در واریانت‌های Success، Warning و Danger
- اضافه شدن کلاس `message-bar--hidden` با انیمیشن transition
- اجرای callback ثبت شده (در صورت وجود)

#### Scenario: Close message bar with close button
- **WHEN** کاربر روی دکمه بستن (X) کلیک می‌کند
- **THEN** message bar با انیمیشن مخفی شود (کلاس `--hidden` اضافه شود)

#### Scenario: Close callback execution
- **WHEN** یک callback با `MessageBar.onClose()` ثبت شده و کاربر message bar را می‌بندد
- **THEN** callback فراخوانی شود

### Requirement: Message Bar JavaScript API
سیستم باید (SHALL) API زیر را از طریق شیء global `MessageBar` ارائه دهد:
- `MessageBar.init()` — فعال‌سازی event listenerها
- `MessageBar.show(element)` — نمایش message bar
- `MessageBar.hide(element)` — مخفی کردن message bar
- `MessageBar.onClose(element, fn)` — ثبت callback بستن

#### Scenario: Auto initialization
- **WHEN** صفحه بارگذاری می‌شود (DOMContentLoaded)
- **THEN** همه عناصر `[data-message-bar]` به صورت خودکار فعال شوند

#### Scenario: Programmatic show/hide
- **WHEN** `MessageBar.show(element)` فراخوانی شود
- **THEN** message bar نمایش داده شود (کلاس `--hidden` حذف شود)
- **WHEN** `MessageBar.hide(element)` فراخوانی شود
- **THEN** message bar مخفی شود (کلاس `--hidden` اضافه شود)

### Requirement: Message Bar RTL Support
کامپوننت باید (SHALL) به صورت کامل از RTL پشتیبانی کند:
- آیکن وضعیت در سمت راست
- متن پیام راست‌چین
- عمل (لینک/بستن) در سمت چپ
- آیکن فلش لینک به سمت چپ

#### Scenario: RTL layout
- **WHEN** صفحه با `dir="rtl"` تنظیم شده
- **THEN** آیکن وضعیت در سمت راست و عمل در سمت چپ قرار گیرد

### Requirement: Message Bar Responsive Design
کامپوننت باید (SHALL) در سه breakpoint واکنش‌گرا باشد:
- **Desktop (>768px)**: چینش تک‌خطی افقی — فونت متن 18px، آیکن 40px، padding 8px 19px
- **Tablet (480–767px)**: چینش تک‌خطی فشرده — فونت متن 15px، آیکن 34px، padding 8px 14px
- **Mobile (<480px)**: فونت متن 14px، آیکن 28px، padding 10px 12px
  - Info: لینک به خط دوم منتقل شود (flex-wrap)
  - Success, Warning, Danger: تک‌خطی با دکمه بستن در بالا-چپ (align-items: flex-start)

تمام تغییرات سایز از طریق override کردن CSS custom properties در media query انجام شود.

#### Scenario: Tablet viewport renders compact layout
- **WHEN** عرض viewport بین 480 تا 767 پیکسل باشد
- **THEN** فونت متن 15px، آیکن 34px و padding فشرده‌تر اعمال شود

#### Scenario: Mobile viewport wraps Info link to second line
- **WHEN** عرض viewport زیر 480 پیکسل باشد و واریانت Info نمایش داده شود
- **THEN** لینک «بیشتر بدانید» به خط دوم منتقل شود (flex-wrap)
- **AND** فونت متن 14px و آیکن 28px باشد

#### Scenario: Mobile viewport keeps close button aligned top
- **WHEN** عرض viewport زیر 480 پیکسل باشد و واریانت Success، Warning یا Danger نمایش داده شود
- **THEN** دکمه بستن در بالا-چپ (RTL) تراز شود (align-items: flex-start)

### Requirement: Message Bar Accessibility
کامپوننت باید (SHALL) از استانداردهای دسترسی‌پذیری پیروی کند:
- `role="status"` روی container پیام
- `aria-label="بستن"` روی دکمه بستن
- قابل تعامل با کیبورد (Tab + Enter)

#### Scenario: Screen reader announces message
- **WHEN** یک message bar در DOM وجود دارد
- **THEN** صفحه‌خوان محتوای متن پیام را اعلام کند (به واسطه `role="status"`)

#### Scenario: Close button keyboard accessible
- **WHEN** کاربر با Tab به دکمه بستن می‌رسد و Enter می‌زند
- **THEN** message bar بسته شود
