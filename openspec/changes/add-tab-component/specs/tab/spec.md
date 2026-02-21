## ADDED Requirements

### Requirement: Tab Purpose and Description
کامپوننت Tab SHALL برای سوئیچ بین چند نمای هم‌سطح داخل یک صفحه استفاده شود — بدون اینکه کاربر از صفحه خارج شود. هر گروه تب شامل لیست تب‌ها (tab list) و پنل‌های محتوا (tab panels) است. تب فعال با ظاهر متمایز مشخص شود و پنل مرتبط نمایش یابد.

#### Scenario: Tab display
- **WHEN** کامپوننت تب رندر شود
- **THEN** لیست تب‌ها در یک نوار افقی با ارتفاع 48px نمایش یابد
- **AND** تب فعال با ظاهر متمایز مشخص شود
- **AND** پنل مرتبط با تب فعال نمایش یابد
- **AND** پنل‌های دیگر مخفی باشند

#### Scenario: Tab switch
- **WHEN** کاربر روی یک تب غیرفعال کلیک کند
- **THEN** آن تب فعال شود
- **AND** پنل مرتبط نمایش یابد
- **AND** تب و پنل قبلی غیرفعال شوند

### Requirement: Tab List Container
کامپوننت Tab SHALL دارای container (نوار تب) با ارتفاع 48px، padding افقی 24px، gap 12px و border-radius 8px باشد. چینش آیتم‌ها به صورت پیش‌فرض `justify-end` (تراز به سمت شروع در RTL) باشد.

#### Scenario: Container appearance
- **WHEN** نوار تب رندر شود
- **THEN** ارتفاع 48px داشته باشد
- **AND** padding افقی 24px و gap 12px بین آیتم‌ها باشد
- **AND** border-radius 8px اعمال شود

#### Scenario: Container alignment
- **WHEN** نوار تب نوع underline یا filled رندر شود
- **THEN** آیتم‌ها با `justify-end` چیده شوند (سمت شروع در RTL)

### Requirement: Underline Variant (Default)
کامپوننت Tab SHALL در نوع پیش‌فرض (Underline) دارای container با پس‌زمینه سفید (#ffffff) باشد. تب فعال با خط زیر 2px سبز (#26a88c)، فونت Medium (500) و رنگ #222323 نمایش یابد. تب غیرفعال با فونت Regular (400) و رنگ #59595a نمایش یابد. تب فعال تمام ارتفاع container را بگیرد تا خط زیر در پایین container قرار گیرد.

#### Scenario: Underline container
- **WHEN** تب نوع underline رندر شود
- **THEN** container پس‌زمینه سفید (#ffffff) داشته باشد
- **AND** border-radius 8px باشد

#### Scenario: Underline active tab
- **WHEN** تب در نوع underline فعال باشد
- **THEN** خط زیر 2px با رنگ #26a88c (border-bottom) نمایش یابد
- **AND** فونت Medium (500) با سایز 13px و line-height 1.3 باشد
- **AND** رنگ متن #222323 باشد
- **AND** تمام ارتفاع container را بگیرد

#### Scenario: Underline inactive tab
- **WHEN** تب در نوع underline غیرفعال باشد
- **THEN** بدون خط زیر باشد
- **AND** فونت Regular (400) با سایز 13px و line-height 1.3 باشد
- **AND** رنگ متن #59595a باشد

### Requirement: Filled Variant
کامپوننت Tab SHALL از نوع Filled (Pill) با کلاس `tab--filled` پشتیبانی کند. Container بدون پس‌زمینه سفید باشد. تب فعال با پس‌زمینه سبز (#26a88c)، رنگ متن سفید، ارتفاع 38px و border-radius 8px نمایش یابد. تب غیرفعال تمام ارتفاع container را بگیرد.

#### Scenario: Filled container
- **WHEN** تب با کلاس `tab--filled` رندر شود
- **THEN** container بدون پس‌زمینه سفید باشد (شفاف)

#### Scenario: Filled active tab
- **WHEN** تب در نوع filled فعال باشد
- **THEN** پس‌زمینه #26a88c داشته باشد
- **AND** رنگ متن سفید (#ffffff) باشد
- **AND** فونت Medium (500) با سایز 13px باشد
- **AND** ارتفاع 38px و border-radius 8px باشد

#### Scenario: Filled inactive tab
- **WHEN** تب در نوع filled غیرفعال باشد
- **THEN** بدون پس‌زمینه باشد
- **AND** فونت Regular (400) و رنگ متن #59595a باشد
- **AND** تمام ارتفاع container را بگیرد

### Requirement: Icon Support
کامپوننت Tab SHALL از نمایش آیکن SVG در کنار متن تب پشتیبانی کند. آیکن با سایز 20px (در باکس 24px) و فاصله 10px از متن قرار گیرد. رنگ آیکن مطابق رنگ متن (فعال/غیرفعال) تغییر کند. در نوع آیکن‌دار، چینش container به `justify-center` تغییر یابد.

#### Scenario: Tab with icon
- **WHEN** تب دارای آیکن باشد
- **THEN** آیکن با سایز 20px نمایش یابد
- **AND** فاصله 10px (gap) بین آیکن و متن باشد
- **AND** رنگ آیکن مطابق رنگ متن تب باشد

#### Scenario: Icon tab container alignment
- **WHEN** تب‌ها دارای آیکن باشند
- **THEN** چینش container به `justify-center` (وسط‌چین) تغییر یابد

#### Scenario: Active tab icon color
- **WHEN** تب دارای آیکن فعال باشد
- **THEN** رنگ آیکن #222323 باشد

#### Scenario: Inactive tab icon color
- **WHEN** تب دارای آیکن غیرفعال باشد
- **THEN** رنگ آیکن #59595a باشد

### Requirement: Badge Support
کامپوننت Tab SHALL از نمایش badge عددی (مثلا "۳") در کنار متن تب فعال پشتیبانی کند. Badge با سایز 15×15px و فاصله 5px از متن قرار گیرد.

#### Scenario: Tab with badge
- **WHEN** تب فعال دارای badge باشد
- **THEN** badge با سایز 15×15px نمایش یابد
- **AND** فاصله 5px (gap) بین badge و متن باشد

#### Scenario: Badge color
- **WHEN** badge در تب فعال نمایش یابد
- **THEN** رنگ badge مطابق رنگ متن فعال باشد

### Requirement: Tab Items
هر آیتم تب SHALL دارای padding افقی 12px و عمودی 16px باشد. فونت Peyda(FaNum) با سایز 13px و line-height 1.3 استفاده شود. آیتم‌ها cursor pointer داشته باشند.

#### Scenario: Tab item spacing
- **WHEN** آیتم تب رندر شود
- **THEN** padding افقی 12px و عمودی 16px داشته باشد
- **AND** فونت Peyda(FaNum) با سایز 13px و line-height 1.3 باشد

#### Scenario: Tab item interaction
- **WHEN** کاربر ماوس را روی آیتم تب ببرد
- **THEN** cursor pointer نمایش یابد

### Requirement: Tab Panels
کامپوننت Tab SHALL از پنل‌های محتوا پشتیبانی کند. هر تب به یک پنل محتوا متصل شود. فقط پنل مرتبط با تب فعال نمایش یابد.

#### Scenario: Panel display
- **WHEN** تبی فعال باشد
- **THEN** پنل مرتبط با آن تب نمایش یابد
- **AND** سایر پنل‌ها مخفی باشند

#### Scenario: Panel switch
- **WHEN** کاربر تب دیگری را فعال کند
- **THEN** پنل قبلی مخفی شود
- **AND** پنل جدید نمایش یابد

### Requirement: Keyboard Support
کامپوننت Tab SHALL از keyboard navigation پشتیبانی کند. Arrow keys برای جابجایی بین تب‌ها، Home/End برای اولین/آخرین تب و Enter/Space برای فعال‌سازی.

#### Scenario: Arrow key navigation
- **WHEN** فوکوس روی تب باشد و کاربر Arrow Right/Left بزند
- **THEN** فوکوس به تب بعدی/قبلی منتقل شود

#### Scenario: Home and End keys
- **WHEN** فوکوس روی تب باشد و کاربر Home بزند
- **THEN** فوکوس به اولین تب منتقل شود
- **WHEN** کاربر End بزند
- **THEN** فوکوس به آخرین تب منتقل شود

#### Scenario: Enter and Space activation
- **WHEN** فوکوس روی تب غیرفعال باشد و کاربر Enter یا Space بزند
- **THEN** آن تب فعال شود

### Requirement: JavaScript API
کامپوننت Tab SHALL دارای API عمومی برای کنترل تب‌ها باشد. `Tab.activate(groupId, index)` برای فعال کردن تب، `Tab.onChange(groupId, fn)` برای callback تغییر و `Tab.initAll()` برای فعال‌سازی خودکار.

#### Scenario: Activate tab by index
- **WHEN** `Tab.activate('my-tabs', 1)` فراخوانی شود
- **THEN** تب دوم (index 1) در گروه `my-tabs` فعال شود

#### Scenario: OnChange callback
- **WHEN** `Tab.onChange('my-tabs', fn)` تنظیم شود و تب تغییر کند
- **THEN** تابع callback با index تب جدید فراخوانی شود

#### Scenario: Auto initialization
- **WHEN** صفحه بارگذاری شود (DOMContentLoaded)
- **THEN** تمام کامپوننت‌های تب به صورت خودکار فعال شوند

### Requirement: Accessibility
کامپوننت Tab SHALL از WAI-ARIA Tabs pattern پشتیبانی کند. Container باید `role="tablist"` داشته باشد. هر آیتم باید `role="tab"` و `aria-selected` داشته باشد. هر پنل باید `role="tabpanel"` داشته باشد. اتصال با `aria-controls` و `aria-labelledby` برقرار شود.

#### Scenario: ARIA attributes on tablist
- **WHEN** لیست تب رندر شود
- **THEN** دارای `role="tablist"` باشد

#### Scenario: ARIA attributes on tabs
- **WHEN** تب رندر شود
- **THEN** دارای `role="tab"` باشد
- **AND** تب فعال `aria-selected="true"` و تب غیرفعال `aria-selected="false"` داشته باشد
- **AND** تب فعال `tabindex="0"` و تب غیرفعال `tabindex="-1"` داشته باشد

#### Scenario: ARIA attributes on panels
- **WHEN** پنل رندر شود
- **THEN** دارای `role="tabpanel"` باشد
- **AND** `aria-labelledby` به id تب مرتبط اشاره کند

### Requirement: RTL Support
کامپوننت Tab SHALL از RTL پشتیبانی کامل داشته باشد. در حالت RTL، آیتم‌ها از راست به چپ چیده شوند. آیکن‌ها بعد از متن (سمت چپ در RTL) و badge‌ها قبل از متن در HTML (سمت چپ متن در RTL) قرار گیرند.

#### Scenario: RTL tab layout
- **WHEN** تب در محیط RTL رندر شود
- **THEN** آیتم‌ها از راست به چپ چیده شوند
- **AND** آیکن‌ها در سمت صحیح قرار گیرند
- **AND** badge‌ها در سمت صحیح قرار گیرند
