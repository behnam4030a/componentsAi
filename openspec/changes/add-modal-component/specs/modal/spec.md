## ADDED Requirements

### Requirement: Modal Purpose and Description
کامپوننت Modal SHALL برای نمایش محتوای فرم، اطلاعات و عملیات‌هایی که نیاز به تمرکز کاربر دارند استفاده شود. مودال شامل overlay (پس‌زمینه تیره)، header (هدر تیره) و body (بدنه سفید) است. مودال دارای نسخه دسکتاپ (slide-in از راست) و موبایل (slide-up از پایین) با رفتارهای متفاوت است.

#### Scenario: Modal display
- **WHEN** مودال با `Modal.open(id)` باز شود
- **THEN** overlay با گرادیانت تیره نمایش یابد
- **AND** container مودال با انیمیشن وارد صفحه شود
- **AND** header تیره با عنوان و آیکن نمایش یابد
- **AND** body سفید با محتوا نمایش یابد

#### Scenario: Modal close
- **WHEN** مودال با `Modal.close(id)` بسته شود
- **THEN** container با انیمیشن از صفحه خارج شود
- **AND** overlay محو شود
- **AND** فوکوس به المان قبلی بازگردد

### Requirement: Desktop Layout
کامپوننت Modal در نسخه دسکتاپ (عرض بیشتر از 768px) SHALL از سمت راست صفحه وارد شود (slide-in from right). عرض پیش‌فرض 500px، ارتفاع تمام viewport با فاصله 16px از بالا و پایین. Container دارای padding 4px، border-radius 8px و shadow سمت چپ باشد.

#### Scenario: Desktop slide-in from right
- **WHEN** مودال در عرض صفحه بیشتر از 768px باز شود
- **THEN** container از سمت راست صفحه با انیمیشن slide-in وارد شود
- **AND** عرض container 500px باشد (سایز پیش‌فرض)
- **AND** ارتفاع container تمام viewport منهای 32px (16px بالا + 16px پایین) باشد

#### Scenario: Desktop container styling
- **WHEN** مودال دسکتاپ نمایش یابد
- **THEN** container دارای padding 4px باشد
- **AND** border-radius 8px اعمال شود
- **AND** shadow: -3px 0px 5px 0px rgba(0,0,0,0.1) نمایش یابد

#### Scenario: Desktop header
- **WHEN** هدر مودال دسکتاپ نمایش یابد
- **THEN** padding یکنواخت 24px داشته باشد
- **AND** عنوان با فونت SemiBold (600) و سایز 20px نمایش یابد

#### Scenario: Desktop body
- **WHEN** بدنه مودال دسکتاپ نمایش یابد
- **THEN** padding 24px داشته باشد

### Requirement: Mobile Layout
کامپوننت Modal در نسخه موبایل (عرض کمتر از 768px) SHALL از سمت پایین صفحه وارد شود (slide-up from bottom). عرض 100% صفحه و ارتفاع بسته به حجم محتوا باشد. هدر و بدنه دارای padding متفاوت با نسخه دسکتاپ هستند.

#### Scenario: Mobile slide-up from bottom
- **WHEN** مودال در عرض صفحه کمتر از 768px باز شود
- **THEN** container از سمت پایین صفحه با انیمیشن slide-up وارد شود
- **AND** عرض container 100% باشد
- **AND** ارتفاع container بسته به حجم محتوا باشد

#### Scenario: Mobile header
- **WHEN** هدر مودال موبایل نمایش یابد
- **THEN** padding افقی 16px و عمودی 24px داشته باشد
- **AND** عنوان با فونت Medium (500) و سایز 18px نمایش یابد

#### Scenario: Mobile body
- **WHEN** بدنه مودال موبایل نمایش یابد
- **THEN** padding 16px داشته باشد

### Requirement: Modal Header
کامپوننت Modal SHALL دارای هدر تیره با پس‌زمینه #222323 باشد. هدر شامل دکمه بستن (×)، عنوان و آیکن‌هولدر است. دکمه بستن سایز 24px در سمت چپ هدر (RTL) قرار گیرد. آیکن‌هولدر مربع 54px با پس‌زمینه #2c2d2d و border #454546 باشد.

#### Scenario: Header appearance
- **WHEN** هدر مودال نمایش یابد
- **THEN** پس‌زمینه #222323 با متن سفید (#ffffff) باشد
- **AND** دکمه بستن (×) با سایز 24px در سمت چپ (RTL) نمایش یابد
- **AND** عنوان و آیکن‌هولدر نمایش یابد

#### Scenario: Icon holder
- **WHEN** آیکن‌هولدر در هدر نمایش یابد
- **THEN** مربع 54px با پس‌زمینه #2c2d2d باشد
- **AND** border با رنگ #454546 و عرض 1px داشته باشد
- **AND** border-radius 8px باشد
- **AND** آیکن داخلی سایز 26px باشد

#### Scenario: Close button click
- **WHEN** کاربر روی دکمه بستن (×) کلیک کند
- **THEN** مودال بسته شود

### Requirement: Modal Body
کامپوننت Modal SHALL دارای بدنه سفید با پس‌زمینه #ffffff باشد. بدنه شامل محتوا (فرم‌ها، متن و ...) و دکمه‌های عملیاتی (actions) است. بدنه در صورت بلند بودن محتوا اسکرول شود.

#### Scenario: Body appearance
- **WHEN** بدنه مودال نمایش یابد
- **THEN** پس‌زمینه #ffffff باشد
- **AND** محتوا در بخش `.modal__content` و دکمه‌ها در `.modal__actions` قرار گیرند

#### Scenario: Body scroll
- **WHEN** محتوای مودال بیشتر از ارتفاع مجاز باشد
- **THEN** بخش `.modal__content` اسکرول شود
- **AND** هدر و دکمه‌های عملیاتی ثابت بمانند

#### Scenario: Action button
- **WHEN** دکمه عملیاتی در پایین بدنه نمایش یابد
- **THEN** دکمه با عرض 100% نمایش یابد

### Requirement: Overlay
کامپوننت Modal SHALL دارای overlay (پس‌زمینه تیره) باشد. Overlay با گرادیانت از rgba(0,0,0,0.05) تا rgba(34,35,35,0.3) نمایش یابد. کلیک روی overlay مودال را می‌بندد.

#### Scenario: Overlay appearance
- **WHEN** مودال باز شود
- **THEN** overlay با گرادیانت تیره نمایش یابد
- **AND** تمام صفحه پشت مودال را بپوشاند

#### Scenario: Overlay click to close
- **WHEN** کاربر روی overlay کلیک کند
- **THEN** مودال بسته شود

### Requirement: Size Variants
کامپوننت Modal SHALL از 3 سایز پشتیبانی کند: کوچک (Small — 400px)، متوسط (Medium — 500px، پیش‌فرض) و بزرگ (Large — 600px). در موبایل هر سه سایز عرض 100% می‌شوند.

#### Scenario: Small size
- **WHEN** مودال با کلاس `modal--sm` ایجاد شود
- **THEN** عرض container در دسکتاپ 400px باشد

#### Scenario: Medium size (default)
- **WHEN** مودال بدون modifier سایز یا با `modal--md` ایجاد شود
- **THEN** عرض container در دسکتاپ 500px باشد

#### Scenario: Large size
- **WHEN** مودال با کلاس `modal--lg` ایجاد شود
- **THEN** عرض container در دسکتاپ 600px باشد

#### Scenario: Mobile size override
- **WHEN** مودال در عرض صفحه کمتر از 768px باشد
- **THEN** عرض container 100% شود صرف‌نظر از سایز تعیین شده

### Requirement: Animation
کامپوننت Modal SHALL دارای انیمیشن‌های نرم هنگام باز و بسته شدن باشد. در دسکتاپ slide-in/slide-out از راست و در موبایل slide-up/slide-down از پایین. Overlay با fade-in/fade-out نمایش یابد.

#### Scenario: Desktop open animation
- **WHEN** مودال در دسکتاپ باز شود
- **THEN** container با انیمیشن slide-in از سمت راست وارد شود
- **AND** overlay با fade-in نمایش یابد

#### Scenario: Desktop close animation
- **WHEN** مودال در دسکتاپ بسته شود
- **THEN** container با انیمیشن slide-out به سمت راست خارج شود
- **AND** overlay با fade-out محو شود

#### Scenario: Mobile open animation
- **WHEN** مودال در موبایل باز شود
- **THEN** container با انیمیشن slide-up از پایین وارد شود

#### Scenario: Mobile close animation
- **WHEN** مودال در موبایل بسته شود
- **THEN** container با انیمیشن slide-down به پایین خارج شود

### Requirement: Keyboard Support
کامپوننت Modal SHALL از keyboard navigation پشتیبانی کند. کلید Escape مودال را می‌بندد.

#### Scenario: Escape to close
- **WHEN** مودال باز باشد و کاربر کلید Escape بزند
- **THEN** مودال بسته شود

### Requirement: Focus Trap
کامپوننت Modal SHALL فوکوس را در مودال باز محدود کند. Tab و Shift+Tab بین المان‌های focusable داخل مودال بچرخد. فوکوس اولیه روی اولین المان focusable قرار گیرد و هنگام بسته شدن به المان trigger بازگردد.

#### Scenario: Focus containment
- **WHEN** مودال باز باشد و کاربر Tab بزند
- **THEN** فوکوس فقط بین المان‌های focusable داخل مودال بچرخد
- **AND** فوکوس از مودال خارج نشود

#### Scenario: Initial focus
- **WHEN** مودال باز شود
- **THEN** فوکوس روی اولین المان focusable داخل مودال قرار گیرد

#### Scenario: Focus restore
- **WHEN** مودال بسته شود
- **THEN** فوکوس به المانی که قبل از باز شدن مودال فوکوس داشت بازگردد

### Requirement: Body Scroll Lock
کامپوننت Modal SHALL هنگام باز بودن، اسکرول صفحه پشت مودال را قفل کند. هنگام بسته شدن اسکرول آزاد شود.

#### Scenario: Scroll lock on open
- **WHEN** مودال باز شود
- **THEN** اسکرول صفحه (body) قفل شود
- **AND** scrollbar width مدیریت شود (جلوگیری از layout shift)

#### Scenario: Scroll unlock on close
- **WHEN** مودال بسته شود
- **THEN** اسکرول صفحه آزاد شود

### Requirement: Responsive Behavior
کامپوننت Modal SHALL بر اساس عرض صفحه بین نسخه دسکتاپ و موبایل تغییر کند. Breakpoint در عرض 768px تنظیم شود.

#### Scenario: Desktop mode
- **WHEN** عرض صفحه بیشتر از 768px باشد
- **THEN** مودال نسخه دسکتاپ (slide-in از راست) نمایش یابد

#### Scenario: Mobile mode
- **WHEN** عرض صفحه کمتر از 768px باشد
- **THEN** مودال نسخه موبایل (slide-up از پایین) نمایش یابد

### Requirement: JavaScript API
کامپوننت Modal SHALL دارای API عمومی برای کنترل مودال‌ها باشد. `Modal.open(id)` برای باز کردن، `Modal.close(id)` برای بستن و `Modal.closeAll()` برای بستن همه مودال‌ها.

#### Scenario: Open modal by ID
- **WHEN** `Modal.open('my-modal')` فراخوانی شود
- **THEN** مودال با id `my-modal` باز شود

#### Scenario: Close modal by ID
- **WHEN** `Modal.close('my-modal')` فراخوانی شود
- **THEN** مودال با id `my-modal` بسته شود

#### Scenario: Close all modals
- **WHEN** `Modal.closeAll()` فراخوانی شود
- **THEN** تمام مودال‌های باز بسته شوند

### Requirement: Accessibility
کامپوننت Modal SHALL از WAI-ARIA Dialog pattern پشتیبانی کند. Container باید `role="dialog"`, `aria-modal="true"` و `aria-labelledby` (اشاره به عنوان) داشته باشد. دکمه بستن باید `aria-label="بستن"` داشته باشد.

#### Scenario: ARIA attributes on container
- **WHEN** مودال رندر شود
- **THEN** container دارای `role="dialog"` باشد
- **AND** `aria-modal="true"` داشته باشد
- **AND** `aria-labelledby` به id عنوان مودال اشاره کند

#### Scenario: Close button accessibility
- **WHEN** دکمه بستن رندر شود
- **THEN** دارای `aria-label="بستن"` باشد
- **AND** با کیبورد قابل فوکوس و فعال‌سازی باشد

### Requirement: RTL Support
کامپوننت Modal SHALL از RTL پشتیبانی کامل داشته باشد. در حالت RTL، مودال دسکتاپ از سمت راست وارد شود، دکمه بستن سمت چپ هدر قرار گیرد و متن فارسی به درستی تراز شود.

#### Scenario: RTL desktop layout
- **WHEN** مودال در محیط RTL در دسکتاپ باز شود
- **THEN** container از سمت راست صفحه اسلاید شود
- **AND** دکمه بستن سمت چپ هدر باشد
- **AND** متن و محتوا از راست به چپ تراز شوند

#### Scenario: RTL mobile layout
- **WHEN** مودال در محیط RTL در موبایل باز شود
- **THEN** container از پایین صفحه اسلاید شود
- **AND** متن و محتوا از راست به چپ تراز شوند

### Requirement: Centered Variant
کامپوننت Modal SHALL از نوع وسط صفحه (Centered) با کلاس `modal--centered` پشتیبانی کند. این نوع مودال در وسط صفحه ظاهر می‌شود، ارتفاع بر اساس حجم محتوا تعیین می‌شود و با انیمیشن scale/fade باز و بسته می‌شود. Overlay گرادیانت از بالا به پایین دارد.

#### Scenario: Centered display
- **WHEN** مودال با کلاس `modal--centered` باز شود
- **THEN** container در وسط صفحه نمایش یابد
- **AND** ارتفاع بر اساس محتوا تعیین شود (حداکثر viewport منهای 32px)
- **AND** عرض مطابق سایز تعریف‌شده باشد (پیش‌فرض 500px)

#### Scenario: Centered animation
- **WHEN** مودال centered باز شود
- **THEN** container با انیمیشن scale(0.95→1) و fade-in ظاهر شود
- **AND** overlay با fade-in و گرادیانت بالا به پایین نمایش یابد

#### Scenario: Centered close animation
- **WHEN** مودال centered بسته شود
- **THEN** container با انیمیشن scale(1→0.95) و fade-out ناپدید شود

#### Scenario: Centered mobile
- **WHEN** مودال centered در موبایل باز شود
- **THEN** container در وسط صفحه نمایش یابد
- **AND** عرض حداکثر calc(100% - 16px) باشد

### Requirement: Header Subtitle
کامپوننت Modal SHALL از زیرعنوان (subtitle) در هدر پشتیبانی کند. زیرعنوان زیر عنوان اصلی با فونت Regular 14px و رنگ #cfd0d2 نمایش یابد. عنوان و زیرعنوان باید در `modal__title-wrap` قرار گیرند.

#### Scenario: Subtitle display
- **WHEN** هدر مودال دارای `modal__subtitle` باشد
- **THEN** زیرعنوان زیر عنوان اصلی با فونت 14px و رنگ #cfd0d2 نمایش یابد
- **AND** عنوان و زیرعنوان در `modal__title-wrap` تراز شوند

#### Scenario: Subtitle mobile
- **WHEN** زیرعنوان در موبایل نمایش یابد
- **THEN** فاصله 4px بین عنوان و زیرعنوان باشد
- **AND** line-height زیرعنوان 1.5 باشد

### Requirement: Expanded Panel
کامپوننت Modal SHALL از پنل جانبی (Expanded Panel) پشتیبانی کند. پنل جانبی در سمت چپ مودال اصلی (در RTL) نمایش یابد و برای انتخاب آیتم‌ها از لیست (مثلا آزمون یا گروه) استفاده شود. با `Modal.openPanel(id)` باز و با `Modal.closePanel(id)` بسته شود.

#### Scenario: Panel open
- **WHEN** `Modal.openPanel('panel-id')` فراخوانی شود
- **THEN** پنل جانبی با انیمیشن slide-in از سمت مودال اصلی ظاهر شود

#### Scenario: Panel close
- **WHEN** `Modal.closePanel('panel-id')` فراخوانی شود
- **THEN** پنل جانبی با انیمیشن بسته شود

#### Scenario: Panel auto-close
- **WHEN** مودال اصلی بسته شود
- **THEN** تمام پنل‌های جانبی باز به صورت خودکار بسته شوند
