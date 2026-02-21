# Design Document: Switch Component

## Context
این کامپوننت Switch بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Switch برای تغییر فوری بین دو حالت روشن/خاموش استفاده می‌شود. ساختار و الگوی پیاده‌سازی مشابه کامپوننت Checkbox است (native input مخفی + المان‌های بصری).

### Stakeholders
- توسعه‌دهندگان frontend
- طراحان UI/UX (consistency با Figma)
- تیم accessibility (WCAG compliance)

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript برای استایل‌دهی)
- باید از design tokens استفاده کند
- باید از RTL/LTR پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- Switch بدون Label داخلی (Label جداگانه)

## Goals / Non-Goals

### Goals
- کامپوننت Switch با 5 حالت تعاملی (Rest, Hover, Pressed, Focus, Disabled)
- پشتیبانی از checked/unchecked با حرکت Thumb
- آیکن checkmark (checked) و X (unchecked) داخل Thumb
- Focus ring بدون تغییر layout (non-exclusive با سایر stateها)
- Thumb transition برای حرکت نرم
- پشتیبانی کامل RTL/LTR
- Accessibility (role="switch", focus ring, keyboard navigation)
- استفاده از CSS custom properties برای theming

### Non-Goals
- Label داخلی (خارج از scope — از کامپوننت Label جداگانه استفاده شود)
- Dark theme
- سایزهای مختلف (طبق Figma فقط یک سایز)
- Drag interaction (فقط click/tap)
- پشتیبانی از IE11

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Checkbox Input with role="switch"
**Decision**: استفاده از `<input type="checkbox" role="switch">` بومی HTML درون `<label>` wrapper

**Rationale**:
- رفتار toggle بومی مرورگر: `:checked`, `:disabled`
- `role="switch"` برای screen readers — تفاوت معنایی با checkbox
- Accessibility built-in (keyboard navigation, Space/Enter to toggle)
- `<label>` wrapper: کلیک روی هر جای المان = toggle
- سازگار با هر framework

### 2. HTML Structure
**Decision**: native input مخفی + المان‌های بصری Track و Thumb

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

**Rationale**:
- `switch__input`: input بومی مخفی (visually-hidden) برای state management
- `switch__track`: نوار پس‌زمینه — رنگ بر اساس state × checked
- `switch__thumb`: دایره متحرک — موقعیت بر اساس checked
- `switch__icon`: آیکن checkmark/X داخل Thumb — با CSS pseudo-elements یا SVG

### 3. State Management: CSS Sibling Selectors
**Decision**: استفاده از `~` (general sibling combinator) برای propagate کردن state از input به المان‌های بصری

```css
.switch__input:checked ~ .switch__track { /* checked track styles */ }
.switch__input:checked ~ .switch__track .switch__thumb { /* thumb position: on */ }
.switch__input:disabled ~ .switch__track { /* disabled styles */ }
.switch:hover .switch__input:not(:disabled) ~ .switch__track { /* hover */ }
```

**State Priority** (CSS specificity):
1. disabled > pressed > focus > hover > rest

### 4. Focus Ring Implementation
**Decision**: border 1px solid #222323 روی wrapper، با border-radius 4px — non-exclusive

**Rationale**:
- فوکوس یک لایه بصری اضافه است (focus ring)
- می‌تواند همزمان با rest، hover و pressed فعال باشد
- border transparent در حالت عادی → solid در focus → بدون layout shift
- نباید رنگ یا موقعیت Track و Thumb را override کند
- disabled همیشه فوکوس را حذف می‌کند

### 5. Thumb Position & Transition
**Decision**: Thumb با CSS positioning و transition حرکت می‌کند

**Rationale**:
- Unchecked: Thumb سمت start (راست در RTL، چپ در LTR)
- Checked: Thumb سمت end (چپ در RTL، راست در LTR)
- transition برای حرکت نرم بین دو موقعیت
- موقعیت فقط به checked وابسته، نه state

### 6. Icon Strategy
**Decision**: آیکن‌های checkmark و X با CSS (inline SVG background یا pseudo-elements)

**Rationale**:
- Checked: آیکن checkmark با رنگ brand (#26a88c)، disabled (#bbbcbe)
- Unchecked: آیکن X با رنگ neutral (#59595a)، disabled (#bbbcbe)
- هر دو آیکن همیشه وجود دارند، visibility با CSS کنترل می‌شود

### 7. Color Strategy
**Decision**: دو مجموعه رنگ بر اساس checked status

**Checked (Track)**:
| State | Background | Border |
|-------|-----------|--------|
| Rest | #26a88c | #eaf8f5 |
| Hover | #22967d | #eaf8f5 |
| Pressed | #19705e | #eaf8f5 |
| Disabled | #f6f8fa | #dddfe1 |

**Unchecked (Track)**:
| State | Background | Border |
|-------|-----------|--------|
| Rest | #ffffff | #e2e4e6 |
| Hover | #f6f8fa | #e2e4e6 |
| Pressed | #dddfe1 | #e2e4e6 |
| Disabled | #f6f8fa | #dddfe1 |

**Thumb (Circle)**:
| Status | Background | Border |
|--------|-----------|--------|
| Checked (normal) | #ffffff | #26a88c |
| Unchecked (normal) | #ffffff | #e2e4e6 |
| Disabled (both) | #e7e9eb | #dddfe1 |

## CSS Class Naming Convention

BEM — مطابق الگوی سایر کامپوننت‌ها:

```css
.switch { }                      /* Block: wrapper label */
.switch__input { }               /* Element: hidden native input */
.switch__track { }               /* Element: background track */
.switch__thumb { }               /* Element: movable circle */
.switch__icon { }                /* Element: icon container inside thumb */
```

## Risks / Trade-offs

### Risk 1: Thumb Position in RTL
**Risk**: جابجایی Thumb در RTL/LTR باید معکوس شود
**Mitigation**: استفاده از logical properties (`inset-inline-start`/`inset-inline-end`) یا `direction`-aware positioning

### Risk 2: Icon Implementation
**Risk**: آیکن‌های checkmark و X باید به صورت CSS-only باشند
**Mitigation**: استفاده از inline SVG در background-image یا CSS pseudo-elements با mask

### Risk 3: `:focus-visible` Browser Support
**Risk**: مرورگرهای قدیمی‌تر `:focus-visible` را پشتیبانی نمی‌کنند
**Mitigation**: fallback با `@supports not selector(:has(*))`

## File Structure

```
/components/switch/
├── switch.css         # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```
