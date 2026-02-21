# Design Document: Radio Component

## Context
این کامپوننت Radio بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Radio برای انتخاب یک گزینه از بین چند گزینه‌ی انحصاری استفاده می‌شود. ساختار و الگوی پیاده‌سازی مشابه کامپوننت Checkbox است.

### Stakeholders
- توسعه‌دهندگان frontend
- طراحان UI/UX (consistency با Figma)
- تیم accessibility (WCAG compliance)

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript برای استایل‌دهی)
- باید از design tokens استفاده کند
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)

## Goals / Non-Goals

### Goals
- کامپوننت Radio با 5 حالت تعاملی (Rest, Hover, Pressed, Focus, Disabled)
- پشتیبانی از checked/unchecked
- Label اختیاری با قابلیت کلیک
- Focus ring بدون تغییر layout
- پشتیبانی کامل RTL
- Accessibility (focus ring, keyboard navigation, semantic input)
- استفاده از CSS custom properties برای theming

### Non-Goals
- Radio Group logic (خارج از scope — مدیریت با `name` attribute بومی)
- Dark theme
- سایزهای مختلف (طبق Figma فقط یک سایز)
- انیمیشن‌های پیچیده
- پشتیبانی از IE11

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Radio Input
**Decision**: استفاده از `<input type="radio">` بومی HTML درون `<label>` wrapper — مشابه الگوی Checkbox

**Rationale**:
- رفتار بومی مرورگر: `:checked`, `:disabled`, `name` grouping
- Accessibility built-in (screen readers, keyboard navigation)
- سازگار با هر framework
- `<label>` wrapper: کلیک روی هر جای المان = کلیک Radio

### 2. HTML Structure
**Decision**: الگوی مشابه Checkbox — native input مخفی + المان‌های بصری

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

**Rationale**:
- `radio__input`: input بومی مخفی (visually-hidden) برای state management
- `radio__box`: container دایره — padding و centering
- `radio__label`: متن برچسب (اختیاری) — بعد از کنترل دایره‌ای
- `radio__circle`: دایره بیرونی — border و border-radius: 50%
- `radio__dot`: نقطه داخلی — فقط در `:checked` نمایش داده می‌شود

### 3. State Management: CSS Sibling Selectors
**Decision**: استفاده از `~` (general sibling combinator) برای propagate کردن state از input به المان‌های بصری — مشابه Checkbox

```css
.radio__input:checked ~ .radio__box .radio__circle { /* checked styles */ }
.radio__input:disabled ~ .radio__box .radio__circle { /* disabled styles */ }
.radio:hover .radio__input:not(:disabled) ~ .radio__box .radio__circle { /* hover */ }
.radio__input:active:not(:disabled) ~ .radio__box .radio__circle { /* pressed */ }
.radio__input:focus-visible ~ .radio__box { /* focus ring on wrapper */ }
```

**State Priority** (CSS specificity):
1. disabled > pressed > focus > hover > rest

### 4. Focus Ring Implementation
**Decision**: border 1px solid #222323 روی wrapper، با border-radius 4px

**Rationale**:
- استفاده از `:focus-visible` (نه `:focus`) — فقط keyboard focus
- border transparent در حالت عادی → solid در focus → بدون layout shift
- مطابق طراحی Figma: focus ring روی کل کامپوننت (نه فقط دایره)

### 5. Checked State: Inner Dot
**Decision**: نقطه داخلی (`radio__dot`) با transform: scale(0) در حالت unchecked و scale(1) در checked

**Rationale**:
- transition نرم برای ظاهر/مخفی شدن
- رنگ dot مطابق state (brand colors / disabled color)
- اندازه ثابت 9px، centered در دایره 17px

### 6. Color Strategy
**Decision**: دو مجموعه رنگ بر اساس checked status

**Unchecked**: Neutral stroke colors
| State | Border |
|-------|--------|
| Rest | #626364 |
| Hover | #59595a |
| Pressed | #4f4f50 |
| Disabled | #bbbcbe |

**Checked**: Brand foreground colors
| State | Border + Dot |
|-------|-------------|
| Rest | #26a88c |
| Hover | #1d836d |
| Pressed | #155e4e |
| Disabled | #bbbcbe |

## CSS Class Naming Convention

BEM — مطابق الگوی Checkbox:

```css
.radio { }                       /* Block: wrapper label */
.radio__input { }                /* Element: hidden native input */
.radio__label { }                /* Element: text label */
.radio__box { }                  /* Element: circle container */
.radio__circle { }               /* Element: outer circle (border) */
.radio__dot { }                  /* Element: inner dot (checked) */
```

## Risks / Trade-offs

### Risk 1: `:focus-visible` Browser Support
**Risk**: مرورگرهای قدیمی‌تر `:focus-visible` را پشتیبانی نمی‌کنند
**Mitigation**: fallback به `:focus` با `@supports not selector(:focus-visible)`

### Risk 2: Radio Group Logic
**Risk**: منطق "فقط یک انتخاب" باید توسط HTML `name` attribute مدیریت شود
**Mitigation**: مستندسازی واضح نحوه استفاده از `name` attribute برای grouping

## File Structure

```
/components/radio/
├── radio.css          # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```
