# Change: Update Message Bar Component

## Why
کامپوننت Message Bar بر اساس طراحی جدید فیگما به‌روزرسانی شده و سه نوع اصلی Dismissible، Actionable و Detailed دارد.

## What Changes

### سه نوع Message Bar

#### 1. Dismissible (قابل بستن)
فقط یک پیام نمایش داده می‌شود و امکان بستن پیام با زدن ضربدر وجود دارد.

#### 2. Actionable (قابل عمل)
پیام با لینک «بیشتر بدانید» (متن پیشفرض قابل تغییر) که به صفحه دیگر لینک می‌شود.

#### 3. Detailed (جزئیات)
توضیحات کامل‌تری در متن پیام نمایش داده می‌شود — یک عنوان و یک متن توضیحات. برای بستن از دکمه ضربدر.

### موقعیت نمایش
- دسکتاپ: پیش‌فرض پایین صفحه سمت راست
- موبایل: پایین صفحه با تمام عرض و مارجین مشخص از طرفین
- موقعیت به صورت آپشن قابل تنظیم است و می‌توان آن را در هرکجای صفحه به نمایش در آورد

### رنگ قابل تغییر
رنگ message barها کاملا نسبت به موضوع پیام قابل تغییر می‌باشد.

### بسته شدن خودکار (Auto-Dismiss)
امکان بسته شدن خودکار پیام پس از طی زمان مشخص فراهم شده و این ویژگی به صورت آپشنال قابل تنظیم است.

## Impact
- Affected specs: message-bar (update existing capability)
- Affected code:
  - /components/message-bar/message-bar.css (update)
  - /components/message-bar/message-bar.js (update)
  - /components/message-bar/tokens.json (update)
  - /components/message-bar/index.html (update)
  - /components/message-bar/README.md (update)
