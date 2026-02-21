## ADDED Requirements

### Requirement: Toast Purpose and Description
کامپوننت Toast SHALL برای نمایش پیام‌های موقتی و غیرمسدودکننده (اعلان‌ها) به کاربر استفاده شود. Toast پیام‌هایی مانند تایید اقدام کاربر، اطلاع‌رسانی رویداد، یا نمایش وضعیت فرآیند را نشان می‌دهد. اطلاعات موجود در Toast مفید و مرتبط است اما هرگز حیاتی نیست.

#### Scenario: Toast basic display
- **WHEN** یک رویداد نیازمند اطلاع‌رسانی رخ دهد
- **THEN** Toast با عنوان و وضعیت مناسب نمایش داده شود
- **AND** Toast نباید مانع تعامل کاربر با سایر بخش‌های UI شود

#### Scenario: Toast non-blocking behavior
- **WHEN** Toast نمایش داده شود
- **THEN** فوکوس کاربر نباید از المان فعلی گرفته شود
- **AND** کاربر باید بتواند با سایر بخش‌های صفحه تعامل داشته باشد

### Requirement: Toast State Variants
کامپوننت Toast SHALL از 4 واریانت وضعیت پشتیبانی کند: Success، Danger، Warning و Neutral. هر واریانت با modifier class مشخص می‌شود و رنگ‌های اصلی Toast را تعیین می‌کند شامل: رنگ نوار پایین (timer indicator)، رنگ آیکن وضعیت و تاکیدات بصری (border/shadow/accent). محتوای متنی (title و description) از نظر ساختار ثابت است و فقط رنگ‌ها با state تغییر می‌کنند.

#### Scenario: Success variant
- **WHEN** Toast با کلاس `toast--success` ایجاد شود
- **THEN** آیکن وضعیت با رنگ سبز (#107c10) و پس‌زمینه دایره‌ای (#f1faf1) نمایش یابد
- **AND** نوار تایمر با رنگ سبز (#107c10) نمایش یابد
- **AND** shadow سبز (rgba(16,124,16,0.25)) اعمال شود

#### Scenario: Danger variant
- **WHEN** Toast با کلاس `toast--danger` ایجاد شود
- **THEN** آیکن وضعیت با رنگ قرمز (#c50f1f) و پس‌زمینه دایره‌ای (#fdf3f4) نمایش یابد
- **AND** نوار تایمر با رنگ قرمز (#c50f1f) نمایش یابد
- **AND** shadow قرمز (rgba(197,15,31,0.25)) اعمال شود

#### Scenario: Warning variant
- **WHEN** Toast با کلاس `toast--warning` ایجاد شود
- **THEN** آیکن وضعیت با رنگ نارنجی (#f7630c) و پس‌زمینه دایره‌ای (#fff9f5) نمایش یابد
- **AND** نوار تایمر با رنگ نارنجی (#f7630c) نمایش یابد
- **AND** shadow نارنجی (rgba(247,99,12,0.25)) اعمال شود

#### Scenario: Neutral variant
- **WHEN** Toast با کلاس `toast--neutral` ایجاد شود
- **THEN** آیکن وضعیت با رنگ خاکستری (#454546) و پس‌زمینه دایره‌ای (#f6f8fa) نمایش یابد
- **AND** نوار تایمر با رنگ خاکستری (#454546) نمایش یابد
- **AND** shadow خاکستری (rgba(69,69,70,0.25)) اعمال شود

### Requirement: Toast Content Structure
کامپوننت Toast SHALL از اجزای زیر تشکیل شود: dismiss button (آیکن ضربدر)، title (متن اصلی، الزامی)، description (متن توضیحی، اختیاری)، status icon (آیکن وضعیت در دایره رنگی) و timer indicator (نوار پیشرفت پایینی). ساختار بصری: [dismiss] [text content] [status icon] و در پایین [timer indicator].

#### Scenario: Toast with title and description
- **WHEN** Toast با title و description ایجاد شود
- **THEN** عنوان با فونت 18px و وزن 500 نمایش یابد
- **AND** توضیحات با فونت 14px و وزن 400 زیر عنوان نمایش یابد

#### Scenario: Toast with title only (no description)
- **WHEN** Toast فقط با title و بدون description ایجاد شود
- **THEN** layout باید بدون فضای خالی اضافی تنظیم شود
- **AND** عنوان به درستی نمایش یابد

#### Scenario: Visual layout order
- **WHEN** Toast نمایش داده شود
- **THEN** dismiss button در سمت start (راست در RTL) قرار گیرد
- **AND** محتوای متنی در وسط قرار گیرد
- **AND** آیکن وضعیت در سمت end (چپ در RTL) قرار گیرد
- **AND** نوار تایمر در پایین Toast قرار گیرد

### Requirement: Timer Indicator (Auto Dismiss)
کامپوننت Toast SHALL به صورت پیش‌فرض دارای یک تایمر نمایش باشد. تایمر به شکل یک نوار افقی در پایین Toast نمایش داده می‌شود و از حالت پر (full) به خالی (empty) تغییر می‌کند. حرکت نوار باید پیوسته و یکنواخت (linear) باشد. رنگ نوار بر اساس state تعیین می‌شود. وقتی نوار به انتها برسد، Toast باید به‌صورت خودکار از UI حذف شود. تایمر فقط نشانگر زمان است و نباید باعث تغییر layout Toast شود.

#### Scenario: Timer animation
- **WHEN** Toast نمایش داده شود
- **THEN** نوار تایمر از عرض 100% با انیمیشن linear به 0% کاهش یابد
- **AND** رنگ نوار مطابق واریانت Toast باشد

#### Scenario: Auto dismiss after timer
- **WHEN** نوار تایمر به انتها برسد (عرض 0%)
- **THEN** Toast باید به‌صورت خودکار از UI حذف شود

#### Scenario: Timer does not affect layout
- **WHEN** انیمیشن تایمر در حال اجرا باشد
- **THEN** layout و ابعاد Toast نباید تغییر کند

### Requirement: Manual Dismiss
کامپوننت Toast SHALL دارای یک dismiss button (ضربدر) باشد. کلیک روی dismiss button تایمر را متوقف می‌کند و Toast را بلافاصله از UI حذف می‌کند. منطق حذف Toast (state management) خارج از خود کامپوننت است و توسط سیستم نمایش Toast مدیریت می‌شود.

#### Scenario: Dismiss button click
- **WHEN** کاربر روی dismiss button کلیک کند
- **THEN** انیمیشن تایمر متوقف شود
- **AND** Toast بلافاصله از UI حذف شود

#### Scenario: Dismiss button keyboard access
- **WHEN** کاربر با Tab به dismiss button برسد و Enter یا Space بزند
- **THEN** Toast باید بسته شود (مشابه کلیک)

### Requirement: Status Icon
آیکن وضعیت (status icon) SHALL بر اساس state انتخاب و با رنگ مطابق واریانت Toast رندر شود. آیکن در یک دایره رنگی با پس‌زمینه و border مخصوص هر واریانت قرار می‌گیرد. رنگ آیکن از قوانین رنگ Toast تبعیت می‌کند و نباید مستقل تعیین شود.

#### Scenario: Icon per variant
- **WHEN** Toast با واریانت Success ایجاد شود
- **THEN** آیکن check-circle با رنگ سبز در دایره سبز روشن نمایش یابد
- **WHEN** Toast با واریانت Danger ایجاد شود
- **THEN** آیکن close-square با رنگ قرمز در دایره قرمز روشن نمایش یابد
- **WHEN** Toast با واریانت Warning ایجاد شود
- **THEN** آیکن danger-triangle با رنگ نارنجی در دایره نارنجی روشن نمایش یابد
- **WHEN** Toast با واریانت Neutral ایجاد شود
- **THEN** آیکن info-circle با رنگ خاکستری در دایره خاکستری روشن نمایش یابد

#### Scenario: Icon color follows state
- **WHEN** واریانت Toast تغییر کند
- **THEN** رنگ آیکن، پس‌زمینه دایره و border دایره همگی مطابق واریانت جدید تغییر کنند

### Requirement: Typography Rules
عنوان (title) SHALL متن اصلی Toast باشد با فونت 18px، وزن 500 (Medium) و line-height 1.3. توضیحات (description) متن اختیاری با فونت 14px، وزن 400 (Regular) و line-height 1.5 است. تغییر state نباید ساختار تایپوگرافی را تغییر دهد، فقط رنگ‌ها تغییر می‌کنند.

#### Scenario: Title typography
- **WHEN** Toast نمایش داده شود
- **THEN** عنوان با فونت Peyda(FaNum)، سایز 18px، وزن 500 و رنگ #222323 نمایش یابد

#### Scenario: Description typography
- **WHEN** Toast با description نمایش داده شود
- **THEN** توضیحات با فونت Peyda(FaNum)، سایز 14px، وزن 400 و رنگ #59595a نمایش یابد

#### Scenario: Typography unchanged across states
- **WHEN** واریانت Toast تغییر کند
- **THEN** ساختار تایپوگرافی (font-size, font-weight, line-height) ثابت بماند

### Requirement: Toast Layout and Dimensions
کامپوننت Toast SHALL با عرض 420px، padding 16px، border-radius 8px و border 2px solid سفید نمایش یابد. آیکن وضعیت 36px در دایره‌ای با padding 12px و border-radius کامل (360px) قرار می‌گیرد. نوار تایمر 3px ارتفاع دارد و با border-radius 8px در پایین Toast با offset -2px از چپ و راست قرار می‌گیرد.

#### Scenario: Toast dimensions
- **WHEN** Toast نمایش داده شود
- **THEN** عرض Toast باید 420px باشد
- **AND** padding داخلی 16px و border-radius 8px باشد
- **AND** gap بین المان‌ها 16px باشد

#### Scenario: Progress bar position
- **WHEN** نوار تایمر نمایش داده شود
- **THEN** در پایین Toast با position absolute قرار گیرد
- **AND** از چپ و راست با offset -2px گسترش یابد

### Requirement: Interaction Rules
Toast SHALL یک کامپوننت غیرمسدودکننده باشد و نباید فوکوس را از کاربر بگیرد. hover یا focus state تعاملی برای خود Toast وجود ندارد مگر برای dismiss button. dismiss button باید ناحیه کلیک استاندارد و قابل دسترس داشته باشد.

#### Scenario: No focus stealing
- **WHEN** Toast نمایش داده شود
- **THEN** فوکوس المان فعلی کاربر نباید تغییر کند

#### Scenario: Only dismiss button is interactive
- **WHEN** کاربر روی بدنه Toast hover کند
- **THEN** هیچ تغییر بصری رخ ندهد
- **BUT** hover روی dismiss button باید تغییر بصری مناسب داشته باشد

### Requirement: Accessibility
Toast SHALL برای screen reader قابل اعلان باشد. برای واریانت‌های Success و Neutral از `role="status"` و برای Danger و Warning از `role="alert"` استفاده شود. Toast نباید مانع تعامل کاربر با سایر بخش‌های UI شود. dismiss button باید قابل دسترس با کیبورد باشد و `aria-label` مناسب داشته باشد.

#### Scenario: Screen reader announcement
- **WHEN** Toast با واریانت Success یا Neutral نمایش داده شود
- **THEN** از `role="status"` استفاده شود (polite announcement)
- **WHEN** Toast با واریانت Danger یا Warning نمایش داده شود
- **THEN** از `role="alert"` استفاده شود (assertive announcement)

#### Scenario: Keyboard accessible dismiss
- **WHEN** کاربر با Tab navigate کند
- **THEN** dismiss button باید قابل focus باشد
- **AND** با Enter یا Space قابل فعال‌سازی باشد

### Requirement: RTL Support
کامپوننت Toast SHALL از RTL پشتیبانی کامل داشته باشد. در حالت RTL، dismiss button سمت راست و آیکن وضعیت سمت چپ قرار گیرد. متن از سمت راست شروع شود. در صورت استفاده از `dir="ltr"`، ترتیب المان‌ها معکوس شود.

#### Scenario: RTL layout
- **WHEN** Toast در محیط RTL نمایش داده شود
- **THEN** dismiss button سمت راست و آیکن سمت چپ قرار گیرد
- **AND** متن از سمت راست تراز شود

#### Scenario: LTR layout
- **WHEN** Toast در محیط LTR نمایش داده شود
- **THEN** dismiss button سمت چپ و آیکن سمت راست قرار گیرد
- **AND** متن از سمت چپ تراز شود

### Requirement: Programmatic Toast Creation
کامپوننت Toast SHALL یک API جاوااسکریپتی (`Toast.show()`) برای ایجاد و نمایش Toast به صورت دینامیک ارائه دهد. این متد باید ساخت HTML، تنظیم آیکن پیش‌فرض، role دسترسی‌پذیری و تایمر را به صورت خودکار انجام دهد. در صورت نبود container، باید به صورت خودکار ساخته شود.

#### Scenario: Show toast with Toast.show()
- **WHEN** توسعه‌دهنده `Toast.show({ variant: 'success', title: 'عنوان' })` را فراخوانی کند
- **THEN** یک Toast با واریانت مشخص شده ساخته و نمایش داده شود
- **AND** آیکن پیش‌فرض واریانت و role صحیح به صورت خودکار تنظیم شود
- **AND** المان Toast ساخته شده بازگردانده شود

#### Scenario: Auto-create container
- **WHEN** `Toast.show()` فراخوانی شود و هیچ container‌ای وجود نداشته باشد
- **THEN** یک container با `id="toast-container"` به صورت خودکار ساخته و به body اضافه شود

#### Scenario: Custom duration via API
- **WHEN** `Toast.show({ variant: 'warning', title: 'هشدار', duration: 3000 })` فراخوانی شود
- **THEN** تایمر Toast باید 3 ثانیه باشد

#### Scenario: Optional description
- **WHEN** `Toast.show()` بدون `description` فراخوانی شود
- **THEN** Toast فقط با عنوان و بدون فضای خالی اضافی نمایش داده شود

### Requirement: Behavior Notes
Toast SHALL بتواند همزمان چند نمونه فعال داشته باشد. ترتیب نمایش (stacking) و محل نمایش (top/bottom، left/right) خارج از محدوده این کامپوننت است. انیمیشن ورود و خروج Toast (در صورت وجود) نباید با تایمر تداخل داشته باشد.

#### Scenario: Multiple toast instances
- **WHEN** چندین Toast همزمان فعال باشند
- **THEN** هر Toast مستقل عمل کند (تایمر و dismiss جداگانه)

#### Scenario: Stacking out of scope
- **WHEN** چندین Toast همزمان نمایش داده شوند
- **THEN** مدیریت موقعیت و ترتیب توسط سیستم بالادستی انجام شود (خارج از scope کامپوننت)
