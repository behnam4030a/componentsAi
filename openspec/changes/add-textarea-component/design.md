# Design Document: Textarea Component

## Context
این کامپوننت Textarea بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Textarea برای دریافت متن چندخطی و آزاد از کاربر استفاده می‌شود (مانند نظر، توضیحات، پیام). ظاهر و رفتار آن با state و size کنترل می‌شود و می‌تواند قابلیت resize داشته باشد.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به کامپوننت Textarea دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript برای استایل‌دهی)
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد
- قوانین Typography و Placeholder مشابه کامپوننت Input

## Goals / Non-Goals

### Goals
- کامپوننت Textarea با 6 حالت تعاملی (Rest, Hover, Focused, Error, Disabled, ReadOnly)
- پشتیبانی از 3 سایز (Large, Medium, Small)
- قابلیت Resize Handler (فعال/غیرفعال) با تغییر اندازه عمودی
- Accessible Indicator (خط پایینی) بر اساس state
- پشتیبانی کامل RTL
- Accessibility features (focus states, ARIA, keyboard navigation)
- استفاده از CSS custom properties برای theming
- API ساده: CSS classes + native HTML textarea

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- انیمیشن‌های پیچیده (فقط transition ساده)
- پشتیبانی از مرورگرهای قدیمی (IE11)
- Character counter / Word counter
- Auto-resize (auto-grow) based on content
- Helper text / Error message text (خارج از scope کامپوننت Textarea)

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Textarea
**Decision**: استفاده از `<textarea>` بومی HTML درون یک wrapper با CSS custom styling

**Rationale**:
- استفاده از رفتار بومی مرورگر برای `:focus`, `:disabled`, `[readonly]`, multi-line
- Accessibility built-in (screen readers, keyboard navigation)
- سازگار با هر framework (React, Vue, Angular, vanilla HTML)
- مطابق الگوی Input component

**Alternatives Considered**:
- Custom div با contentEditable: مشکلات accessibility و cross-browser
- Web Components: over-engineering برای این use case

### 2. HTML Structure: Wrapper Pattern
**Decision**: استفاده از `<div>` wrapper با textarea بومی داخل آن

```html
<div class="textarea textarea--large">
  <div class="textarea__container">
    <textarea class="textarea__field" placeholder="متن نگهدارنده"></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>
```

**Rationale**:
- Wrapper اصلی (`textarea`) مسئول border-radius و overflow clip — در حالت Error، outer border روی wrapper اعمال می‌شود
- `textarea__container` المان داخلی که border، background و padding را مدیریت می‌کند
- `textarea__field` استایل‌های پیش‌فرض مرورگر را reset می‌کند و فضای کامل را پر می‌کند
- `textarea__indicator` خط پایینی مستقل از container
- Resize handler توسط مرورگر (CSS `resize: vertical`) مدیریت می‌شود

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables (custom properties) برای theming — مطابق الگوی Input

```css
:root {
  --textarea-color-neutral-fg-placeholder: #59595a;
  --textarea-color-neutral-fg-text: #222323;
  --textarea-color-neutral-stroke-rest: #e2e4e6;
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Input و Button و سایر components
- امکان override کردن توسط developer
- Runtime theming support

### 4. State Management: CSS Pseudo-classes + Modifier Classes
**Decision**: ترکیب pseudo-classes بومی CSS و modifier classes

**State Mapping**:
- Rest: `.textarea` (default)
- Hover: `.textarea:hover` (با شرط عدم disabled/readonly)
- Focused: `.textarea:focus-within` (وقتی `textarea__field` فوکوس دارد)
- Error: `.textarea.textarea--error`
- Disabled: `.textarea:has(.textarea__field:disabled)` + `.textarea--disabled` (fallback)
- ReadOnly: `.textarea:has(.textarea__field[readonly])` + `.textarea--readonly` (fallback)

**Priority Order** (CSS specificity handles this):
1. **Disabled**: غیرفعال، هیچ تعاملی — pointer-events: none
2. **Error**: خطا — outer border قرمز، inner border عادی، background صورتی
3. **Focused**: فوکوس — shadow سبز، indicator سبز
4. **Hover**: هاور — border تیره‌تر، indicator خاکستری
5. **Rest**: پیش‌فرض — border خاکستری

**Rationale**:
- `:focus-within` روی container اعمال می‌شود وقتی textarea داخلی فوکوس دارد
- `[readonly]` و `:disabled` attribute selectors بومی هستند
- `.textarea--error` class توسط form validation منطقی set می‌شود
- `:has()` selector برای propagate کردن state از textarea به container

### 5. Error State: Double Border Pattern
**Decision**: در حالت Error، wrapper بیرونی border قرمز (#c50f1f) و container داخلی border عادی (#e2e4e6) دارد

**Rationale**:
- مطابق طراحی Figma — Error state در Textarea با Input متفاوت است
- Wrapper بیرونی outer border قرمز دارد
- Container داخلی همچنان border عادی خودش را حفظ می‌کند
- background صورتی (#fdf3f4) روی container داخلی اعمال می‌شود

### 6. Resize Handler
**Decision**: استفاده از CSS `resize` property بومی مرورگر

**Rationale**:
- `resize: vertical` برای فعال کردن تغییر اندازه فقط عمودی
- `resize: none` برای غیرفعال کردن
- مرورگرها به صورت پیش‌فرض هندل resize را نمایش می‌دهند
- در حالت disabled، `resize: none` اعمال می‌شود
- سازگار با CSS classes: `.textarea--resizable` (یا مشابه)

### 7. Accessible Indicator (Bottom Line)
**Decision**: خط پایینی (1.5px) به عنوان المان مستقل (`textarea__indicator`) که بر اساس state تغییر می‌کند

**State Mapping**:
- Rest: مخفی (opacity: 0)
- Hover: قابل مشاهده (#59595a)
- Focused: قابل مشاهده (#2abb9c)
- Error/Disabled/ReadOnly: مخفی

**Rationale**:
- مطابق طراحی Figma
- المان مستقل برای کنترل بهتر
- Transition نرم برای نمایش/مخفی شدن

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier) — مطابق الگوی Input:

```css
.textarea { }                      /* Block */
.textarea__container { }           /* Element: inner flex container */
.textarea__field { }               /* Element: native textarea */
.textarea__indicator { }           /* Element: bottom accessible indicator */

.textarea--large { }               /* Modifier: Size */
.textarea--medium { }
.textarea--small { }

.textarea--error { }               /* Modifier: Error state */
.textarea--disabled { }            /* Modifier: Disabled fallback */
.textarea--readonly { }            /* Modifier: ReadOnly fallback */
.textarea--resizable { }           /* Modifier: Resize enabled */
```

## CSS API (Usage)

### Classes
```html
<!-- Basic Large Textarea -->
<div class="textarea textarea--large">
  <div class="textarea__container">
    <textarea class="textarea__field" placeholder="متن نگهدارنده"></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>

<!-- With Resize Handler -->
<div class="textarea textarea--large textarea--resizable">
  <div class="textarea__container">
    <textarea class="textarea__field" placeholder="متن نگهدارنده"></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>

<!-- Error State -->
<div class="textarea textarea--large textarea--error">
  <div class="textarea__container">
    <textarea class="textarea__field" placeholder="متن نگهدارنده"></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>

<!-- Disabled -->
<div class="textarea textarea--large">
  <div class="textarea__container">
    <textarea class="textarea__field" placeholder="متن نگهدارنده" disabled></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>

<!-- ReadOnly -->
<div class="textarea textarea--large">
  <div class="textarea__container">
    <textarea class="textarea__field" readonly>متن فقط‌خواندنی</textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>
```

## Accessibility Requirements

### ARIA Attributes
```html
<div class="textarea textarea--large" role="group">
  <div class="textarea__container">
    <textarea class="textarea__field"
      placeholder="متن نگهدارنده"
      aria-label="توضیح فیلد"
      aria-invalid="false"
    ></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>

<!-- Error state -->
<div class="textarea textarea--large textarea--error" role="group">
  <div class="textarea__container">
    <textarea class="textarea__field"
      aria-invalid="true"
      aria-describedby="error-msg"
    ></textarea>
  </div>
  <span class="textarea__indicator"></span>
</div>
```

### Keyboard Navigation
- **Tab**: Navigate to/from textarea field (native browser behavior)
- **Typing**: Enter text (native behavior)
- **Enter**: New line (native textarea behavior)
- **Select All** (Ctrl+A): Select text in field

### Color Contrast
- تمام ترکیب‌های رنگ باید WCAG 2.1 Level AA را رعایت کنند
- حداقل contrast ratio 4.5:1 برای متن
- placeholder text باید حداقل 3:1 contrast ratio داشته باشد

## File Structure

```
/components/textarea/
├── textarea.css       # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```

## Risks / Trade-offs

### Risk 1: `:has()` Browser Support
**Risk**: CSS `:has()` selector در برخی مرورگرهای قدیمی‌تر پشتیبانی نمی‌شود

**Mitigation**:
- استفاده از modifier classes (`.textarea--disabled`, `.textarea--readonly`) به عنوان fallback
- Modern browsers target (Chrome 105+, Firefox 121+, Safari 15.4+) همگی `:has()` را پشتیبانی می‌کنند

### Risk 2: Custom Textarea Styling Cross-Browser
**Risk**: Reset کردن استایل‌های پیش‌فرض textarea در مرورگرهای مختلف ممکن است متفاوت باشد

**Mitigation**:
- استفاده از CSS reset کامل برای `textarea__field`
- تست در مرورگرهای هدف
- `appearance: none` برای حذف استایل‌های بومی

### Risk 3: Resize Handler Styling
**Risk**: هندل resize بومی مرورگر قابل سفارشی‌سازی محدود است

**Mitigation**:
- استفاده از CSS `resize: vertical` بومی مرورگر
- در صورت نیاز به سفارشی‌سازی بیشتر، می‌توان از custom resize handle با JavaScript استفاده کرد (خارج از scope فعلی)

### Risk 4: Placeholder Color Cross-Browser
**Risk**: `::placeholder` pseudo-element ممکن است در مرورگرهای مختلف متفاوت رفتار کند

**Mitigation**:
- استفاده از `::placeholder` استاندارد
- تعیین صریح `opacity: 1` برای placeholder (Firefox default opacity < 1)

### Risk 5: Error State Needs External Logic
**Risk**: حالت Error توسط CSS pseudo-class مدیریت نمی‌شود و نیاز به JavaScript/framework دارد

**Mitigation**:
- مستندسازی واضح نحوه set/remove کردن `.textarea--error` class

## Migration Plan

### Phase 1: Initial Implementation
1. ساخت CSS component
2. تست در demo page
3. مستندسازی

### Phase 2: Integration
1. استفاده در یک feature واقعی
2. جمع‌آوری feedback
3. رفع bugs و بهبودها
