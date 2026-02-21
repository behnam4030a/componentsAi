# Change: Add Radio Component (Pure CSS)

## Why
ساخت یک کامپوننت Radio قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. کامپوننت Radio برای انتخاب یک گزینه از بین چند گزینه‌ی انحصاری استفاده می‌شود. در هر گروه رادیویی، فقط یک Radio می‌تواند در حالت انتخاب‌شده باشد. این کامپوننت شامل کنترل دایره‌ای و در صورت نیاز Label متنی است.

## What Changes
- افزودن کامپوننت Radio به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 3 خصوصیت (Property):
  - **state**: وضعیت تعاملی/سیستمی — 5 حالت:
    - **Rest**: حالت پیش‌فرض
    - **Hover**: نشانگر روی ناحیه Radio یا Label
    - **Pressed**: هنگام کلیک یا فشردن (`:active`)
    - **Focus**: فوکوس با کیبورد یا کلیک — نمایش focus ring بدون تغییر layout
    - **Disabled**: غیرفعال — هیچ تعاملی مجاز نیست
  - **checked**: آیا Radio انتخاب شده — boolean
    - وقتی checked=true: نشانگر داخلی (inner dot) نمایش داده می‌شود
    - checked مستقل از stateهای تعاملی پایدار است
    - منطق Radio Group (فقط یک انتخاب) خارج از محدوده این کامپوننت
  - **label**: آیا Label متنی نمایش داده شود — boolean
    - وقتی true: متن Label در کنار کنترل نمایش، کلیک روی Label معادل کلیک Radio
    - وقتی false: فقط کنترل دایره‌ای نمایش داده می‌شود
- **Visual Rules — Control (Radio Circle)**:
  - دایره بیرونی (outer circle): 17px، border 1px solid
  - نشانگر داخلی (inner dot): 9px، دایره توپر — فقط در checked=true
  - استایل دایره و dot بر اساس ترکیب state × checked تغییر می‌کند
  - Unchecked: border رنگ‌های neutral stroke (#626364 → #59595a → #4f4f50)
  - Checked: border و dot رنگ‌های brand (#26a88c → #1d836d → #155e4e)
  - Disabled: هم دایره و هم dot رنگ #bbbcbe
- **Visual Rules — Label Styling**:
  - Label از state Radio تبعیت می‌کند (بدون state مستقل)
  - در حالت disabled: متن Label نیز رنگ disabled (#bbbcbe)
- **Focus Ring**:
  - border 1px solid #222323 روی wrapper با border-radius 4px
  - نباید باعث تغییر اندازه layout شود
- **Layout Rules**:
  - ساختار: [radio control] [label (optional)] (در RTL: control سمت راست، label سمت چپ)
  - فاصله: gap=2px، label padding-start=8px
  - تراز عمودی: center
  - سازگاری کامل RTL/LTR
- **State Priority**: disabled > pressed > focus > hover > rest
- **Interaction Notes**:
  - hover: روی کنترل یا Label فعال
  - focus: از طریق Tab یا کلیک
  - pressed: موقتی، بعد از رها شدن به rest/focus برمی‌گردد
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: radio (new capability)
- **Dependencies**:
  - tokens.json (already created inside radio component)
- Affected code:
  - /components/radio/radio.css (new)
  - /components/radio/tokens.json (already created)
  - /components/radio/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + native HTML `<input type="radio">` element
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <label class="radio">
    <input type="radio" class="radio__input" name="group" />
    <span class="radio__box">
      <span class="radio__circle">
        <span class="radio__dot"></span>
      </span>
    </span>
    <span class="radio__label">برچسب</span>
  </label>
  ```
- **State Management**: CSS-based (`:hover`, `:active`, `:focus-visible`, `:checked`, `:disabled`)
- **Accessibility**: WCAG 2.1 Level AA (focus ring, ARIA, keyboard navigation)
- **RTL Support**: Full support for Persian/Arabic text via flexbox
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State Priority**: disabled > pressed > focus > hover > rest
2. **Disabled Rules**: هیچ state تعاملی (hover/pressed/focus) نباید فعال شود؛ کلیک و انتخاب غیرمجاز
3. **Pressed موقتی**: فقط در زمان تعامل فعال، بعد از رها شدن به rest/focus برمی‌گردد
4. **Focus Ring**: با border مشخص، بدون تغییر layout
5. **checked مستقل**: وضعیت checked مستقل از stateهای تعاملی پایدار است
6. **Radio Group**: منطق گروه (فقط یک انتخاب) خارج از محدوده این کامپوننت
7. **Label تبعی**: Label نباید state مستقل داشته باشد و فقط از state Radio تبعیت می‌کند
8. **کلیک Label**: کلیک روی Label باید معادل کلیک روی خود Radio باشد
