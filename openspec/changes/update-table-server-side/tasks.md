# تسک‌های پیاده‌سازی Update Table — Server-Side Mode

## 1. JS — table.js

- [x] 1.1 خواندن `data-mode` از container در `initTable` و ذخیره در state (`mode: 'client'|'server'`)
- [x] 1.2 افزودن `totalRows` به state (در server mode توسط `Table.setTotal` تنظیم می‌شود)
- [x] 1.3 در server mode: جستجو به جای `filterRows`، callback `search` را با `{ query }` فایر کند
- [x] 1.4 در server mode: تغییر صفحه/page-size به جای `showPage`، callback `pageChange` را با `{ page, pageSize }` فایر کند
- [x] 1.5 در server mode: `getTotalPages` از `state.totalRows` محاسبه کند (نه DOM rows)
- [x] 1.6 در server mode: bulk delete به جای حذف DOM، callback `bulkAction` را با `{ action, rows }` فایر کند
- [x] 1.7 پیاده‌سازی `Table.setRows(id, rows)`: جایگزینی tbody rows و re-attach کردن listeners
- [x] 1.8 پیاده‌سازی `Table.setTotal(id, total)`: تنظیم `state.totalRows` و re-render پیجینیشن
- [x] 1.9 پیاده‌سازی `Table.onSearch(id, fn)` و `Table.onBulkAction(id, fn)` callbacks
- [x] 1.10 در server mode: نمایش loading state در tbody هنگام انتظار برای داده (کلاس `table--loading`)

## 2. CSS — table.css

- [x] 2.1 افزودن loading state: `.table--loading .table__tbody` با overlay یا opacity

## 3. HTML Demo — index.html

- [x] 3.1 افزودن demo section برای server-side mode با `data-mode="server"`
- [x] 3.2 نمایش callback events در demo (console.log یا یک div نمایش)

## 4. مستندات — README.md

- [x] 4.1 مستندسازی `data-mode` اتریبیوت
- [x] 4.2 مستندسازی `Table.setRows`, `Table.setTotal`, `Table.onSearch`, `Table.onBulkAction`
- [x] 4.3 افزودن نمونه کد server-side integration به README
