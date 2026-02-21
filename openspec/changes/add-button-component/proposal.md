# Change: Add Button Component (Pure CSS)

## Why
ساخت یک کامپوننت Button قابل استفاده مجدد با CSS برای استفاده در سیستم طراحی FrontLayer EsanjUiKit. این کامپوننت باید از design tokens استخراج شده از Figma پیروی کند و تمام انواع، سایزها و حالت‌های تعریف شده در UI Kit را پشتیبانی نماید.

## What Changes
- افزودن کامپوننت Button به صورت Pure CSS (بدون JavaScript)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- **پشتیبانی از لینک‌ها**: علاوه بر `<button>` elements، از `<a>` elements هم پشتیبانی می‌کند تا لینک‌هایی با ظاهر دکمه ایجاد شوند
- پشتیبانی از 6 نوع دکمه: Primary, AI, Secondary, Subtle, Outline, Transparent
  - type فقط استایل (رنگ، بک‌گراند، border، shadow) را تغییر می‌دهد، نه ساختار
  - همه typeها در همه sizeها قابل استفاده
- پشتیبانی از 3 سایز: Large (45px), Medium (37px), Small (24px)
  - size روی height, padding, font, gap, icon size تاثیر می‌گذارد
- پشتیبانی از 4 state با CSS pseudo-classes:
  - Rest (پیش‌فرض)
  - Hover (`:hover`)
  - Pressed (`:active`)
  - Selected (`.btn--selected`)
- **Icon Integration** (با inline SVG یا Icon Component):
  - استفاده از ساختار HTML: `<span class="btn__icon">` + `<span class="btn__text">`
  - Color inheritance: رنگ آیکن از `currentColor`
  - RTL/LTR positioning: با CSS flexbox و `direction`
- Focus Management:
  - Focus ring خارج از مرز (no layout shift)
  - فقط در keyboard navigation (`:focus-visible`)
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: button (new capability)
- **Dependencies**:
  - tokens.json (already created inside button component)
- Affected code:
  - /components/button/button.css (new)
  - /components/button/tokens.json (already created - specific to button)

## Technical Details
- **Technology Stack**: CSS3 (بدون JavaScript)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**: `<button class="btn btn--primary btn--large">متن</button>`
- **Icon Integration**: Inline SVG داخل `<span class="btn__icon">`
- **Accessibility**: WCAG 2.1 Level AA (focus states, ARIA attributes, color contrast 4.5:1)
- **RTL Support**: Full support for Persian/Arabic text via CSS `direction` and logical properties
- **State Management**: CSS-based (`:hover`, `:active`, `:focus-visible`, `.btn--selected`, `.btn--disabled`)
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **Type Constraint**: type فقط styling را تغییر می‌دهد (NOT structure)
2. **State Rules**: hover و pressed با CSS pseudo-classes، selected با CSS class
3. **Icon Integration**: آیکون‌ها با inline SVG یا Icon Component در ساختار HTML
4. **Focus Independence**: focus مستقل از state و خارج از boundary
5. **Size Effects**: size باید height, padding, font, gap, icon size را تغییر دهد
