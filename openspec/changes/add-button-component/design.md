# Design Document: Button Component

## Context
این کامپوننت Button بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. هدف اصلی ایجاد یک کامپوننت سبک، قابل استفاده مجدد و بدون نیاز به JavaScript است که design tokens را از Figma دریافت کرده و مطابق با UI Kit طراحی شده باشد.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به کامپوننت Button دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- باید فقط با CSS پیاده‌سازی شود (بدون JavaScript)
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- ✅ کامپوننت Button با 6 variant (Primary, AI, Secondary, Subtle, Outline, Transparent)
- ✅ پشتیبانی از 3 size (Large, Medium, Small)
- ✅ مدیریت 4 state (Rest, Hover, Pressed, Selected) با CSS
- ✅ قابلیت افزودن icon قبل/بعد از متن با inline HTML
- ✅ پشتیبانی کامل RTL
- ✅ Accessibility features (focus ring, ARIA, keyboard navigation)
- ✅ استفاده از CSS custom properties برای theming
- ✅ API ساده: فقط CSS classes

### Non-Goals
- ❌ پشتیبانی از Dark theme (فعلاً فقط Light theme)
- ❌ انیمیشن‌های پیچیده (فقط transition ساده)
- ❌ Loading state with spinner (می‌تواند در آینده اضافه شود)
- ❌ Button group component (scope جداگانه)
- ❌ پشتیبانی از مرورگرهای قدیمی (IE11)
- ❌ JavaScript API (pure CSS approach)

## Decisions

### 1. Architecture Pattern: Pure CSS Component
**Decision**: استفاده از CSS classes (BEM) بدون JavaScript

**Rationale**:
- سبک‌ترین approach ممکن (صفر KB JavaScript)
- مشابه Bootstrap و سایر CSS frameworks
- بدون نیاز به initialization یا DOM manipulation
- سازگار با هر framework (React, Vue, Angular, vanilla HTML)
- عملکرد بهتر (بدون runtime JS overhead)

**Alternatives Considered**:
- ES6 Class با auto-initialization: پیچیده‌تر، overhead بیشتر
- Web Components: over-engineering برای این use case

### 2. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables (custom properties) برای theming

**Rationale**:
- امکان override کردن توسط developer
- Runtime theming support
- سازگاری با design tokens
- Performance خوب

Example:
```css
:root {
  --button-color-brand-bg-rest: #26a88c;
  --button-color-brand-bg-hover: #22967d;
  /* ... */
}
```

### 3. Icon Implementation: Inline HTML Structure
**Decision**: آیکن‌ها با ساختار HTML inline (SVG یا Icon Component)

**Rationale**:
- بدون نیاز به JavaScript برای inject کردن آیکن
- کنترل کامل developer روی icon
- رنگ آیکن با `currentColor` از دکمه inherit می‌شود

```html
<button class="btn btn--primary btn--medium">
  <span class="btn__inner">
    <span class="btn__icon"><svg>...</svg></span>
    <span class="btn__text">متن دکمه</span>
  </span>
</button>
```

### 4. RTL Support: CSS Logical Properties + dir attribute
**Decision**: استفاده از CSS logical properties و HTML `dir` attribute

**Rationale**:
- پشتیبانی بهتر از RTL/LTR
- کاهش کد CSS
- استاندارد مدرن

### 5. State Management: CSS Pseudo-classes
**Decision**: استفاده از CSS pseudo-classes و modifier classes

**State Mapping**:
- Rest: `.btn` (default)
- Hover: `.btn:hover`
- Pressed: `.btn:active`
- Selected: `.btn.btn--selected`
- Disabled: `.btn.btn--disabled` + `disabled` attribute
- Focus: `.btn:focus-visible`

**Rationale**:
- بدون JavaScript
- عملکرد بومی مرورگر
- رفتار قابل پیش‌بینی

### 6. State Combination Rules
**Priority Order** (CSS specificity handles this):
1. **Disabled**: غیرفعال، هیچ تعاملی
2. **Pressed** (`:active`): هنگام mousedown
3. **Selected + Hover**: ترکیب `.btn--selected:hover`
4. **Hover** (`:hover`): هنگام hover
5. **Selected**: `.btn--selected`
6. **Focus**: لایه اضافی با `:focus-visible`
7. **Rest**: پیش‌فرض

## Important Constraints from Design System

### Type Constraints
- `type` فقط باید روی **styling** تاثیر بگذارد (color, background, border, shadow)
- `type` نباید **structure** را تغییر دهد (padding, radius, typography)
- همه typeها باید در همه sizeها کار کنند

### Size Effects
Size باید روی موارد زیر تاثیر بگذارد:
- ارتفاع دکمه (height)
- padding افقی/عمودی
- اندازه فونت (font-size) و line-height
- فاصله بین آیکن و متن (gap)
- اندازه آیکن (icon size)

### Icon Rules
- رنگ آیکن = رنگ متن (`currentColor`)
- جایگاه آیکن بر اساس RTL/LTR (CSS flexbox handles this)
- Icon-only button: padding مساوی طبق design system

### Focus Rules
- focus یک حالت **مستقل** از state است
- focus ring باید خارج از مرز (outline/box-shadow) باشد
- focus نباید باعث layout shift شود
- فقط در keyboard navigation (`:focus-visible`)

### Layout Structure
```html
<button class="btn btn--primary btn--medium">
  <span class="btn__inner">
    <span class="btn__icon">...</span>
    <span class="btn__text">متن</span>
    <span class="btn__icon">...</span>
  </span>
</button>
```

## CSS API (Usage)

### Classes
```html
<!-- Base -->
<button class="btn">...</button>

<!-- Type -->
<button class="btn btn--primary">...</button>
<button class="btn btn--ai">...</button>
<button class="btn btn--secondary">...</button>
<button class="btn btn--subtle">...</button>
<button class="btn btn--outline">...</button>
<button class="btn btn--transparent">...</button>

<!-- Size -->
<button class="btn btn--small">...</button>
<button class="btn btn--medium">...</button>
<button class="btn btn--large">...</button>

<!-- State -->
<button class="btn btn--disabled" disabled>...</button>
<button class="btn btn--selected" aria-pressed="true">...</button>

<!-- Link as Button -->
<a href="#" class="btn btn--primary btn--large">...</a>
```

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier):

```css
.btn { }                        /* Block */
.btn__inner { }                 /* Element */
.btn__icon { }
.btn__text { }

.btn--primary { }               /* Modifier: Type */
.btn--secondary { }
.btn--ai { }
.btn--subtle { }
.btn--outline { }
.btn--transparent { }

.btn--large { }                 /* Modifier: Size */
.btn--medium { }
.btn--small { }

.btn--selected { }              /* Modifier: State */
.btn--disabled { }
```

## Accessibility Requirements

### ARIA Attributes
```html
<button
  class="btn btn--primary btn--large"
  aria-label="متن دکمه"
  aria-pressed="false"
>
  ...
</button>
```

### Keyboard Navigation
- **Enter/Space**: Activate button (native browser behavior)
- **Tab**: Navigate to next focusable element
- **Shift+Tab**: Navigate to previous element

### Focus Visible
- نمایش focus ring فقط در keyboard navigation
- استفاده از `:focus-visible` pseudo-class

### Color Contrast
- تمام ترکیب‌های رنگ باید WCAG 2.1 Level AA را رعایت کنند
- حداقل contrast ratio 4.5:1 برای متن

## File Structure

```
/components/button/
├── button.css         # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens
```

## Risks / Trade-offs

### Risk 1: No Dynamic State Management
**Risk**: بدون JavaScript، تغییر state (selected, disabled) باید توسط developer مدیریت شود

**Mitigation**:
- مستندسازی واضح نحوه اضافه/حذف CSS classes
- سازگار با هر framework که DOM manipulation دارد

### Risk 2: Browser Compatibility
**Risk**: CSS custom properties و `:focus-visible` در مرورگرهای قدیمی کار نمی‌کنند

**Mitigation**:
- مستندسازی minimum browser requirements
- در صورت نیاز، استفاده از CSS fallback values

### Risk 3: Icon Integration
**Risk**: آیکن‌ها باید به صورت inline در HTML قرار بگیرند

**Mitigation**:
- ارائه مثال‌های واضح در مستندات
- سازگاری با Icon Component در آینده

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
1. افزودن loading state (در صورت نیاز)
2. افزودن dark theme support
3. افزودن tooltip support
