# Change: Update Table Component — Mobile Card Layout + Desktop Refinements

## Why
کامپوننت Table در حال حاضر فقط حالت دسکتاپ (جدول ردیفی) را پشتیبانی می‌کند. طبق دیزاین Figma، در موبایل (زیر 768px) باید به **حالت کارت** تغییر کند. هر ردیف جدول به یک کارت عمودی تبدیل می‌شود که داده‌ها را به صورت key-value نمایش می‌دهد.

## What Changes

### 1. موبایل — حالت کارت (NEW)
در عرض زیر 768px، جدول به حالت کارت تبدیل می‌شود:

#### ساختار هدر موبایل
- **ردیف عنوان**: عنوان (مثلاً «لیست کاربران») + تعداد (مثلاً «تعداد: ۴۷ نفر»)
- **ردیف دکمه‌ها**: «افزودن کاربر جدید» (primary) + «بارگذاری گروهی» (outline) — کنار هم و full-width
- **ردیف فیلتر/جستجو**: دکمه فیلتر + input جستجو

#### ساختار کارت
- **هدر کارت**: checkbox + کد اختصاصی (مقدار + label) + دکمه ⋮ (سه‌نقطه)
- **بدنه کارت**: داده‌ها به صورت عمودی key-value:
  - هر ردیف: label (سمت راست، ۱۳px خاکستری) | مقدار (سمت چپ، ۱۴px مشکی)
  - بین هر ردیف: divider (خط جداکننده)
  - ردیف وضعیت آزمون: شامل progress bar + متن
  - ردیف وضعیت: شامل tag (فعال/غیرفعال)

#### ردیف «انتخاب همه»
- بالای کارت‌ها: checkbox «انتخاب همه» + دکمه «فعالیت گروهی»

#### فوتر موبایل
- pagination (دکمه‌های شماره صفحه)
- دکمه «۱۰ ردیف در هر صفحه» full-width

#### حالت‌های موبایل
| حالت | توضیح |
|------|-------|
| Default | کارت‌ها با checkbox خالی، بدون action bar |
| Setting (Selected) | کارت‌های انتخاب‌شده: checkbox سبز + border-inline-start سبز + action bar تیره پایین صفحه |

### 2. دسکتاپ — بروزرسانی‌ها (MINOR)
- اضافه شدن دکمه «بارگذاری گروهی» در هدر (کنار فیلتر و دکمه اصلی)

### 3. مقادیر دیزاین موبایل (از Figma)
| Token | Value |
|-------|-------|
| Card bg | `white` (#ffffff) |
| Card border | `white` (border: 1px solid white) |
| Card radius | `8px` |
| Card header padding | `12px 16px` |
| Card content padding | `12px 24px` |
| Card data label | `13px, #59595a, Regular` |
| Card data value | `14px, #222323, Regular` |
| Card divider | `1px solid #e2e4e6` (خط نازک) |
| Select-all row bg | `white`, padding `12px 16px` |
| Select-all row radius | `8px` |
| Mobile progress width | `100px` |
| Mobile progress height | `3px` |
| Page bg | `#f6f8fa` |
| Gap between cards | `8px` |
| Gap between sections | `16px` |

## Impact
- Affected specs: table (existing capability)
- Affected code:
  - `components/table/table.css` (update — add mobile card styles)
  - `components/table/table.js` (update — JS support for card layout)
  - `components/table/index.html` (update — add mobile-compatible HTML)
  - `components/table/tokens.json` (update — add mobile tokens)

## Technical Details
- **Breakpoint**: `@media (max-width: 768px)` — کارت‌ها فقط در موبایل نمایش داده می‌شوند
- **HTML Approach**: جدول HTML (`<table>`) در دسکتاپ + نمایش کارتی CSS-only از همان داده‌ها در موبایل (با `data-label` attributes)
- **JS Updates**: اسکریپت‌های selection/pagination/search باید با ساختار کارتی هم کار کنند
