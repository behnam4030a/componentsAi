## ADDED Requirements

### Requirement: Tab Hover State
کامپوننت Tab SHALL در حالت hover رنگ متن تب غیرفعال را به brand color (#26a88c) تغییر دهد — هم در نوع underline هم filled.

#### Scenario: Hover on inactive underline tab
- **WHEN** کاربر ماوس را روی تب غیرفعال (underline) ببرد
- **THEN** رنگ متن به #26a88c (brand) تغییر کند

#### Scenario: Hover on inactive filled tab
- **WHEN** کاربر ماوس را روی تب غیرفعال (filled) ببرد
- **THEN** رنگ متن به #26a88c (brand) تغییر کند

### Requirement: Colored Active Variant
کامپوننت Tab SHALL از modifier `tab--colored` پشتیبانی کند که در آن تب فعال به جای رنگ تیره (#222323)، رنگ brand (#26a88c) داشته باشد. این modifier با هر دو نوع underline و filled قابل ترکیب است.

#### Scenario: Colored underline active tab
- **WHEN** tab دارای کلاس `tab--colored` باشد و تب فعال رندر شود
- **THEN** رنگ متن تب فعال #26a88c (brand) باشد
- **AND** خط زیر همچنان #26a88c باشد

#### Scenario: Colored filled active tab
- **WHEN** tab دارای کلاسه‌های `tab--filled tab--colored` باشد و تب فعال رندر شود
- **THEN** تب فعال همچنان پس‌زمینه سبز و متن سفید داشته باشد (رفتار filled بدون تغییر)

### Requirement: Mobile Horizontal Scroll
کامپوننت Tab SHALL در موبایل (عرض ≤ 767px) وقتی تب‌ها از عرض صفحه خارج شوند، اسکرول افقی داشته باشد.

#### Scenario: Mobile scroll when tabs overflow
- **WHEN** عرض صفحه ≤ 767px باشد و تعداد تب‌ها از عرض container بیشتر شود
- **THEN** نوار تب قابل اسکرول افقی باشد
- **AND** تمام تب‌ها قابل دسترسی باشند

## MODIFIED Requirements

### Requirement: Tab Item interaction
هر آیتم تب SHALL دارای padding افقی 12px و عمودی 16px باشد. فونت Peyda(FaNum) با سایز 13px و line-height 1.3 استفاده شود. آیتم‌ها cursor pointer داشته باشند. در hover، رنگ متن به brand color (#26a88c) تغییر کند.

#### Scenario: Tab item spacing
- **WHEN** آیتم تب رندر شود
- **THEN** padding افقی 12px و عمودی 16px داشته باشد
- **AND** فونت Peyda(FaNum) با سایز 13px و line-height 1.3 باشد

#### Scenario: Tab item hover
- **WHEN** کاربر ماوس را روی آیتم تب ببرد
- **THEN** cursor pointer نمایش یابد
- **AND** رنگ متن به #26a88c (brand) تغییر کند
