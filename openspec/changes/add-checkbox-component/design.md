# Design Document: Checkbox Component

## Context
این کامپوننت Checkbox بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Checkbox یک کامپوننت انتخاب سه‌حالته (Unchecked، Checked، Indeterminate) است که از design tokens استخراج شده از Figma استفاده می‌کند.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به کامپوننت Checkbox دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (JavaScript فقط برای indeterminate state)
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- کامپوننت Checkbox با 3 وضعیت منطقی (Unchecked، Checked، Indeterminate)
- پشتیبانی از 5 حالت تعاملی (Rest، Hover، Pressed، Focused، Disabled)
- پشتیبانی از 2 سایز (Large، Medium)
- Label اختیاری با قابلیت کلیک برای تغییر Status
- پشتیبانی کامل RTL
- Accessibility features (focus ring، ARIA، keyboard navigation)
- استفاده از CSS custom properties برای theming
- API ساده: CSS classes + native HTML checkbox

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- انیمیشن‌های پیچیده (فقط transition ساده)
- Checkbox Group component (scope جداگانه)
- پشتیبانی از مرورگرهای قدیمی (IE11)
- Select All logic (فقط visual state ارائه می‌شود)

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Checkbox
**Decision**: استفاده از `<input type="checkbox">` بومی HTML با CSS custom styling

**Rationale**:
- استفاده از رفتار بومی مرورگر برای `:checked` و `:disabled`
- بدون نیاز به JavaScript برای toggle بین Checked و Unchecked
- Accessibility built-in (screen readers، keyboard navigation)
- سازگار با هر framework (React، Vue، Angular، vanilla HTML)

**Alternatives Considered**:
- Custom div با JavaScript toggle: پیچیده‌تر، مشکلات accessibility
- Web Components: over-engineering برای این use case

### 2. HTML Structure: Label Wrapping Pattern
**Decision**: استفاده از `<label>` به عنوان wrapper اصلی

```html
<label class="checkbox checkbox--large">
  <input type="checkbox" class="checkbox__input" />
  <span class="checkbox__box">
    <span class="checkbox__icon"><!-- checkmark/minus SVG --></span>
  </span>
  <span class="checkbox__label">برچسب</span>
</label>
```

**Rationale**:
- کلیک روی Label به طور بومی input را toggle می‌کند
- بدون نیاز به `for`/`id` matching
- ساختار ساده و semantic

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables (custom properties) برای theming

```css
:root {
  --checkbox-color-brand-bg-rest: #26a88c;
  --checkbox-color-brand-bg-hover: #22967d;
  --checkbox-color-brand-bg-pressed: #19705e;
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Button component
- امکان override کردن توسط developer
- Runtime theming support

### 4. Hiding Native Checkbox: Visually Hidden Pattern
**Decision**: مخفی کردن input بومی با `visually-hidden` technique (نه `display: none`)

```css
.checkbox__input {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

**Rationale**:
- Screen readers هنوز input را می‌خوانند
- `:focus-visible` روی input کار می‌کند
- `:checked` pseudo-class قابل استفاده است

### 5. Indeterminate State Handling
**Decision**: حالت Indeterminate با CSS class و JavaScript property

**Rationale**:
- HTML attribute `indeterminate` وجود ندارد — فقط JavaScript property
- CSS pseudo-class `:indeterminate` کار می‌کند وقتی property از طریق JS ست شود
- یک CSS class `.checkbox--indeterminate` هم برای fallback ارائه می‌شود

```javascript
// Required for indeterminate
document.querySelector('.checkbox__input').indeterminate = true;
```

### 6. State Management: CSS Pseudo-classes + Sibling Selectors
**Decision**: استفاده از state های input برای استایل‌دهی box

**State Mapping**:
- Unchecked Rest: `.checkbox__input:not(:checked):not(:indeterminate) ~ .checkbox__box`
- Checked Rest: `.checkbox__input:checked ~ .checkbox__box`
- Indeterminate: `.checkbox__input:indeterminate ~ .checkbox__box`
- Hover: `.checkbox:hover .checkbox__box`
- Pressed: `.checkbox:active .checkbox__box`
- Focused: `.checkbox__input:focus-visible ~ .checkbox__box`
- Disabled: `.checkbox__input:disabled ~ .checkbox__box`

**Priority Order** (CSS specificity):
1. **Disabled**: غیرفعال، هیچ تعاملی — hover/pressed/focus نباید فعال شوند
2. **Focused**: حلقه فوکوس خارجی (لایه اضافی، مستقل)
3. **Pressed** (`:active`): هنگام mousedown
4. **Hover** (`:hover`): هنگام hover
5. **Rest**: پیش‌فرض

### 7. Icon Implementation: Inline SVG
**Decision**: آیکون‌های checkmark و minus به صورت inline SVG

**Rationale**:
- رنگ آیکن با `currentColor` قابل تغییر
- بدون HTTP request اضافی
- Performance بهتر از image

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier) — مطابق الگوی Button:

```css
.checkbox { }                    /* Block */
.checkbox__input { }             /* Element: native input (hidden) */
.checkbox__box { }               /* Element: visual checkbox box */
.checkbox__icon { }              /* Element: checkmark/minus icon */
.checkbox__label { }             /* Element: label text */

.checkbox--large { }             /* Modifier: Size */
.checkbox--medium { }

.checkbox--disabled { }          /* Modifier: State */
.checkbox--indeterminate { }     /* Modifier: Indeterminate fallback */
```

## CSS API (Usage)

### Classes
```html
<!-- Base (Large, with label) -->
<label class="checkbox checkbox--large">
  <input type="checkbox" class="checkbox__input" />
  <span class="checkbox__box">
    <svg class="checkbox__icon">...</svg>
  </span>
  <span class="checkbox__label">برچسب</span>
</label>

<!-- Medium, without label -->
<label class="checkbox checkbox--medium">
  <input type="checkbox" class="checkbox__input" />
  <span class="checkbox__box">
    <svg class="checkbox__icon">...</svg>
  </span>
</label>

<!-- Disabled -->
<label class="checkbox checkbox--large checkbox--disabled">
  <input type="checkbox" class="checkbox__input" disabled />
  <span class="checkbox__box">
    <svg class="checkbox__icon">...</svg>
  </span>
  <span class="checkbox__label">غیرفعال</span>
</label>

<!-- Checked -->
<label class="checkbox checkbox--large">
  <input type="checkbox" class="checkbox__input" checked />
  <span class="checkbox__box">
    <svg class="checkbox__icon">...</svg>
  </span>
  <span class="checkbox__label">انتخاب شده</span>
</label>
```

## Accessibility Requirements

### ARIA Attributes
```html
<!-- Indeterminate requires aria-checked="mixed" -->
<label class="checkbox checkbox--large">
  <input type="checkbox" class="checkbox__input" aria-checked="mixed" />
  <span class="checkbox__box">...</span>
  <span class="checkbox__label">برچسب</span>
</label>
```

### Keyboard Navigation
- **Space**: Toggle checkbox (native browser behavior)
- **Tab**: Navigate to next focusable element
- **Shift+Tab**: Navigate to previous element

### Focus Visible
- نمایش focus ring فقط در keyboard navigation
- استفاده از `:focus-visible` pseudo-class
- Focus ring: 1px solid `#222323` روی container خارجی

### Color Contrast
- تمام ترکیب‌های رنگ باید WCAG 2.1 Level AA را رعایت کنند
- حداقل contrast ratio 4.5:1 برای متن label

## File Structure

```
/components/checkbox/
├── checkbox.css         # Component styles (pure CSS)
├── index.html           # Demo page
└── tokens.json          # Design tokens (already created)
```

## Risks / Trade-offs

### Risk 1: Indeterminate Requires JavaScript
**Risk**: حالت Indeterminate فقط از طریق JavaScript property قابل تنظیم است

**Mitigation**:
- مستندسازی واضح نحوه استفاده
- ارائه مثال JavaScript در demo page
- CSS class `.checkbox--indeterminate` به عنوان fallback

### Risk 2: Custom Checkbox Styling Cross-Browser
**Risk**: مخفی کردن و re-style کردن native checkbox ممکن است در بعضی مرورگرها متفاوت باشد

**Mitigation**:
- استفاده از `visually-hidden` pattern اثبات شده
- تست در مرورگرهای هدف

### Risk 3: RTL Label Positioning
**Risk**: موقعیت label نسبت به box در RTL ممکن است نیاز به توجه خاص داشته باشد

**Mitigation**:
- استفاده از CSS flexbox با `row-reverse` یا logical properties
- در Figma design، label در سمت راست box قرار دارد (RTL default)

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
1. افزودن Checkbox Group component (در صورت نیاز)
2. افزودن dark theme support
3. افزودن animation/transition effects
