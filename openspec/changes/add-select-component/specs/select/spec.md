## ADDED Requirements

### Requirement: Select Purpose and Description
کامپوننت Select SHALL برای انتخاب مقدار از میان گزینه‌های موجود استفاده شود. سلکت‌ها یک انتخاب را مشخص می‌کنند و معمولاً وضعیت یا رفتار بعدی سیستم را تعیین می‌کنند. Select شامل یک trigger (ناحیه کلیک‌پذیر) و یک dropdown (لیست آیتم‌ها) است.

#### Scenario: Select basic display
- **WHEN** کامپوننت Select در صفحه رندر شود
- **THEN** trigger با placeholder یا مقدار انتخاب شده نمایش داده شود
- **AND** dropdown در حالت پیش‌فرض بسته باشد

#### Scenario: Select dropdown toggle
- **WHEN** کاربر روی trigger کلیک کند
- **THEN** dropdown باز شود و لیست آیتم‌ها نمایش داده شود
- **AND** trigger به حالت active تغییر کند

### Requirement: Select Types
کامپوننت Select SHALL از 4 نوع پشتیبانی کند: Basic، Primary (Single Select)، Multiple و Tagify. هر نوع با modifier class مشخص می‌شود و رفتار انتخاب و نمایش مقدار را تعیین می‌کند.

#### Scenario: Basic type
- **WHEN** Select با کلاس `select--basic` ایجاد شود
- **THEN** مقدار انتخاب شده به صورت متن ساده در trigger نمایش یابد
- **AND** dropdown دارای فیلد جستجو و اسکرول‌بار سفارشی باشد
- **AND** فقط یک آیتم قابل انتخاب باشد

#### Scenario: Primary type (Single Select)
- **WHEN** Select با کلاس `select--primary` ایجاد شود
- **THEN** مقدار انتخاب شده به صورت تگ بنفش در trigger نمایش یابد
- **AND** تگ دارای آیکن حذف (close) باشد
- **AND** فقط یک آیتم قابل انتخاب باشد
- **AND** dropdown بدون فیلد جستجو باشد

#### Scenario: Multiple type
- **WHEN** Select با کلاس `select--multiple` ایجاد شود
- **THEN** مقادیر انتخاب شده به صورت تگ‌های خاکستری در trigger نمایش یابند
- **AND** هر تگ دارای آیکن حذف (close-remove) باشد
- **AND** چند آیتم قابل انتخاب باشد
- **AND** dropdown بدون فیلد جستجو باشد

#### Scenario: Tagify type
- **WHEN** Select با کلاس `select--tagify` ایجاد شود
- **THEN** مقادیر انتخاب شده به صورت تگ‌های خاکستری در trigger نمایش یابند
- **AND** هر تگ دارای آیکن حذف (close-square) باشد
- **AND** چند آیتم قابل انتخاب باشد

### Requirement: Select States
کامپوننت Select SHALL از 4 وضعیت پشتیبانی کند: Rest، Active/Focused، Selected و Disabled. هر وضعیت ظاهر بصری متفاوتی دارد.

#### Scenario: Rest state
- **WHEN** Select در حالت پیش‌فرض باشد
- **THEN** border با رنگ خاکستری (#e2e4e6) نمایش یابد
- **AND** متن placeholder با رنگ #59595a نمایش یابد

#### Scenario: Active/Focused state
- **WHEN** Select فوکوس دریافت کند یا dropdown باز شود
- **THEN** border با رنگ بنفش (#8a38f5) نمایش یابد
- **AND** shadow بنفش (0px 0px 4px 0px rgba(138,56,245,0.5)) اعمال شود

#### Scenario: Selected state
- **WHEN** کاربر یک یا چند آیتم را انتخاب کند
- **THEN** مقدار انتخاب شده در trigger نمایش یابد (متن یا تگ بر اساس نوع)

#### Scenario: Disabled state
- **WHEN** Select با کلاس `select--disabled` ایجاد شود
- **THEN** پس‌زمینه خاکستری (#f1f3f5) و متن کم‌رنگ (#bbbcbe) نمایش یابد
- **AND** border با رنگ #dddfe1 نمایش یابد
- **AND** هیچ تعاملی (کلیک، hover) ممکن نباشد

### Requirement: Dropdown Panel
کامپوننت Select SHALL دارای یک dropdown panel برای نمایش لیست آیتم‌ها باشد. Dropdown با position absolute خارج از flow اصلی قرار گیرد و shadow مخصوص داشته باشد. آیتم انتخاب شده با پس‌زمینه بنفش روشن و متن بنفش مشخص شود.

#### Scenario: Dropdown appearance
- **WHEN** dropdown باز شود
- **THEN** با border-radius 8px و shadow (1px 4px 5.8px 0px rgba(93,93,93,0.09)) نمایش یابد
- **AND** padding 8px داشته باشد
- **AND** پس‌زمینه سفید باشد

#### Scenario: Selected item highlight
- **WHEN** آیتمی در لیست انتخاب شده باشد
- **THEN** پس‌زمینه بنفش روشن (rgba(138,56,245,0.05)) و متن بنفش (#8a38f5) نمایش یابد

#### Scenario: Item hover
- **WHEN** کاربر روی آیتم hover کند
- **THEN** تغییر بصری مناسب (highlight) نمایش یابد

#### Scenario: Close dropdown on outside click
- **WHEN** کاربر خارج از کامپوننت Select کلیک کند
- **THEN** dropdown بسته شود

### Requirement: Search Functionality
کامپوننت Select نوع Basic SHALL دارای فیلد جستجو در بالای dropdown باشد. جستجو آیتم‌ها را بر اساس متن فیلتر می‌کند. فیلد جستجو با height 32px، border-radius 4px و border خاکستری (#cacbcd) نمایش یابد.

#### Scenario: Search filter
- **WHEN** کاربر متنی در فیلد جستجو تایپ کند
- **THEN** فقط آیتم‌هایی که شامل متن جستجو هستند نمایش یابند
- **AND** سایر آیتم‌ها مخفی شوند

#### Scenario: Search auto-focus
- **WHEN** dropdown نوع Basic باز شود
- **THEN** فوکوس به صورت خودکار روی فیلد جستجو قرار گیرد

#### Scenario: Search clear on close
- **WHEN** dropdown بسته شود
- **THEN** متن فیلد جستجو پاک شود
- **AND** تمام آیتم‌ها مجدداً نمایش یابند

### Requirement: Tag System
کامپوننت Select SHALL از دو نوع تگ برای نمایش مقادیر انتخاب شده پشتیبانی کند. تگ تکی (Primary) با پس‌زمینه بنفش روشن و متن بنفش، و تگ چندگانه (Multiple/Tagify) با پس‌زمینه خاکستری روشن و متن خاکستری نمایش یابد. هر تگ دارای آیکن حذف باشد.

#### Scenario: Single tag (Primary)
- **WHEN** آیتمی در Select نوع Primary انتخاب شود
- **THEN** تگ با پس‌زمینه rgba(138,56,245,0.05) و متن #8a38f5 نمایش یابد
- **AND** آیکن حذف (close) روی تگ قابل کلیک باشد

#### Scenario: Multiple tags
- **WHEN** آیتم‌هایی در Select نوع Multiple انتخاب شوند
- **THEN** هر آیتم به صورت تگ با پس‌زمینه rgba(89,89,90,0.05) و متن #59595a نمایش یابد
- **AND** آیکن حذف (close-remove) روی هر تگ قابل کلیک باشد

#### Scenario: Tag removal
- **WHEN** کاربر روی آیکن حذف تگ کلیک کند
- **THEN** تگ از trigger حذف شود
- **AND** آیتم مربوطه از حالت انتخاب خارج شود

### Requirement: Size Variants
کامپوننت Select SHALL از 3 اندازه پشتیبانی کند: کوچک (Small)، متوسط (Medium) و بزرگ (Large). اندازه پیش‌فرض متوسط است. تغییر اندازه بر ارتفاع trigger، اندازه فونت و padding تأثیر می‌گذارد.

#### Scenario: Small size
- **WHEN** Select با کلاس `select--sm` ایجاد شود
- **THEN** trigger با ارتفاع کمتر و فونت کوچک‌تر نمایش یابد

#### Scenario: Medium size (default)
- **WHEN** Select بدون modifier اندازه یا با کلاس `select--md` ایجاد شود
- **THEN** trigger با ارتفاع 45px نمایش یابد

#### Scenario: Large size
- **WHEN** Select با کلاس `select--lg` ایجاد شود
- **THEN** trigger با ارتفاع بیشتر و فونت بزرگ‌تر نمایش یابد

### Requirement: Select Layout and Dimensions
کامپوننت Select SHALL با عرض 320px، ارتفاع trigger 45px (Medium)، border-radius 8px نمایش یابد. آیتم‌ها با فونت 14px، وزن 400 و line-height 2 نمایش یابند. Chevron icon سایز 16px و close icon تگ سایز 12px باشد.

#### Scenario: Select dimensions
- **WHEN** Select نمایش داده شود
- **THEN** عرض 320px باشد
- **AND** ارتفاع trigger در حالت Medium برابر 45px باشد
- **AND** border-radius 8px باشد

#### Scenario: Item typography
- **WHEN** آیتم‌ها در dropdown نمایش داده شوند
- **THEN** با فونت Peyda(FaNum)، سایز 14px، وزن 400 و line-height 2 نمایش یابند

#### Scenario: Icon sizes
- **WHEN** Select نمایش داده شود
- **THEN** آیکن chevron سایز 16px باشد
- **AND** آیکن حذف تگ سایز 12px باشد

### Requirement: Custom Scrollbar
کامپوننت Select نوع Basic SHALL دارای اسکرول‌بار سفارشی در dropdown باشد. اسکرول‌بار با عرض 5px و ارتفاع thumb 10px و رنگ #d9d9d9 نمایش یابد.

#### Scenario: Custom scrollbar in Basic
- **WHEN** لیست آیتم‌ها در نوع Basic بیشتر از ارتفاع مجاز باشد
- **THEN** اسکرول‌بار سفارشی با عرض 5px نمایش یابد
- **AND** رنگ thumb اسکرول‌بار #d9d9d9 باشد

### Requirement: Keyboard Navigation
کامپوننت Select SHALL از keyboard navigation کامل پشتیبانی کند. کاربر باید بتواند با Arrow keys بین آیتم‌ها حرکت کند، با Enter انتخاب کند، با Escape dropdown را ببندد و با Tab از کامپوننت خارج شود.

#### Scenario: Arrow key navigation
- **WHEN** dropdown باز باشد و کاربر Arrow Down بزند
- **THEN** آیتم بعدی highlight شود
- **WHEN** کاربر Arrow Up بزند
- **THEN** آیتم قبلی highlight شود

#### Scenario: Enter to select
- **WHEN** آیتمی highlight شده باشد و کاربر Enter بزند
- **THEN** آیتم انتخاب شود

#### Scenario: Escape to close
- **WHEN** dropdown باز باشد و کاربر Escape بزند
- **THEN** dropdown بسته شود

#### Scenario: Tab to exit
- **WHEN** کاربر Tab بزند
- **THEN** فوکوس از کامپوننت Select خارج شود
- **AND** dropdown بسته شود

### Requirement: Accessibility
کامپوننت Select SHALL از WAI-ARIA Listbox pattern پشتیبانی کند. trigger باید `aria-haspopup="listbox"` و `aria-expanded` داشته باشد. لیست آیتم‌ها با `role="listbox"` و هر آیتم با `role="option"` و `aria-selected` مشخص شود. در حالت multi-select، `aria-multiselectable="true"` اعمال شود.

#### Scenario: ARIA attributes on trigger
- **WHEN** Select رندر شود
- **THEN** trigger دارای `aria-haspopup="listbox"` باشد
- **AND** `aria-expanded="false"` در حالت بسته و `aria-expanded="true"` در حالت باز باشد

#### Scenario: ARIA attributes on list
- **WHEN** dropdown باز شود
- **THEN** لیست دارای `role="listbox"` باشد
- **AND** هر آیتم دارای `role="option"` باشد
- **AND** آیتم انتخاب شده دارای `aria-selected="true"` باشد

#### Scenario: Multi-select ARIA
- **WHEN** Select نوع Multiple یا Tagify باشد
- **THEN** لیست دارای `aria-multiselectable="true"` باشد

#### Scenario: Keyboard accessible
- **WHEN** کاربر با کیبورد navigate کند
- **THEN** تمام عملکردها (باز/بسته، انتخاب، حذف تگ) با کیبورد قابل دسترس باشند

### Requirement: RTL Support
کامپوننت Select SHALL از RTL پشتیبانی کامل داشته باشد. در حالت RTL، متن از سمت راست شروع شود، chevron سمت چپ و تگ‌ها سمت راست قرار گیرند. در صورت استفاده از `dir="ltr"`، ترتیب المان‌ها معکوس شود.

#### Scenario: RTL layout
- **WHEN** Select در محیط RTL نمایش داده شود
- **THEN** متن از سمت راست تراز شود
- **AND** chevron سمت چپ trigger قرار گیرد
- **AND** تگ‌ها از سمت راست چیده شوند

#### Scenario: LTR layout
- **WHEN** Select در محیط LTR نمایش داده شود
- **THEN** متن از سمت چپ تراز شود
- **AND** chevron سمت راست trigger قرار گیرد
