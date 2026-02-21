# Change: Add Checkbox Component (Pure CSS)

## Why
ساخت یک کامپوننت Checkbox سه‌حالته (Unchecked، Checked، Indeterminate) قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. این کامپوننت باید از design tokens استخراج شده از Figma پیروی کند و تمام وضعیت‌ها، سایزها و حالت‌های تعاملی تعریف شده در UI Kit را پشتیبانی نماید.

## What Changes
- افزودن کامپوننت Checkbox به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 3 وضعیت منطقی (Status):
  - **Unchecked**: کامپوننت انتخاب نشده — باکس خالی با border
  - **Checked**: کامپوننت انتخاب شده — باکس پر با آیکون تیک (checkmark)
  - **Indeterminate**: انتخاب جزئی — باکس پر با آیکون خط (minus)، فقط در سناریوی Select All
- پشتیبانی از 5 حالت تعاملی (State):
  - Rest (پیش‌فرض)
  - Hover (`:hover`)
  - Pressed (`:active`)
  - Focused (`:focus-visible`) — با حلقه فوکوس خارجی برای ناوبری کیبورد
  - Disabled (`.checkbox--disabled`) — غیرفعال، بدون تعامل
- پشتیبانی از 2 سایز: Large (28px boxholder) و Medium (24px boxholder)
- **Label (برچسب توضیحی)**:
  - اختیاری، در کنار Checkbox نمایش داده می‌شود
  - کلیک روی Label باعث تغییر Status می‌شود (با استفاده از `<label>` بومی HTML)
  - سایز فونت وابسته به Size: بزرگ=14px، متوسط=12px
- **Icon Integration**:
  - آیکون Checkmark (تیک) برای حالت Checked
  - آیکون Minus (خط) برای حالت Indeterminate
  - رنگ آیکون سفید در حالت عادی، خاکستری در حالت Disabled
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: checkbox (new capability)
- **Dependencies**:
  - tokens.json (already created inside checkbox component)
- Affected code:
  - /components/checkbox/checkbox.css (new)
  - /components/checkbox/tokens.json (already created)
  - /components/checkbox/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + minimal HTML structure (بدون JavaScript برای استایل‌دهی)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**: `<label class="checkbox checkbox--large"><input type="checkbox" class="checkbox__input" /><span class="checkbox__box">...</span><span class="checkbox__label">برچسب</span></label>`
- **Indeterminate State**: نیاز به JavaScript برای set کردن `input.indeterminate = true` (محدودیت HTML)
- **Accessibility**: WCAG 2.1 Level AA (focus states, ARIA attributes, color contrast)
- **RTL Support**: Full support for Persian/Arabic text
- **State Management**: CSS-based (`:hover`, `:active`, `:focus-visible`, `:checked`, `:indeterminate`, `:disabled`)
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **Status vs State**: Status (مقدار منطقی) و State (حالت تعاملی) دو مفهوم جداگانه هستند
2. **Indeterminate**: فقط در سناریوی Select All استفاده می‌شود و یک حالت بصری است، نه مقدار نهایی داده
3. **Disabled Rules**: در حالت Disabled، هیچ‌یک از Hover، Pressed و Focused نباید فعال شوند
4. **Label Click**: کلیک روی Label باید Status را تغییر دهد (از طریق `<label>` بومی HTML)
5. **Size Effects**: Size فقط بر ابعاد بصری تأثیر دارد، نه رفتار
6. **Focus Independence**: Focus مستقل از State و با حلقه خارجی (بدون layout shift)
7. **Checkbox vs Radio**: Checkbox برای انتخاب چندگانه، Radio برای انتخاب تکی
8. **Checkbox vs Switch**: Checkbox نیاز به مرحله ارسال دارد، Switch اثر فوری دارد
