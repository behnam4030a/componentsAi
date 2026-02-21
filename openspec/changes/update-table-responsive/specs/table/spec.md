## ADDED Requirements

### Requirement: Table Mobile Card Layout
سیستم باید (SHALL) در عرض صفحه زیر 768px، جدول را به حالت کارتی تبدیل کند. هر ردیف جدول به یک کارت عمودی تبدیل می‌شود که داده‌ها را به صورت key-value نمایش می‌دهد.

هر کارت شامل:
- **هدر کارت**: checkbox + کد اختصاصی (label + value) + دکمه سه‌نقطه (⋮)
- **بدنه کارت**: ردیف‌های key-value عمودی:
  - label سمت راست (۱۳px, خاکستری #59595a)
  - مقدار سمت چپ (۱۴px, مشکی #222323)
  - divider بین هر ردیف
- **ردیف progress**: نوار پیشرفت (100px × 3px) + متن
- **ردیف وضعیت**: tag (فعال/غیرفعال)

#### Scenario: Table converts to cards on mobile
- **WHEN** عرض صفحه کمتر از 768px باشد
- **THEN** ردیف‌های جدول به صورت کارت‌های عمودی با key-value نمایش داده شوند

#### Scenario: Card shows all data fields
- **WHEN** یک کارت موبایل نمایش داده شود
- **THEN** تمام فیلدهای داده (نام، کد، شماره تماس، وضعیت آزمون، وضعیت) به صورت ردیف‌های جداگانه با label نمایش داده شوند

### Requirement: Table Mobile Header Layout
سیستم باید (SHALL) در حالت موبایل، هدر جدول را به صورت عمودی ساختاردهی کند:
- ردیف اول: عنوان + تعداد
- ردیف دوم: دکمه‌های «افزودن» (primary) + «بارگذاری گروهی» (outline) کنار هم و full-width
- ردیف سوم: دکمه فیلتر + input جستجو

#### Scenario: Mobile header stacks vertically
- **WHEN** عرض صفحه کمتر از 768px باشد
- **THEN** هدر جدول به صورت عمودی با دکمه‌های full-width نمایش داده شود

### Requirement: Table Mobile Select All Row
سیستم باید (SHALL) ردیف «انتخاب همه» را بالای کارت‌ها در موبایل نمایش دهد:
- سمت راست: checkbox + متن «انتخاب همه»
- سمت چپ: دکمه «فعالیت گروهی»
- پس‌زمینه: سفید، border-radius: 8px

#### Scenario: Select all row selects all cards
- **WHEN** کاربر checkbox «انتخاب همه» را فعال کند
- **THEN** تمام کارت‌ها انتخاب شوند و action bar نمایش داده شود

### Requirement: Table Mobile Card Selection State
سیستم باید (SHALL) حالت انتخاب‌شده کارت‌ها را با تغییرات بصری نمایش دهد:
- checkbox سبز (#26a88c)
- border-inline-start سبز (3px solid #26a88c)
- action bar تیره (#222323) در پایین صفحه

#### Scenario: Selected card shows green border
- **WHEN** کاربر یک کارت را انتخاب کند
- **THEN** کارت با border سبز سمت راست و checkbox سبز نمایش داده شود و action bar ظاهر شود

### Requirement: Table Mobile Pagination
سیستم باید (SHALL) pagination در موبایل را شامل موارد زیر کند:
- دکمه‌های شماره صفحه (prev/next + اعداد)
- دکمه «ردیف در هر صفحه» full-width در زیر pagination

#### Scenario: Mobile pagination works correctly
- **WHEN** کاربر دکمه صفحه بعد را بزند
- **THEN** کارت‌های صفحه جدید نمایش داده شوند

## MODIFIED Requirements

### Requirement: Table Header Actions
سیستم باید (SHALL) دکمه «بارگذاری گروهی» (outline, با آیکن upload) را در هدر جدول کنار دکمه اصلی و فیلتر نمایش دهد.

در دسکتاپ: دکمه‌ها در یک ردیف افقی
در موبایل: دکمه‌ها به صورت full-width در ردیف جداگانه

#### Scenario: Group upload button visible in header
- **WHEN** جدول نمایش داده شود
- **THEN** دکمه «بارگذاری گروهی» در هدر کنار سایر دکمه‌ها نمایش داده شود
