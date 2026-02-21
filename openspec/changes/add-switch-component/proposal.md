# Change: Add Switch Component (Pure CSS)

## Why
ساخت یک کامپوننت Switch قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. سوئیچ به کاربران امکان می‌دهد بین دو گزینه منحصر به فرد متقابل (روشن/خاموش) یک گزینه را انتخاب کنند. فعال کردن سوئیچ باعث تغییر فوری می‌شود.

## What Changes
- افزودن کامپوننت Switch به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 2 خصوصیت (Property):
  - **state**: وضعیت تعاملی/سیستمی — 5 حالت:
    - **Rest**: حالت پیش‌فرض
    - **Hover**: نشانگر روی Switch قرار می‌گیرد
    - **Pressed**: هنگام کلیک یا فشردن (`:active`)
    - **Focus**: فوکوس با کیبورد یا کلیک — نمایش focus ring بدون تغییر layout
    - **Disabled**: غیرفعال — هیچ تعاملی مجاز نیست
  - **checked**: آیا Switch روشن است — boolean
    - وقتی checked=true: Thumb در موقعیت روشن (on)، Track با رنگ brand
    - وقتی checked=false: Thumb در موقعیت خاموش (off)، Track با رنگ neutral
    - checked مستقل از stateهای تعاملی پایدار است
- **Visual Rules — Track**:
  - Track پس‌زمینه اصلی Switch است
  - رنگ Track بر اساس ترکیب state × checked تغییر می‌کند
  - Checked: bg brand (#26a88c → #22967d → #19705e)، border (#eaf8f5)
  - Unchecked: bg neutral (#ffffff → #f6f8fa → #dddfe1)، border (#e2e4e6)
  - Disabled: bg (#f6f8fa)، border (#dddfe1) — تفاوت on/off همچنان قابل تشخیص
- **Visual Rules — Thumb**:
  - Thumb عنصر متحرک داخل Track است
  - موقعیت Thumb فقط به checked وابسته است (چپ/راست)
  - حاوی آیکن checkmark (checked) یا X (unchecked)
  - حرکت Thumb با transition تعریف می‌شود
  - Checked: circle border brand (#26a88c)، icon brand (#26a88c)
  - Unchecked: circle border neutral (#e2e4e6)، icon neutral (#59595a)
  - Disabled: circle bg (#e7e9eb)، circle border (#dddfe1)، icon (#bbbcbe)
- **Focus Ring**:
  - border 1px solid #222323 روی wrapper با border-radius 4px
  - نباید باعث تغییر اندازه layout شود
  - فوکوس لایه‌ی بصری اضافه است و رنگ/موقعیت Track و Thumb را override نمی‌کند
- **Focus Behavior (Non-Exclusive)**:
  - فوکوس می‌تواند همزمان با rest، hover و pressed فعال باشد
  - ترکیب‌های معتبر: rest+focus، hover+focus، pressed+focus
  - disabled همیشه فوکوس را حذف می‌کند
- **Layout Rules**:
  - Switch یک کامپوننت مستقل است و Label داخلی ندارد
  - در صورت نیاز به Label، از کامپوننت Label جداگانه کنار Switch استفاده شود
  - اندازه Track و Thumb ثابت است (از طریق design tokens)
- **State Priority**: disabled > pressed > focus > hover > rest
- **Interaction Notes**:
  - کلیک روی هر نقطه از Switch مقدار checked را تغییر می‌دهد
  - hover روی Track یا Thumb فعال می‌شود
  - pressed موقتی، بعد از رها شدن به rest/focus برمی‌گردد
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از RTL/LTR

## Impact
- Affected specs: switch (new capability)
- **Dependencies**:
  - tokens.json (already created inside switch component)
- Affected code:
  - /components/switch/switch.css (new)
  - /components/switch/tokens.json (already created)
  - /components/switch/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + native HTML `<input type="checkbox">` element (role="switch")
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <label class="switch">
    <input type="checkbox" class="switch__input" role="switch" />
    <span class="switch__track">
      <span class="switch__thumb">
        <span class="switch__icon"></span>
      </span>
    </span>
  </label>
  ```
- **State Management**: CSS-based (`:hover`, `:active`, `:focus-visible`, `:checked`, `:disabled`)
- **Accessibility**: WCAG 2.1 Level AA (role="switch", aria-checked, focus ring, keyboard navigation)
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State Priority**: disabled > pressed > focus > hover > rest
2. **Disabled Rules**: هیچ state تعاملی نباید فعال شود؛ تغییر checked غیرمجاز
3. **Pressed موقتی**: فقط در زمان تعامل فعال، بعد از رها شدن به rest/focus برمی‌گردد
4. **Focus Ring**: لایه بصری اضافه، بدون override رنگ Track/Thumb، بدون تغییر layout
5. **Focus Non-Exclusive**: همزمان با rest/hover/pressed فعال، فقط disabled آن را حذف می‌کند
6. **checked مستقل**: وضعیت checked مستقل از stateهای تعاملی پایدار است
7. **بدون Label داخلی**: Switch مستقل است و Label جداگانه استفاده شود
8. **Thumb Position**: موقعیت Thumb فقط به checked وابسته است نه به state
