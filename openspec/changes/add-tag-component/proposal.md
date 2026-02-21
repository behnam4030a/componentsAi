# Change: Add Tag Component (Pure CSS)

## Why
ساخت یک کامپوننت Tag قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. Tag برای نمایش اطلاعات کوتاه، وضعیت‌ها، دسته‌بندی‌ها یا مقادیر انتخاب‌شده استفاده می‌شود. Tag یک عنصر سبک و غیرمسدودکننده است که می‌تواند صرفا نمایشی باشد یا امکان تعامل محدود (مثل فوکوس یا حذف) داشته باشد.

## What Changes
- افزودن کامپوننت Tag به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 8 خصوصیت (Property):
  - **state**: وضعیت تعاملی/سیستمی — 4 حالت:
    - **Rest**: حالت پیش‌فرض
    - **Hover**: نشانگر روی Tag قرار می‌گیرد
    - **Focus**: فوکوس با کیبورد یا کلیک — نمایش focus ring
    - **Disabled**: غیرفعال — هیچ تعاملی مجاز نیست
  - **radius**: شکل گوشه‌ها — 2 حالت:
    - **Rounded**: گوشه‌های نرم (8px)
    - **Circular**: گوشه‌های کاملا گرد / pill-like (360px)
  - **size**: ابعاد Tag — 3 سایز:
    - **Small**: ارتفاع 24px، فونت 13px، padding افقی 8px
    - **Medium**: ارتفاع 32px، فونت 14px، padding افقی 8px
    - **Large**: ارتفاع 37px، فونت 16px، padding افقی 12px
  - **style**: نوع نمایش بصری — 2 استایل:
    - **Filled**: پس‌زمینه رنگی + border 2px سفید
    - **Outline**: بدون پس‌زمینه + border 1px رنگی
  - **color**: پالت رنگی — 4 رنگ:
    - **Gray**: خنثی (#f6f8fa / #222323)
    - **Green**: موفقیت (#f1faf1 / #107c10)
    - **Orange**: هشدار (#fff9f5 / #f7630c)
    - **Red**: خطر (#fdf3f4 / #c50f1f)
  - **dismiss**: امکان حذف Tag — boolean
    - وقتی true: آیکن × در Tag نمایش داده می‌شود
    - وقتی false: هیچ عنصر حذف‌کننده‌ای نمایش داده نمی‌شود
  - **focus**: فوکوس‌پذیری — boolean
    - وقتی true: Tag می‌تواند فوکوس دریافت کند (tabindex="0")
    - وقتی false: Tag فوکوس‌پذیر نیست
  - **icon**: نمایش آیکن — boolean
    - وقتی true: آیکن در کنار متن نمایش داده می‌شود
    - وقتی false: فقط متن (و dismiss icon در صورت فعال بودن)
- **Visual Rules — Filled Style**:
  - پس‌زمینه رنگی بر اساس color + border 2px solid سفید (#ffffff)
  - Hover: پس‌زمینه کمی تیره‌تر
  - Focus: border 1px solid #222323 (جایگزین border سفید)
  - Disabled: bg #e7e9eb، بدون border، متن #bbbcbe
- **Visual Rules — Outline Style**:
  - بدون پس‌زمینه + border 1px solid رنگی (stroke/1)
  - Hover: border تیره‌تر (stroke/2) + متن تیره‌تر (برای رنگ‌های غیر gray)
  - Focus: border 1px solid #222323
  - Disabled: border #e7e9eb، متن #bbbcbe
- **Focus Ring**:
  - border 1px solid #222323 روی خود Tag
  - نباید باعث تغییر اندازه یا layout شود
  - فوکوس overlay state است و همزمان با rest یا hover فعال است
  - در حالت disabled فوکوس نمایش داده نمی‌شود
- **Layout Rules**:
  - ساختار کلی: [icon (optional)] [text] [dismiss icon (optional)]
  - تراز عمودی همه عناصر centered
  - فاصله بین عناصر: gap 4px (ثابت در همه سایزها)
  - جهت نمایش با RTL/LTR سازگار
- **State Priority**: disabled > focus > hover > rest
- **Behavior Notes**:
  - Tag منطق انتخاب، حذف یا تغییر state را در خودش نگه نمی‌دارد (فقط نمایشی)
  - تمام تغییرات state همزمان روی متن، آیکن‌ها، بوردر و پس‌زمینه اعمال می‌شوند
  - در حالت disabled، dismiss icon نمایش داده می‌شود اما قابل تعامل نیست
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از RTL/LTR

## Impact
- Affected specs: tag (new capability)
- **Dependencies**:
  - tokens.json (already created inside tag component)
- Affected code:
  - /components/tag/tag.css (new)
  - /components/tag/tokens.json (already created)
  - /components/tag/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + semantic HTML `<span>` / `<div>` elements
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <span class="tag tag--filled tag--gray tag--medium tag--rounded">
    <span class="tag__text">متن تگ</span>
  </span>
  ```
- **State Management**: CSS classes for style/color/size/radius + CSS pseudo-classes for hover/focus/disabled
- **Accessibility**: WCAG 2.1 Level AA (tabindex for focus, keyboard navigation, contrast)
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State Priority**: disabled > focus > hover > rest (بدون pressed)
2. **Disabled Rules**: هیچ state تعاملی نباید فعال شود؛ تمام عناصر داخلی استایل disabled داشته باشند
3. **Focus Overlay**: فوکوس لایه بصری اضافه، همزمان با rest یا hover، بدون تغییر layout
4. **Color × Style × State**: استایل نهایی از ترکیب سه‌گانه color + style + state به‌دست می‌آید
5. **Disabled Uniform**: در حالت disabled همه رنگ‌ها به نسخه خنثی (gray disabled) تبدیل می‌شوند
6. **Radius مستقل**: تغییر radius نباید روی padding، اندازه متن یا رفتار stateها اثر بگذارد
7. **Icon رنگ‌پذیر**: رنگ آیکن و dismiss icon دقیقا مانند رنگ متن Tag تبعیت می‌کند
8. **Size بر ابعاد اثر دارد**: ارتفاع، padding، font-size، line-height و اندازه آیکن
