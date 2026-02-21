## ADDED Requirements

### Requirement: Tooltip Purpose and Description
کامپوننت Tooltip SHALL برای نمایش اطلاعات غیر ضروری و متنی هنگام hover یا focus روی یک عنصر رابط کاربری استفاده شود. تولتیپ یک پیام کوچک و مرتفع است که اطلاعات ساده و مفید ارائه می‌کند. تولتیپ نباید برای بازخورد سیستم یا اطلاعات تعاملی استفاده شود؛ برای اطلاعات تعاملی از Popover استفاده کنید.

#### Scenario: Tooltip basic display
- **WHEN** کاربر روی یک عنصر با tooltip hover کند
- **THEN** tooltip با متن مربوطه نمایش داده شود
- **AND** tooltip نباید مانع تعامل کاربر با سایر بخش‌های UI شود

#### Scenario: Tooltip informational only
- **WHEN** tooltip نمایش داده شود
- **THEN** محتوای آن فقط متن ساده باشد
- **AND** هیچ عنصر تعاملی (لینک، دکمه) داخل tooltip نباشد

### Requirement: Tooltip Positions
کامپوننت Tooltip SHALL از 4 جهت نمایش پشتیبانی کند: Top (بالا)، Bottom (پایین)، Right (راست) و Left (چپ). هر جهت با modifier class یا `data-tooltip-position` attribute مشخص می‌شود. فلش (arrow) همیشه به سمت trigger اشاره می‌کند.

#### Scenario: Top position
- **WHEN** Tooltip با جهت `top` تنظیم شود
- **THEN** bubble بالای trigger ظاهر شود
- **AND** فلش از پایین bubble به سمت trigger اشاره کند

#### Scenario: Bottom position
- **WHEN** Tooltip با جهت `bottom` تنظیم شود
- **THEN** bubble پایین trigger ظاهر شود
- **AND** فلش از بالای bubble به سمت trigger اشاره کند

#### Scenario: Right position
- **WHEN** Tooltip با جهت `right` تنظیم شود
- **THEN** bubble سمت راست trigger ظاهر شود
- **AND** فلش از سمت چپ bubble به سمت trigger اشاره کند

#### Scenario: Left position
- **WHEN** Tooltip با جهت `left` تنظیم شود
- **THEN** bubble سمت چپ trigger ظاهر شود
- **AND** فلش از سمت راست bubble به سمت trigger اشاره کند

### Requirement: Tooltip Visual Design
کامپوننت Tooltip SHALL با پس‌زمینه تیره (#364455)، متن سفید، فونت 14px Medium، border-radius 4px و padding 8px 12px نمایش یابد. فلش (arrow) با همان رنگ پس‌زمینه و اندازه 6px ساخته شود.

#### Scenario: Tooltip appearance
- **WHEN** tooltip نمایش داده شود
- **THEN** پس‌زمینه #364455 و متن سفید با فونت Peyda(FaNum) سایز 14px و وزن 500 نمایش یابد
- **AND** border-radius 4px و padding عمودی 8px و افقی 12px باشد

#### Scenario: Arrow appearance
- **WHEN** tooltip نمایش داده شود
- **THEN** فلش مثلثی با رنگ #364455 و اندازه 6px به سمت trigger نمایش یابد

### Requirement: Show/Hide Behavior
کامپوننت Tooltip SHALL هنگام hover (mouseenter) و focus روی trigger نمایش داده شود و هنگام خروج mouse (mouseleave) و از دست دادن focus (focusout) مخفی شود. تأخیر نمایش قابل تنظیم باشد.

#### Scenario: Show on hover
- **WHEN** کاربر mouse را روی trigger قرار دهد (mouseenter)
- **THEN** tooltip نمایش داده شود

#### Scenario: Hide on mouse leave
- **WHEN** کاربر mouse را از trigger خارج کند (mouseleave)
- **THEN** tooltip مخفی شود

#### Scenario: Show on focus
- **WHEN** trigger فوکوس دریافت کند (focusin)
- **THEN** tooltip نمایش داده شود

#### Scenario: Hide on blur
- **WHEN** trigger فوکوس خود را از دست بدهد (focusout)
- **THEN** tooltip مخفی شود

#### Scenario: Custom delay
- **WHEN** `data-tooltip-delay` با مقدار میلی‌ثانیه تنظیم شود
- **THEN** tooltip با آن تأخیر نمایش داده شود

### Requirement: Data Attribute API
کامپوننت Tooltip SHALL از data attributes برای تنظیم متن و جهت پشتیبانی کند. `data-tooltip` متن tooltip و `data-tooltip-position` جهت نمایش (right یا left) را مشخص می‌کند. JavaScript به صورت خودکار bubble و arrow را می‌سازد.

#### Scenario: Data attribute usage
- **WHEN** المانی با `data-tooltip="متن tooltip"` در DOM باشد
- **THEN** JavaScript به صورت خودکار tooltip bubble و arrow را بسازد
- **AND** هنگام hover/focus متن مشخص شده نمایش یابد

#### Scenario: Position via data attribute
- **WHEN** `data-tooltip-position="left"` تنظیم شود
- **THEN** tooltip سمت چپ trigger ظاهر شود

### Requirement: Accessibility
کامپوننت Tooltip SHALL برای screen reader قابل اعلام باشد. bubble باید `role="tooltip"` داشته باشد و trigger باید با `aria-describedby` به tooltip متصل باشد. tooltip باید هنگام focus روی trigger قابل دسترس باشد.

#### Scenario: ARIA attributes
- **WHEN** tooltip ساخته شود
- **THEN** bubble دارای `role="tooltip"` و `id` یکتا باشد
- **AND** trigger دارای `aria-describedby` با اشاره به id tooltip باشد

#### Scenario: Keyboard accessible
- **WHEN** کاربر با Tab به trigger برسد
- **THEN** tooltip نمایش داده شود
- **AND** screen reader محتوای tooltip را اعلام کند

### Requirement: RTL Support
کامپوننت Tooltip SHALL از RTL پشتیبانی کامل داشته باشد. متن فارسی به صورت صحیح نمایش یابد. در صورت استفاده از `dir="ltr"` ترتیب متن معکوس شود.

#### Scenario: RTL text
- **WHEN** tooltip در محیط RTL نمایش داده شود
- **THEN** متن از سمت راست تراز شود

#### Scenario: LTR text
- **WHEN** tooltip در محیط LTR نمایش داده شود
- **THEN** متن از سمت چپ تراز شود
