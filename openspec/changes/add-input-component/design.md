# Design Document: Input Component

## Context
این کامپوننت Input بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Input برای دریافت متن کوتاه و آزاد از کاربر استفاده می‌شود. ظاهر و رفتار آن با state و size کنترل می‌شود و می‌تواند آیکن قبل/بعد از متن داشته باشد.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به کامپوننت Input دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript برای استایل‌دهی)
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- کامپوننت Input با 6 حالت تعاملی (Rest, Hover, Focused, Error, Disabled, ReadOnly)
- پشتیبانی از 3 سایز (Large, Medium, Small)
- آیکن قبل/بعد از متن با Icon Component
- Divider عمودی بین آیکن before و متن
- Accessible Indicator (خط پایینی) بر اساس state
- پشتیبانی کامل RTL
- Accessibility features (focus states, ARIA, keyboard navigation)
- استفاده از CSS custom properties برای theming
- API ساده: CSS classes + native HTML input

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- انیمیشن‌های پیچیده (فقط transition ساده)
- Input Group component (scope جداگانه)
- Textarea / Multi-line input (کامپوننت جداگانه)
- پشتیبانی از مرورگرهای قدیمی (IE11)
- Input masking یا formatting
- Floating label
- Helper text / Error message text (خارج از scope کامپوننت Input)

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Input
**Decision**: استفاده از `<input>` بومی HTML درون یک wrapper با CSS custom styling

**Rationale**:
- استفاده از رفتار بومی مرورگر برای `:focus`, `:disabled`, `[readonly]`
- Accessibility built-in (screen readers, keyboard navigation)
- سازگار با هر framework (React, Vue, Angular, vanilla HTML)
- مطابق الگوی Button و Checkbox component

**Alternatives Considered**:
- Custom div با contentEditable: مشکلات accessibility و cross-browser
- Web Components: over-engineering برای این use case

### 2. HTML Structure: Wrapper Pattern
**Decision**: استفاده از `<div>` wrapper با input بومی داخل آن

```html
<div class="input input--large">
  <div class="input__container">
    <span class="input__icon input__icon--before"><!-- Icon Component --></span>
    <span class="input__divider"></span>
    <input type="text" class="input__field" placeholder="متن نگهدارنده" />
    <span class="input__icon input__icon--after"><!-- Icon Component --></span>
  </div>
  <span class="input__indicator"></span>
</div>
```

**Rationale**:
- Container اصلی border, background و shadow را مدیریت می‌کند
- `input__container` المان داخلی flex است که آیکن‌ها و input را تراز می‌کند
- `input__field` استایل‌های پیش‌فرض مرورگر را reset می‌کند و فضای باقی‌مانده را پر می‌کند
- `input__indicator` خط پایینی مستقل از container
- `input__divider` خط عمودی بین آیکن before و فیلد متن

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables (custom properties) برای theming — مطابق الگوی Button و Checkbox

```css
:root {
  --input-color-neutral-fg-placeholder: #59595a;
  --input-color-neutral-fg-text: #222323;
  --input-color-neutral-stroke-rest: #e2e4e6;
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Button و Checkbox components
- امکان override کردن توسط developer
- Runtime theming support

### 4. State Management: CSS Pseudo-classes + Modifier Classes
**Decision**: ترکیب pseudo-classes بومی CSS و modifier classes

**State Mapping**:
- Rest: `.input` (default)
- Hover: `.input:hover` (با شرط عدم disabled/readonly)
- Focused: `.input:focus-within` (وقتی `input__field` فوکوس دارد)
- Error: `.input.input--error`
- Disabled: `.input:has(.input__field:disabled)` + `.input--disabled` (fallback)
- ReadOnly: `.input:has(.input__field[readonly])` + `.input--readonly` (fallback)

**Priority Order** (CSS specificity handles this):
1. **Disabled**: غیرفعال، هیچ تعاملی — pointer-events: none
2. **Error**: خطا — border قرمز، background صورتی، shadow قرمز
3. **Focused**: فوکوس — border سبز، shadow سبز، indicator سبز
4. **Hover**: هاور — border تیره‌تر، indicator خاکستری
5. **Rest**: پیش‌فرض — border خاکستری

**Rationale**:
- `:focus-within` روی container اعمال می‌شود وقتی input داخلی فوکوس دارد
- `[readonly]` و `:disabled` attribute selectors بومی هستند
- `.input--error` class توسط form validation منطقی set می‌شود
- `:has()` selector برای propagate کردن state از input به container (با class fallback برای مرورگرهایی که پشتیبانی نمی‌کنند)

### 5. Icon Integration: Icon Component Slots
**Decision**: آیکن‌ها در slot‌های مشخص (`input__icon--before` و `input__icon--after`) با Icon Component قرار می‌گیرند

**Rationale**:
- Input فقط جایگذاری آیکن و فاصله/تراز را کنترل می‌کند
- شکل آیکن از Icon Component می‌آید
- رنگ آیکن با `color` inheritance از parent تعیین می‌شود (مطابق state)
- اندازه آیکن با mapping از Input.size:
  - Large → icon: 20px
  - Medium → icon: 20px
  - Small → icon: 16px

### 6. Accessible Indicator (Bottom Line)
**Decision**: خط پایینی (1.5px) به عنوان المان مستقل (`input__indicator`) که بر اساس state تغییر می‌کند

**State Mapping**:
- Rest: مخفی (opacity: 0)
- Hover: قابل مشاهده (#c0c1c3)
- Focused: قابل مشاهده (#2abb9c)
- Error/Disabled/ReadOnly: مخفی

**Rationale**:
- مطابق طراحی Figma
- المان مستقل برای کنترل بهتر
- Transition نرم برای نمایش/مخفی شدن

### 7. Divider Between Icon and Text
**Decision**: یک المان `input__divider` به صورت خط عمودی بین `input__icon--before` و فیلد متن

**Rationale**:
- فقط وقتی `beforeTextIcon` وجود دارد نمایش داده می‌شود
- ارتفاع وابسته به size: Large=16px, Medium=12px, Small=8px
- رنگ: مطابق stroke rest
- در DOM، بعد از `input__icon--before` و قبل از `input__field` قرار می‌گیرد

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier) — مطابق الگوی Button و Checkbox:

```css
.input { }                       /* Block */
.input__container { }            /* Element: inner flex container */
.input__field { }                /* Element: native input */
.input__icon { }                 /* Element: icon wrapper */
.input__icon--before { }         /* Modifier: before text icon */
.input__icon--after { }          /* Modifier: after text icon */
.input__divider { }              /* Element: vertical divider */
.input__indicator { }            /* Element: bottom accessible indicator */

.input--large { }                /* Modifier: Size */
.input--medium { }
.input--small { }

.input--error { }                /* Modifier: Error state */
.input--disabled { }             /* Modifier: Disabled fallback */
.input--readonly { }             /* Modifier: ReadOnly fallback */
```

## CSS API (Usage)

### Classes
```html
<!-- Basic Large Input -->
<div class="input input--large">
  <div class="input__container">
    <input type="text" class="input__field" placeholder="متن نگهدارنده" />
  </div>
  <span class="input__indicator"></span>
</div>

<!-- With Before Icon + Divider -->
<div class="input input--large">
  <div class="input__container">
    <span class="input__icon input__icon--before"><!-- Icon Component --></span>
    <span class="input__divider"></span>
    <input type="text" class="input__field" placeholder="متن نگهدارنده" />
  </div>
  <span class="input__indicator"></span>
</div>

<!-- With Both Icons -->
<div class="input input--medium">
  <div class="input__container">
    <span class="input__icon input__icon--before"><!-- Icon Component --></span>
    <span class="input__divider"></span>
    <input type="text" class="input__field" placeholder="متن نگهدارنده" />
    <span class="input__icon input__icon--after"><!-- Icon Component --></span>
  </div>
  <span class="input__indicator"></span>
</div>

<!-- Error State -->
<div class="input input--large input--error">
  <div class="input__container">
    <input type="text" class="input__field" placeholder="متن نگهدارنده" />
  </div>
  <span class="input__indicator"></span>
</div>

<!-- Disabled -->
<div class="input input--large">
  <div class="input__container">
    <input type="text" class="input__field" placeholder="متن نگهدارنده" disabled />
  </div>
  <span class="input__indicator"></span>
</div>

<!-- ReadOnly -->
<div class="input input--large">
  <div class="input__container">
    <input type="text" class="input__field" value="متن فقط‌خواندنی" readonly />
  </div>
  <span class="input__indicator"></span>
</div>
```

## Accessibility Requirements

### ARIA Attributes
```html
<div class="input input--large" role="group">
  <div class="input__container">
    <input type="text" class="input__field"
      placeholder="متن نگهدارنده"
      aria-label="توضیح فیلد"
      aria-invalid="false"
    />
  </div>
  <span class="input__indicator"></span>
</div>

<!-- Error state -->
<div class="input input--large input--error" role="group">
  <div class="input__container">
    <input type="text" class="input__field"
      aria-invalid="true"
      aria-describedby="error-msg"
    />
  </div>
  <span class="input__indicator"></span>
</div>
```

### Keyboard Navigation
- **Tab**: Navigate to/from input field (native browser behavior)
- **Typing**: Enter text (native behavior)
- **Select All** (Ctrl+A): Select text in field

### Color Contrast
- تمام ترکیب‌های رنگ باید WCAG 2.1 Level AA را رعایت کنند
- حداقل contrast ratio 4.5:1 برای متن
- placeholder text باید حداقل 3:1 contrast ratio داشته باشد

## File Structure

```
/components/input/
├── input.css          # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```

## Risks / Trade-offs

### Risk 1: `:has()` Browser Support
**Risk**: CSS `:has()` selector در برخی مرورگرهای قدیمی‌تر پشتیبانی نمی‌شود

**Mitigation**:
- استفاده از modifier classes (`.input--disabled`, `.input--readonly`) به عنوان fallback
- مستندسازی واضح نحوه استفاده از هر دو روش
- Modern browsers target (Chrome 105+, Firefox 121+, Safari 15.4+) همگی `:has()` را پشتیبانی می‌کنند

### Risk 2: Custom Input Styling Cross-Browser
**Risk**: Reset کردن استایل‌های پیش‌فرض input در مرورگرهای مختلف ممکن است متفاوت باشد

**Mitigation**:
- استفاده از CSS reset کامل برای `input__field`
- تست در مرورگرهای هدف
- `appearance: none` برای حذف استایل‌های بومی

### Risk 3: Placeholder Color Cross-Browser
**Risk**: `::placeholder` pseudo-element ممکن است در مرورگرهای مختلف متفاوت رفتار کند

**Mitigation**:
- استفاده از `::placeholder` استاندارد (پشتیبانی خوب در مرورگرهای مدرن)
- تعیین صریح `opacity: 1` برای placeholder (Firefox default opacity < 1)

### Risk 4: Error State Needs External Logic
**Risk**: حالت Error توسط CSS pseudo-class مدیریت نمی‌شود و نیاز به اضافه کردن class توسط JavaScript/framework دارد

**Mitigation**:
- مستندسازی واضح نحوه set/remove کردن `.input--error` class
- سازگاری با HTML5 validation (`input:invalid` به عنوان extension ممکن)

## Migration Plan

### Phase 1: Initial Implementation
1. ساخت CSS component
2. تست در demo page
3. مستندسازی

### Phase 2: Integration
1. استفاده در یک feature واقعی
2. جمع‌آوری feedback
3. رفع bugs و بهبودها

### Phase 3: Expansion
1. افزودن Textarea component (در صورت نیاز)
2. افزودن dark theme support
3. افزودن Input Group / Form Field wrapper (label + input + error message)
