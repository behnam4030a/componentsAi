## ADDED Requirements

### Requirement: Server-Side Mode
کامپوننت Table SHALL از حالت server-side پشتیبانی کند که در آن JS به جای فیلتر/صفحه‌بندی client-side، رویدادها را از طریق callback به لایه‌ی بالاتر اطلاع می‌دهد و داده‌ها از سرور بارگذاری می‌شوند.

#### Scenario: Activating server-side mode
- **WHEN** container دارای `data-mode="server"` باشد
- **THEN** جدول در حالت server-side فعال می‌شود
- **AND** جستجو، تغییر صفحه و حذف دسته‌ای دیگر DOM را مستقیم تغییر نمی‌دهند

#### Scenario: Default client-side mode unchanged
- **WHEN** container فاقد `data-mode` یا دارای `data-mode="client"` باشد
- **THEN** رفتار قبلی (client-side) حفظ می‌شود بدون هیچ تغییری

### Requirement: Server-Side Row Update
کامپوننت Table SHALL متد `Table.setRows(id, rows)` را ارائه دهد که ردیف‌های tbody را با داده‌های جدید از سرور جایگزین کند.

#### Scenario: Setting rows with TR elements
- **WHEN** `Table.setRows('my-table', [trElement1, trElement2, ...])` فراخوانی می‌شود
- **THEN** ردیف‌های قبلی tbody پاک می‌شوند
- **AND** ردیف‌های جدید در tbody درج می‌شوند
- **AND** event listeners (checkbox، row action) روی ردیف‌های جدید bind می‌شوند
- **AND** loading state حذف می‌شود

#### Scenario: Setting rows with HTML string
- **WHEN** `Table.setRows('my-table', '<tr>...</tr><tr>...</tr>')` با HTML string فراخوانی می‌شود
- **THEN** HTML parse شده و ردیف‌ها جایگزین محتوای tbody می‌شوند
- **AND** event listeners روی ردیف‌های جدید bind می‌شوند

#### Scenario: Empty result set
- **WHEN** `Table.setRows('my-table', [])` یا `Table.setRows('my-table', '')` فراخوانی می‌شود
- **THEN** tbody خالی می‌شود
- **AND** پیام «نتیجه‌ای یافت نشد» نمایش می‌یابد

### Requirement: Server-Side Total Count
کامپوننت Table SHALL متد `Table.setTotal(id, total)` را ارائه دهد که تعداد کل ردیف‌ها را از سرور دریافت و صفحه‌بندی را به‌روز کند.

#### Scenario: Updating total count
- **WHEN** `Table.setTotal('my-table', 250)` فراخوانی می‌شود
- **THEN** تعداد کل صفحات بر اساس `total / pageSize` محاسبه می‌شود
- **AND** صفحه‌بندی با تعداد صفحات جدید re-render می‌شود

### Requirement: Server-Side Search Callback
کامپوننت Table SHALL در حالت server-side به جای فیلتر client-side، callback `onSearch` را با query جستجو فایر کند.

#### Scenario: Search fires callback
- **WHEN** کاربر در فیلد جستجو تایپ می‌کند (با debounce 250ms) و جدول در server-side mode است
- **THEN** callback ثبت‌شده با `Table.onSearch` با `{ query: string }` فراخوانی می‌شود
- **AND** هیچ فیلتری روی DOM اعمال نمی‌شود

#### Scenario: Clear search fires callback
- **WHEN** کاربر دکمه clear جستجو را کلیک می‌کند و جدول در server-side mode است
- **THEN** callback با `{ query: '' }` فراخوانی می‌شود

### Requirement: Server-Side Bulk Action Callback
کامپوننت Table SHALL در حالت server-side به جای حذف DOM، callback `onBulkAction` را با عملیات و ردیف‌های انتخاب‌شده فایر کند.

#### Scenario: Bulk delete fires callback
- **WHEN** کاربر دکمه «حذف» در action bar کلیک می‌کند و جدول در server-side mode است
- **THEN** callback ثبت‌شده با `Table.onBulkAction` با `{ action: 'delete', rows: Element[] }` فراخوانی می‌شود
- **AND** ردیف‌ها از DOM حذف نمی‌شوند (سرور تصمیم می‌گیرد)

### Requirement: Table Loading State
کامپوننت Table SHALL در حالت server-side loading state را از طریق CSS class نمایش دهد.

#### Scenario: Loading state active
- **WHEN** داده در حال بارگذاری است (قبل از فراخوانی `Table.setRows`)
- **THEN** کلاس `table--loading` روی container وجود دارد
- **AND** tbody با opacity کاهش‌یافته نمایش می‌یابد

#### Scenario: Loading state removed
- **WHEN** `Table.setRows` فراخوانی می‌شود
- **THEN** کلاس `table--loading` از container حذف می‌شود

## MODIFIED Requirements

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
- **AND** `Table.onPageChange(tableId, fn)` callback تغییر صفحه ثبت می‌کند — در server mode با `{ page, pageSize }` فراخوانی می‌شود
- **AND** `Table.setRows(tableId, rows)` ردیف‌های tbody را در server mode جایگزین می‌کند
- **AND** `Table.setTotal(tableId, total)` تعداد کل را در server mode تنظیم می‌کند
- **AND** `Table.onSearch(tableId, fn)` callback جستجو در server mode ثبت می‌کند
- **AND** `Table.onBulkAction(tableId, fn)` callback عملیات دسته‌ای در server mode ثبت می‌کند
