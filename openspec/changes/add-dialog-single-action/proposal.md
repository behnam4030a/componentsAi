# Change: Add Single-Action Variant to Dialog

## Why
در حال حاضر Dialog همیشه دو دکمه دارد (اقدام + انصراف). گاهی فقط یک تأیید ساده نیاز است — مثل نمایش هشدار یا اطلاعیه‌ای که کاربر باید «متوجه شدم» بزند. نیاز است یک حالت single-action با یک دکمه تمام‌عرض اضافه شود.

## What Changes
- افزودن modifier class `dialog__actions--single` روی `dialog__actions` برای تنظیم خودکار چیدمان تک‌دکمه‌ای
- افزودن نوع دکمه جدید `dialog__btn--confirm` با پس‌زمینه سبز برند (تأیید مثبت)
- در حالت single-action، دکمه به‌صورت خودکار تمام عرض را می‌گیرد
- بدون تغییر در JS — رفتار موجود (data-action + callback) بدون تغییر کار می‌کند

## Impact
- Affected specs: `add-dialog-component` → requirement "Dialog Action Buttons"
- Affected code: `components/dialog/dialog.css`, `components/dialog/index.html`, `components/dialog/README.md`
