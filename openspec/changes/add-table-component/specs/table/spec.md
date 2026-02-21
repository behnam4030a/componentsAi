## ADDED Requirements

### Requirement: Table Purpose
جدول (Table) SHALL نمایش داده‌ی ساخت‌یافته در قالب ردیف و ستون را فراهم کند — ابزار اصلی برای مقایسه، اسکن سریع و انجام عملیات روی داده‌ها.

#### Scenario: Basic table rendering
- **WHEN** عنصر `div.table-container[data-table]` در صفحه وجود دارد
- **THEN** جدول با ساختار کامل (header, search, thead, tbody, pagination) رندر می‌شود
- **AND** جدول RTL-first است و از چپ به راست نیز پشتیبانی می‌کند

### Requirement: Tile Header
نوار عنوان جدول SHALL شامل عنوان، تعداد آیتم‌ها و دکمه‌های عملیات باشد.

#### Scenario: Header layout
- **WHEN** `.table__header` رندر می‌شود
- **THEN** عنوان (SemiBold 20px #222323) در سمت راست قرار دارد
- **AND** تعداد (Regular 13px #222323) با نقطه جداکننده (4px) بعد از عنوان نمایش می‌یابد
- **AND** دکمه‌های عملیات در سمت چپ قرار دارند
- **AND** padding 16px 24px و gap 24px بین بخش‌ها وجود دارد

#### Scenario: Action buttons
- **WHEN** دکمه‌های عملیات رندر می‌شوند
- **THEN** دکمه primary (افزودن): bg #26a88c، border #1d836d، متن سفید، ارتفاع 45px، radius 8px
- **AND** دکمه secondary (بارگذاری): bg سفید، border #e2e4e6، متن #222323، ارتفاع 45px
- **AND** خط جداکننده عمودی (30px) بین دکمه فیلتر و بقیه وجود دارد

### Requirement: Search Box
باکس جستجو SHALL فیلتر client-side ردیف‌ها را فراهم کند.

#### Scenario: Search rendering
- **WHEN** `.table__search` رندر می‌شود
- **THEN** ارتفاع 45px، bg سفید، border #e2e4e6، radius 8px
- **AND** آیکن جستجو (20px) در سمت راست و placeholder «جستجو...» (Regular 14px #59595a)

#### Scenario: Search filtering
- **WHEN** کاربر متن در فیلد جستجو تایپ می‌کند
- **THEN** ردیف‌هایی که شامل متن جستجو نیستند مخفی می‌شوند
- **AND** پیجینیشن بر اساس نتایج فیلتر شده به‌روزرسانی می‌شود

### Requirement: Table Head
سرستون جدول SHALL ستون‌ها را با آیکن و متن نمایش دهد.

#### Scenario: Header row
- **WHEN** `.table__row--head` رندر می‌شود
- **THEN** ارتفاع 55px، bg سفید، border-bottom 1px #e2e4e6
- **AND** هر ستون: padding 16px، فونت Regular 13px #59595a، gap 8px بین آیکن و متن
- **AND** ستون اول (سمت راست در RTL) شامل چک‌باکس select-all است

### Requirement: Table Body Rows
ردیف‌های بدنه جدول SHALL داده‌ها را در سلول‌ها نمایش دهند.

#### Scenario: Default row
- **WHEN** `.table__row` در tbody رندر می‌شود
- **THEN** ارتفاع 60px، bg سفید، border-bottom 1px #e2e4e6
- **AND** متن سلول: Regular 14px #222323، padding 16px

#### Scenario: Hover row
- **WHEN** کاربر ماوس را روی یک ردیف می‌برد
- **THEN** پس‌زمینه ردیف به #f6f8fa تغییر می‌کند
- **AND** خط سبز عمودی 3px در سمت چپ ردیف (border-inline-start) ظاهر می‌شود
- **AND** آیکن سه‌نقطه (⋮) در سمت چپ‌ترین ستون نمایش می‌یابد

#### Scenario: Selected row
- **WHEN** چک‌باکس یک ردیف فعال می‌شود
- **THEN** کلاس `.table__row--selected` به ردیف اضافه می‌شود
- **AND** چک‌باکس حالت checked (bg #26a88c، آیکن سفید) نمایش می‌دهد

### Requirement: Checkbox Column
ستون چک‌باکس SHALL انتخاب تکی و گروهی ردیف‌ها را فراهم کند.

#### Scenario: Checkbox styling
- **WHEN** چک‌باکس رندر می‌شود
- **THEN** سایز 28px، border 1px #626364، radius 4px
- **AND** حالت checked: bg #26a88c با آیکن سفید

#### Scenario: Select all
- **WHEN** چک‌باکس هدر کلیک می‌شود
- **THEN** همه چک‌باکس‌های ردیف‌ها toggle می‌شوند
- **AND** Action Bar نمایش/مخفی می‌شود بر اساس تعداد انتخاب شده

### Requirement: Status Tags
تگ وضعیت SHALL حالت «فعال» یا «غیرفعال» را نمایش دهد.

#### Scenario: Tag rendering
- **WHEN** `.table__tag` رندر می‌شود
- **THEN** ارتفاع 32px، bg #f6f8fa، border 2px سفید، radius 8px، padding 0 8px
- **AND** فونت Regular 14px #222323

### Requirement: Progress Bar
نوار پیشرفت SHALL درصد تکمیل را به صورت بصری نمایش دهد.

#### Scenario: Progress rendering
- **WHEN** `.table__progress` رندر می‌شود
- **THEN** متن «X از Y انجام شده» (Regular 14px #222323) بالای نوار نمایش می‌یابد
- **AND** نوار: عرض 120px، ارتفاع 3px، bg #e2e4e6، fill #26a88c، radius 360px
- **AND** عرض fill متناسب با نسبت X/Y محاسبه می‌شود

### Requirement: Pagination
پیجینیشن SHALL ناوبری بین صفحات جدول را فراهم کند.

#### Scenario: Pagination layout
- **WHEN** `.table__pagination` رندر می‌شود
- **THEN** دکمه‌های صفحه در سمت چپ: 37×37px، radius 8px، border #e2e4e6، shadow
- **AND** صفحه فعال: bg #26a88c، متن سفید، border #1d836d
- **AND** «۱۰ ردیف در هر صفحه» در سمت راست

#### Scenario: Page navigation
- **WHEN** کاربر دکمه صفحه را کلیک می‌کند
- **THEN** ردیف‌های صفحه جدید نمایش و ردیف‌های قبلی مخفی می‌شوند
- **AND** دکمه صفحه فعال به‌روزرسانی می‌شود

### Requirement: Action Bar
نوار عملیات دسته‌ای SHALL وقتی ردیف‌هایی انتخاب شده‌اند نمایش یابد.

#### Scenario: Action bar visibility
- **WHEN** حداقل یک ردیف انتخاب شده
- **THEN** نوار عملیات در پایین جدول نمایش می‌یابد (bg #222323)
- **AND** تعداد ردیف‌های انتخاب شده نمایش می‌یابد (Regular 14px سفید)
- **AND** دکمه‌های عملیات با آیکن و متن نمایش می‌یابند (Regular 13px سفید)

#### Scenario: Action bar hidden
- **WHEN** هیچ ردیفی انتخاب نشده
- **THEN** نوار عملیات مخفی است

### Requirement: JavaScript API
کامپوننت جدول SHALL یک API عمومی روی `window.Table` فراهم کند.

#### Scenario: API methods
- **WHEN** JavaScript بارگذاری شده
- **THEN** `Table.init(element)` یک جدول را فعال می‌کند
- **AND** `Table.initAll()` همه جدول‌ها را فعال می‌کند
- **AND** `Table.getSelected(tableId)` آرایه ردیف‌های انتخاب شده را برمی‌گرداند
- **AND** `Table.selectAll(tableId)` همه ردیف‌ها را انتخاب می‌کند
- **AND** `Table.deselectAll(tableId)` انتخاب همه را لغو می‌کند
- **AND** `Table.goToPage(tableId, page)` به صفحه مشخص می‌رود
- **AND** `Table.onSelect(tableId, fn)` callback انتخاب ثبت می‌کند
- **AND** `Table.onPageChange(tableId, fn)` callback تغییر صفحه ثبت می‌کند

### Requirement: RTL Support
کامپوننت جدول SHALL از RTL (راست به چپ) و LTR (چپ به راست) پشتیبانی کند.

#### Scenario: RTL layout
- **WHEN** صفحه `dir="rtl"` دارد
- **THEN** ستون‌ها از راست به چپ چیده می‌شوند
- **AND** ستون چک‌باکس سمت راست قرار دارد
- **AND** عنوان سمت راست و دکمه‌ها سمت چپ هستند
- **AND** خط سبز هاور سمت چپ ردیف ظاهر می‌شود

#### Scenario: LTR layout
- **WHEN** صفحه `dir="ltr"` دارد
- **THEN** ستون‌ها از چپ به راست چیده می‌شوند

### Requirement: Auto Initialization
کامپوننت جدول SHALL هنگام DOMContentLoaded به صورت خودکار فعال شود.

#### Scenario: Auto-init
- **WHEN** صفحه بارگذاری می‌شود
- **THEN** تمام عناصر `[data-table]` به صورت خودکار فعال می‌شوند
- **AND** پیجینیشن، انتخاب ردیف و جستجو فعال می‌شوند
