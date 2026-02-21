# Design Document: Tag Component

## Context
این کامپوننت Tag بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Tag برای نمایش اطلاعات کوتاه، وضعیت‌ها، دسته‌بندی‌ها یا مقادیر انتخاب‌شده استفاده می‌شود.

### Stakeholders
- توسعه‌دهندگان frontend
- طراحان UI/UX (consistency با Figma)
- تیم accessibility (WCAG compliance)

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript برای استایل‌دهی)
- باید از design tokens استفاده کند
- باید از RTL/LTR پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)

## Goals / Non-Goals

### Goals
- کامپوننت Tag با 4 حالت تعاملی (Rest, Hover, Focus, Disabled)
- 2 استایل بصری (Filled, Outline)
- 4 واریانت رنگی (Gray, Green, Orange, Red)
- 3 سایز (Small, Medium, Large)
- 2 شکل گوشه (Rounded, Circular)
- پشتیبانی از dismiss icon (دکمه حذف)
- پشتیبانی از trailing icon
- Focus ring بدون تغییر layout (overlay state)
- پشتیبانی کامل RTL/LTR
- Accessibility (focus ring, keyboard navigation)
- استفاده از CSS custom properties برای theming

### Non-Goals
- منطق حذف یا انتخاب (Tag فقط نمایشی است)
- Dark theme
- Pressed state (طبق Figma فقط Rest, Hover, Focus, Disabled)
- Drag & Drop
- پشتیبانی از IE11

## Decisions

### 1. Architecture Pattern: CSS Classes (BEM) + Semantic HTML
**Decision**: استفاده از `<span>` با CSS classes برای کنترل style, color, size, radius

**Rationale**:
- Tag عنصر نمایشی است (نه form control)
- State management با CSS classes و pseudo-classes
- BEM naming مطابق الگوی سایر کامپوننت‌ها
- سازگار با هر framework

### 2. HTML Structure
**Decision**: `<span>` container با المان‌های داخلی

```html
<span class="tag tag--filled tag--gray tag--medium tag--rounded">
  <svg class="tag__icon">...</svg>           <!-- optional: trailing icon -->
  <span class="tag__text">متن تگ</span>
  <button class="tag__dismiss">...</button>  <!-- optional: dismiss icon -->
</span>
```

**Rationale**:
- `tag`: container اصلی — inline-flex, centered alignment
- `tag__icon`: آیکن اختیاری کنار متن (سمت start)
- `tag__text`: متن تگ
- `tag__dismiss`: دکمه حذف — `<button>` برای accessibility (کلیک + keyboard)
- ترتیب المان‌ها در HTML: icon → text → dismiss (طبق Figma layout)

### 3. State Management: CSS Classes + Pseudo-Classes
**Decision**: ترکیب CSS classes (modifier) و pseudo-classes

```css
.tag--filled.tag--gray { /* filled gray rest */ }
.tag--filled.tag--gray:hover:not(.tag--disabled) { /* hover */ }
.tag--filled.tag--gray.tag--focused:not(.tag--disabled) { /* focus */ }
.tag--disabled { /* disabled styles */ }
```

**State Priority** (CSS specificity):
1. disabled > focus > hover > rest

### 4. Focus Implementation
**Decision**: focus ring با border 1px solid #222323 — overlay state

**Rationale**:
- فوکوس یک لایه بصری اضافه است
- می‌تواند همزمان با rest و hover وجود داشته باشد
- برای Filled: border 2px white در rest → border 1px solid #222323 در focus
- برای Outline: border 1px colored در rest → border 1px solid #222323 در focus
- disabled همیشه فوکوس را حذف می‌کند
- با `tabindex="0"` فوکوس‌پذیر می‌شود (اختیاری)

### 5. Color Strategy
**Decision**: 4 رنگ × 2 استایل × 4 حالت = ماتریس رنگی کامل

**Filled Style:**
| Color | Rest bg | Hover bg | Rest border | Text |
|-------|---------|----------|-------------|------|
| Gray | #f6f8fa | #f1f3f5 | #ffffff (2px) | #222323 |
| Green | #f1faf1 | #e7f2e7 | #ffffff (2px) | #107c10 |
| Orange | #fff9f5 | #feefe7 | #ffffff (2px) | #f7630c |
| Red | #fdf3f4 | #f9e7e9 | #ffffff (2px) | #c50f1f |

**Outline Style (Rest):**
| Color | Border | Text |
|-------|--------|------|
| Gray | #e2e4e6 | #222323 |
| Green | #9fd89f | #107c10 |
| Orange | #fdcfb4 | #f7630c |
| Red | #eeacb2 | #c50f1f |

**Outline Style (Hover):**
| Color | Border | Text |
|-------|--------|------|
| Gray | #e2e4e6 | #222323 |
| Green | #107c10 | #0c5e0c |
| Orange | #f7630c | #bc4b09 |
| Red | #c50f1f | #960b18 |

**Focus (همه):**
| عنصر | مقدار |
|------|-------|
| Border | 1px solid #222323 |

**Disabled (همه رنگ‌ها یکسان):**
| Style | Background | Border | Text |
|-------|-----------|--------|------|
| Filled | #e7e9eb | — (بدون border) | #bbbcbe |
| Outline | — | 1px solid #e7e9eb | #bbbcbe |

### 6. Size Strategy
**Decision**: 3 سایز با تفاوت در ارتفاع، padding، فونت و اندازه آیکن

| Size | Height | Padding X | Font Size | Line Height | Icon Wrapper |
|------|--------|-----------|-----------|-------------|--------------|
| Small | 24px | 8px | 13px | 1.3 | 18px |
| Medium | 32px | 8px | 14px | 1.5 | 18px |
| Large | 37px | 12px | 16px | 1.5 | 22px |

### 7. Dismiss Icon Strategy
**Decision**: `<button>` با SVG آیکن × (close/remove)

**Rationale**:
- dismiss icon = دکمه تعاملی → باید `<button>` باشد
- رنگ آیکن dismiss = رنگ متن Tag (هماهنگ با color, style, state)
- در disabled: نمایش داده می‌شود ولی قابل تعامل نیست
- اندازه: 24px container (ثابت در همه سایزها)

## CSS Class Naming Convention

BEM — مطابق الگوی سایر کامپوننت‌ها:

```css
.tag { }                 /* Block: container */
.tag__text { }           /* Element: label text */
.tag__icon { }           /* Element: trailing icon */
.tag__dismiss { }        /* Element: dismiss button */

/* Modifiers — Style */
.tag--filled { }
.tag--outline { }

/* Modifiers — Color */
.tag--gray { }
.tag--green { }
.tag--orange { }
.tag--red { }

/* Modifiers — Size */
.tag--small { }
.tag--medium { }
.tag--large { }

/* Modifiers — Radius */
.tag--rounded { }
.tag--circular { }

/* Modifiers — State */
.tag--focused { }
.tag--disabled { }
```

## Risks / Trade-offs

### Risk 1: تعداد ترکیبات بالا
**Risk**: 4 رنگ × 2 استایل × 4 حالت × 3 سایز × 2 شکل = 192 ترکیب
**Mitigation**: استفاده از CSS custom properties و ساختار modular — سایز و radius مستقل از رنگ/style/state

### Risk 2: Border Width تفاوت بین Filled و Outline
**Risk**: Filled دارای border 2px و Outline دارای border 1px — تفاوت در focus
**Mitigation**: مدیریت دقیق border-width و padding تا layout shift نداشته باشیم

### Risk 3: Dismiss Icon Accessibility
**Risk**: dismiss icon باید با keyboard قابل دسترسی باشد
**Mitigation**: استفاده از `<button>` element با aria-label

## File Structure

```
/components/tag/
├── tag.css            # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```
