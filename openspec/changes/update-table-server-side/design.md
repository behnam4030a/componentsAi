# Design — Table Server-Side Mode

## Context

کامپوننت Table در حال حاضر client-side است: تمام ردیف‌ها در DOM وجود دارند و JS مستقیماً آن‌ها را نمایش/مخفی می‌کند. Server-side mode برای جداولی است که داده از API می‌آید و نباید همه رکوردها به‌یک‌بار لود شوند.

## Goals / Non-Goals

- **Goals:**
  - پشتیبانی از `data-mode="server"` بدون تغییر در client mode
  - API ساده برای تنظیم ردیف‌ها و تعداد کل
  - Callbacks برای جستجو، تغییر صفحه، حذف دسته‌ای

- **Non-Goals:**
  - Sorting روی ستون‌ها (پیاده‌سازی جداگانه)
  - Virtual scrolling یا infinite scroll
  - Cache کردن صفحات قبلی
  - WebSocket / real-time updates

## Decisions

### 1. تشخیص حالت با `data-mode="server"`
- Default: `data-mode="client"` (رفتار فعلی)
- Server mode: `data-mode="server"` — JS callbacks می‌زند، DOM را مدیریت نمی‌کند

### 2. `Table.setRows(id, rows)` — بازنویسی ردیف‌ها
- ورودی: آرایه‌ای از المان‌های `<tr>` یا HTML string
- JS ردیف‌های قدیمی tbody را پاک می‌کند، ردیف‌های جدید را insert می‌کند
- بعد از insert، event listeners (checkbox، row action) مجدداً bind می‌شوند
- `state.allRows` به‌روز می‌شود
- Loading state برداشته می‌شود

### 3. `Table.setTotal(id, total)` — تعداد کل از سرور
- `state.totalRows = total`
- Pagination با `totalRows` محاسبه می‌شود (نه DOM rows)
- `renderPagination` فراخوانی می‌شود

### 4. Callbacks در server mode
- `onSearch(id, fn)`: fn با `{ query: string }` فراخوانی می‌شود
- `onPageChange(id, fn)`: fn با `{ page: number, pageSize: number }` فراخوانی می‌شود
- `onBulkAction(id, fn)`: fn با `{ action: string, rows: Element[] }` فراخوانی می‌شود

### 5. Loading state
- وقتی داده هنوز نرسیده: `table--loading` کلاس روی container
- CSS: opacity کاهش پیدا می‌کند، pointer-events none

## Risks / Trade-offs

- **Re-bind listeners**: هر بار `setRows` فراخوانی می‌شود، باید listeners مجدداً bind شوند — overhead کوچک قابل قبول است چون فقط current page rows bind می‌شوند
- **No sort**: برای پروژه‌های که sort نیاز دارند، باید جداگانه پیاده‌سازی شود

## Migration Plan

تغییر backward-compatible است: جداول بدون `data-mode` یا با `data-mode="client"` دقیقاً مثل قبل کار می‌کنند.
