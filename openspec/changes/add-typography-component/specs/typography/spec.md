## ADDED Requirements

### Requirement: Typography Base Class
سیستم باید (SHALL) کلاس پایه `.typo` را ارائه دهد که شامل:
- font-family: `'Peyda(FaNum)', sans-serif`
- letter-spacing: `0`
- text-align: `right` (RTL-first)
- font-style: `normal`

#### Scenario: Base class applies font family
- **WHEN** یک عنصر HTML کلاس `.typo` را دارد
- **THEN** فونت `Peyda(FaNum)` اعمال شود و متن راست‌چین باشد

### Requirement: Typography Display Style
سیستم باید (SHALL) استایل Display را با کلاس `.typo--display` ارائه دهد:
- font-size: `58px`
- font-weight: `700` (Bold)
- line-height: `75px`

#### Scenario: Display style renders correctly
- **WHEN** عنصر کلاس `.typo.typo--display` دارد
- **THEN** متن با سایز 58px، وزن Bold و فاصله خطوط 75px نمایش داده شود

### Requirement: Typography Large Title Style
سیستم باید (SHALL) استایل Large Title را با کلاس `.typo--large-title` ارائه دهد:
- font-size: `40px`
- font-weight: `600` (SemiBold)
- line-height: `52px`

#### Scenario: Large Title style renders correctly
- **WHEN** عنصر کلاس `.typo.typo--large-title` دارد
- **THEN** متن با سایز 40px، وزن SemiBold و فاصله خطوط 52px نمایش داده شود

### Requirement: Typography Heading Styles
سیستم باید (SHALL) شش سطح سرتیتر را ارائه دهد:
- `.typo--heading-1`: 32px, Bold (700), line-height 1.3
- `.typo--heading-2`: 28px, SemiBold (600), line-height 1.3
- `.typo--heading-3`: 24px, SemiBold (600), line-height 1.3
- `.typo--heading-4`: 20px, SemiBold (600), line-height 1.3
- `.typo--heading-5`: 18px, Medium (500), line-height 1.3
- `.typo--heading-6`: 16px, Medium (500), line-height 1.3

#### Scenario: Heading-1 renders as largest heading
- **WHEN** عنصر کلاس `.typo.typo--heading-1` دارد
- **THEN** متن با سایز 32px، وزن Bold و line-height 1.3 نمایش داده شود

#### Scenario: Heading-6 renders as smallest heading
- **WHEN** عنصر کلاس `.typo.typo--heading-6` دارد
- **THEN** متن با سایز 16px، وزن Medium و line-height 1.3 نمایش داده شود

#### Scenario: Heading hierarchy is visually distinct
- **WHEN** تمام شش سطح heading کنار هم نمایش داده شوند
- **THEN** هر سطح از سطح بالاتر کوچکتر باشد (58→40→32→28→24→20→18→16)

### Requirement: Typography Body Large Styles
سیستم باید (SHALL) سه variant از Body Large (16px) را ارائه دهد:
- `.typo--body-large-200`: Regular (400), line-height 2 — برای پاراگراف‌های طولانی
- `.typo--body-large-150`: Regular (400), line-height 1.5 — برای متن عادی
- `.typo--body-large-emp`: Medium (500), line-height 1.5 — برای تأکید

#### Scenario: Body Large 200 has wider line spacing
- **WHEN** عنصر کلاس `.typo.typo--body-large-200` دارد
- **THEN** متن با سایز 16px، وزن Regular و line-height 2 (فاصله خطوط زیاد) نمایش داده شود

#### Scenario: Body Large EMP is emphasized
- **WHEN** عنصر کلاس `.typo.typo--body-large-emp` دارد
- **THEN** متن با سایز 16px، وزن Medium (تأکیدی) و line-height 1.5 نمایش داده شود

### Requirement: Typography Body Medium Styles
سیستم باید (SHALL) سه variant از Body Medium (14px) را ارائه دهد:
- `.typo--body-medium-200`: Regular (400), line-height 2
- `.typo--body-medium-150`: Regular (400), line-height 1.5
- `.typo--body-medium-emp`: Medium (500), line-height 1.5

#### Scenario: Body Medium 150 renders with normal spacing
- **WHEN** عنصر کلاس `.typo.typo--body-medium-150` دارد
- **THEN** متن با سایز 14px، وزن Regular و line-height 1.5 نمایش داده شود

#### Scenario: Body Medium EMP is emphasized
- **WHEN** عنصر کلاس `.typo.typo--body-medium-emp` دارد
- **THEN** متن با سایز 14px، وزن Medium و line-height 1.5 نمایش داده شود

### Requirement: Typography Body Small Styles
سیستم باید (SHALL) سه variant از Body Small (12px) را ارائه دهد:
- `.typo--body-small-200`: Regular (400), line-height 2
- `.typo--body-small-150`: Regular (400), line-height 1.5
- `.typo--body-small-emp`: Medium (500), line-height 1.5

#### Scenario: Body Small 200 has wider line spacing
- **WHEN** عنصر کلاس `.typo.typo--body-small-200` دارد
- **THEN** متن با سایز 12px، وزن Regular و line-height 2 نمایش داده شود

#### Scenario: Body Small EMP is emphasized
- **WHEN** عنصر کلاس `.typo.typo--body-small-emp` دارد
- **THEN** متن با سایز 12px، وزن Medium و line-height 1.5 نمایش داده شود

### Requirement: Typography Caption Styles
سیستم باید (SHALL) دو variant از Caption (13px) را ارائه دهد:
- `.typo--caption`: Regular (400), line-height 1.3
- `.typo--caption-emp`: Medium (500), line-height 1.3

#### Scenario: Caption renders as small annotation text
- **WHEN** عنصر کلاس `.typo.typo--caption` دارد
- **THEN** متن با سایز 13px، وزن Regular و line-height 1.3 نمایش داده شود

#### Scenario: Caption EMP renders as emphasized annotation
- **WHEN** عنصر کلاس `.typo.typo--caption-emp` دارد
- **THEN** متن با سایز 13px، وزن Medium و line-height 1.3 نمایش داده شود

### Requirement: Typography Button Styles
سیستم باید (SHALL) سه سایز Button typography را ارائه دهد:
- `.typo--button-large`: 14px, Medium (500), line-height 1.4
- `.typo--button-medium`: 14px, Medium (500), line-height 1.4
- `.typo--button-small`: 12px, Medium (500), line-height 1.4

#### Scenario: Button Large text style
- **WHEN** عنصر کلاس `.typo.typo--button-large` دارد
- **THEN** متن با سایز 14px، وزن Medium و line-height 1.4 نمایش داده شود

#### Scenario: Button Small has smaller font
- **WHEN** عنصر کلاس `.typo.typo--button-small` دارد
- **THEN** متن با سایز 12px، وزن Medium و line-height 1.4 نمایش داده شود

### Requirement: Typography CSS Custom Properties
سیستم باید (SHALL) تمام مقادیر تایپوگرافی را از طریق CSS custom properties در `:root` تعریف کند تا امکان override و سفارشی‌سازی فراهم باشد.

#### Scenario: Custom properties are overridable
- **WHEN** یک custom property مانند `--typo-heading-1-size` با مقدار جدید override شود
- **THEN** تمام عناصر با کلاس `.typo--heading-1` سایز جدید را اعمال کنند

### Requirement: Typography RTL/LTR Support
سیستم باید (SHALL) از هر دو جهت متن پشتیبانی کند:
- پیش‌فرض: text-align right (RTL-first)
- پشتیبانی از `[dir="ltr"]` برای text-align left

#### Scenario: Default RTL alignment
- **WHEN** صفحه با `dir="rtl"` تنظیم شده
- **THEN** تمام عناصر `.typo` راست‌چین باشند

#### Scenario: LTR alignment override
- **WHEN** یک عنصر یا والد آن `dir="ltr"` دارد
- **THEN** متن چپ‌چین شود

### Requirement: Typography Demo Page
سیستم باید (SHALL) صفحه دمو (`index.html`) برای کامپوننت Typography ارائه دهد که شامل:
- نمایش تمام 22 استایل با متن نمونه فارسی
- جدول مرجع با ستون‌های Style, Weight, Size, Line Height
- مثال‌های کد HTML

#### Scenario: Demo page shows all styles
- **WHEN** صفحه دمو باز شود
- **THEN** تمام 22 استایل تایپوگرافی با متن نمونه نمایش داده شوند

### Requirement: Typography Integration in Component Demos
سیستم باید (SHALL) فایل typography.css را در تمام دمو صفحات کامپوننت‌های موجود لینک کند تا استایل‌های متنی یکپارچه در همه دموها قابل استفاده باشد.

#### Scenario: Typography CSS available in all demos
- **WHEN** هر یک از دمو صفحات کامپوننت‌ها باز شود
- **THEN** کلاس‌های `.typo` و modifier ها قابل استفاده و فعال باشند
