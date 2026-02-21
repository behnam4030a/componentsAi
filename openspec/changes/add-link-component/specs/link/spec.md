## ADDED Requirements

### Requirement: Link Base Class
سیستم باید (SHALL) کلاس `.link` را ارائه دهد که فقط استایل‌های اختصاصی لینک را اعمال کند:
- color: `var(--link-color, #0078d4)`
- text-decoration: `var(--link-text-decoration, underline)`
- cursor: `pointer`

استایل‌های فونت (سایز، وزن، ارتفاع خط) از کامپوننت Typography ارث‌بری می‌شود.

#### Scenario: Link class applies color and underline
- **WHEN** یک عنصر `<a>` کلاس `.link` را به همراه کلاس‌های Typography دارد
- **THEN** متن آبی رنگ (#0078d4) با خط زیر نمایش داده شود و cursor به pointer تغییر کند

### Requirement: Link Typography Integration
سیستم باید (SHALL) از کامپوننت Typography برای سایزبندی لینک استفاده کند:
- لینک بزرگ: `<a class="typo typo--body-large-200 link">` (16px, Regular, line-height 2)
- لینک متوسط: `<a class="typo typo--body-medium-200 link">` (14px, Regular, line-height 2)

#### Scenario: Large link uses typography body-large-200
- **WHEN** عنصر لینک کلاس‌های `.typo.typo--body-large-200.link` دارد
- **THEN** متن با سایز 16px از Typography و رنگ آبی از Link نمایش داده شود

#### Scenario: Medium link uses typography body-medium-200
- **WHEN** عنصر لینک کلاس‌های `.typo.typo--body-medium-200.link` دارد
- **THEN** متن با سایز 14px از Typography و رنگ آبی از Link نمایش داده شود

### Requirement: Link CSS Custom Properties
سیستم باید (SHALL) مقادیر اختصاصی لینک را از طریق CSS custom properties در `:root` تعریف کند:
- `--link-color`: رنگ متن لینک
- `--link-text-decoration`: نوع خط تزئینی

#### Scenario: Custom properties are overridable
- **WHEN** یک custom property مانند `--link-color` با مقدار جدید override شود
- **THEN** تمام عناصر با کلاس `.link` رنگ جدید را اعمال کنند

### Requirement: Link Demo Page
سیستم باید (SHALL) صفحه دمو (`index.html`) برای کامپوننت Link ارائه دهد که شامل:
- لینک دادن typography.css برای استفاده از کلاس‌های فونت
- نمایش هر دو سایز (Large و Medium) با متن نمونه فارسی
- مثال کد HTML

#### Scenario: Demo page shows both sizes with typography
- **WHEN** صفحه دمو باز شود
- **THEN** هر دو سایز لینک با ترکیب کلاس‌های Typography و Link نمایش داده شوند
