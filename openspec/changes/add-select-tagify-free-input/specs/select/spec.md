## MODIFIED Requirements

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

#### Scenario: Tagify type — predefined selection
- **WHEN** Select با کلاس `select--tagify` ایجاد شود
- **THEN** مقادیر انتخاب شده به صورت تگ‌های خاکستری در trigger نمایش یابند
- **AND** هر تگ دارای آیکن حذف (close-square) باشد
- **AND** چند آیتم قابل انتخاب باشد

#### Scenario: Tagify type — free input mode
- **WHEN** Select با کلاس `select--tagify` و attribute `data-free-input="true"` ایجاد شود
- **THEN** یک inline text input در داخل trigger نمایش داده شود
- **AND** کاربر بتواند مستقیماً در trigger تایپ کند
- **AND** با فشار دادن Enter یا کاما (`,`) تگ جدید از متن وارد شده ایجاد شود
- **AND** متن خالی یا فاصله‌دار نادیده گرفته شود
- **AND** با Backspace در input خالی، آخرین تگ حذف شود
- **AND** dropdown (اگر وجود داشته باشد) همچنان برای انتخاب آیتم‌های از پیش تعریف‌شده کار کند

## ADDED Requirements

### Requirement: Tagify Free-Input Behavior
در حالت free-input، کامپوننت Tagify SHALL به کاربر اجازه دهد تگ‌های دلخواه را با تایپ کردن ایجاد کند، علاوه بر انتخاب از dropdown.

#### Scenario: Create tag by typing
- **WHEN** کاربر در tagify free-input متنی تایپ کند و Enter بزند
- **THEN** تگ جدید با همان متن به trigger اضافه شود
- **AND** inline input پاک شود
- **AND** مقدار تگ در hidden input ثبت شود

#### Scenario: Create tag by comma
- **WHEN** کاربر در tagify free-input متنی تایپ کند و کاما (`,`) بزند
- **THEN** تگ جدید ایجاد شود (بدون نمایش کاما)
- **AND** inline input پاک شود

#### Scenario: Backspace removes last tag
- **WHEN** inline input خالی باشد و کاربر Backspace بزند
- **THEN** آخرین تگ موجود حذف شود

#### Scenario: Duplicate tag prevention
- **WHEN** کاربر مقداری تایپ کند که از قبل به عنوان تگ موجود است
- **THEN** تگ تکراری ایجاد نشود

#### Scenario: Inline input auto-focus on trigger click
- **WHEN** کاربر روی trigger tagify free-input کلیک کند
- **THEN** فوکوس به inline input منتقل شود

#### Scenario: Placeholder in inline input
- **WHEN** هیچ تگی در tagify free-input انتخاب نشده باشد
- **THEN** inline input متن placeholder را نمایش دهد
- **WHEN** حداقل یک تگ وجود داشته باشد
- **THEN** placeholder مخفی شود
