# Change: Update Table — Server-Side Mode

## Why
کامپوننت Table در حال حاضر فقط client-side کار می‌کند — همه ردیف‌ها در DOM هستند و JS فیلتر، صفحه‌بندی و جستجو را مستقیماً روی DOM انجام می‌دهد. برای جداول با داده‌های بزرگ (صدها هزار ردیف) یا داده‌های پویا که از API می‌آیند، باید server-side mode اضافه شود — جایی که JS فقط رویدادها را به سرور اطلاع می‌دهد و سرور داده‌های صفحه فعلی را می‌فرستد.

## What Changes
- **ADDED** `data-mode="server"` اتریبیوت: فعال‌سازی حالت server-side روی container
- **ADDED** `Table.setRows(id, rows)`: جایگزینی ردیف‌های tbody با ردیف‌های جدید از سرور (با آرایه المان‌های TR یا HTML string)
- **ADDED** `Table.setTotal(id, total)`: تنظیم تعداد کل ردیف‌ها از سرور برای محاسبه صفحه‌بندی
- **ADDED** `Table.onSearch(id, fn)`: callback برای دریافت query جستجو از سرور
- **MODIFIED** `Table.onPageChange`: در server-side mode، callback با `{ page, pageSize }` فراخوانی می‌شود (به جای فقط page)
- در server-side mode: جستجو callback می‌زند (نه DOM فیلتر)، تغییر صفحه callback می‌زند (نه نمایش/مخفی ردیف)، حذف دسته‌ای callback می‌زند (نه حذف DOM)

## Impact
- Affected specs: table
- Affected code: `components/table/table.js`, `components/table/index.html`, `components/table/README.md`
