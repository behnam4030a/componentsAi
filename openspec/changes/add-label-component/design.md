# Design Document: Label Component

## Context
این کامپوننت Label بخشی از سیستم طراحی FrontLayer EsanjUiKit است که به صورت Pure CSS پیاده‌سازی می‌شود. Label برای نمایش برچسب متنی در کنار یا بالای فیلدها (مثل Input، Select، Checkbox) استفاده می‌شود. این کامپوننت نقش اطلاع‌رسانی دارد و رفتار تعاملی مستقل ندارد.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به کامپوننت Label دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- باید عمدتاً با CSS پیاده‌سازی شود (بدون JavaScript)
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- کامپوننت Label با 2 حالت: Normal و Disabled
- پشتیبانی از 3 سایز (Large, Medium, Small)
- پشتیبانی از 2 نوع فونت (Regular, Semibold)
- Required indicator (علامت *)
- پشتیبانی کامل RTL
- Accessibility features (semantic label, color contrast)
- استفاده از CSS custom properties برای theming
- API ساده: CSS classes + native HTML label

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- State‌های تعاملی (hover, focus) — Label کامپوننت نمایشی است
- Helper text / Error message (خارج از scope)
- Floating label / Animated label
- Form validation logic
- پشتیبانی از مرورگرهای قدیمی (IE11)

## Decisions

### 1. Architecture Pattern: CSS + Native HTML Label
**Decision**: استفاده از `<label>` بومی HTML با CSS custom styling

**Rationale**:
- Accessibility built-in (screen readers، association با فیلد)
- سازگار با هر framework (React, Vue, Angular, vanilla HTML)
- مطابق الگوی Button، Checkbox و Input component
- عدم نیاز به JavaScript

**Alternatives Considered**:
- `<span>` با role: از دست دادن semantic meaning
- `<div>`: عدم ارتباط بومی با فیلد ورودی

### 2. HTML Structure
**Decision**: استفاده از `<label>` به عنوان wrapper با المان‌های داخلی برای متن و indicator

```html
<label class="label label--medium label--required">
  <span class="label__text">برچسب</span>
  <span class="label__required">*</span>
</label>
```

**Rationale**:
- ساختار ساده و flat (بدون nesting اضافی)
- `label__text` المان اصلی متن، اول قرار می‌گیرد
- `label__required` المان ستاره، بعد از متن (سمت end) قرار می‌گیرد
- Flexbox با gap: 4px برای فاصله‌گذاری
- align-items: start برای تراز بالایی (مطابق طراحی Figma)

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables (custom properties) برای theming — مطابق الگوی موجود

```css
:root {
  --label-color-text: #222323;
  --label-color-disabled: #bbbcbe;
  --label-color-required: #c50f1f;
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Button، Checkbox و Input components
- امکان override کردن توسط developer
- Runtime theming support

### 4. Type Management: Modifier Class
**Decision**: استفاده از `.label--semibold` modifier class برای تغییر font-weight

**Rationale**:
- type فقط font-weight را تغییر می‌دهد (400 → 500)
- نباید رنگ، اندازه یا فاصله‌ها را تغییر دهد
- Regular حالت پیش‌فرض است (بدون class اضافی)
- Semibold با modifier class فعال می‌شود

### 5. Size Management: Modifier Classes
**Decision**: استفاده از `.label--large`, `.label--medium`, `.label--small` modifier classes

**Typography mapping (Regular)**:
- Large: 16px / 400 / 1.5 → Body Large
- Medium: 14px / 400 / 1.5 → Body Medium
- Small: 12px / 400 / 1.5 → Body Small

**Typography mapping (Semibold)**:
- Large: 16px / 500 / 1.5 → Body Large EMP
- Medium: 12px / 500 / 1.5 → Body Small EMP
- Small: 12px / 500 / 1.5 → Body Small EMP

**نکته مهم**: در سایز Small، ستاره required از استایل Caption (13px/1.3) استفاده می‌کند نه Body Small، برای تراز بصری بهتر.

### 6. Disabled State: Modifier Class
**Decision**: استفاده از `.label--disabled` modifier class

**Rationale**:
- Label خودش تعامل‌پذیر نیست و attribute `disabled` بومی ندارد
- modifier class توسط developer یا framework بر اساس وضعیت فیلد مرتبط set می‌شود
- هم متن و هم required indicator به رنگ disabled (#bbbcbe) تغییر می‌کنند

### 7. Required Indicator: Separate Element
**Decision**: ستاره (*) در یک المان جداگانه `<span class="label__required">` بعد از متن

**Rationale**:
- امکان استایل‌دهی مستقل (رنگ قرمز متفاوت از متن)
- در RTL: ستاره سمت چپ متن (end side)
- در LTR: ستاره سمت راست متن (end side)
- تراز با align-items: start برای هماهنگی با baseline

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier) — مطابق الگوی سایر کامپوننت‌ها:

```css
.label { }                      /* Block */
.label__text { }                 /* Element: label text (first) */
.label__required { }             /* Element: required indicator (*) (after text) */

.label--large { }                /* Modifier: Size */
.label--medium { }
.label--small { }

.label--semibold { }             /* Modifier: Font weight type */
.label--required { }             /* Modifier: Has required indicator */
.label--disabled { }             /* Modifier: Disabled state */
```

## Risks / Trade-offs

### Risk 1: Typography Inconsistency in Semibold Medium
**Risk**: در Figma، Semibold Medium از Body Small EMP (12px) استفاده می‌کند نه Body Medium EMP (14px)، چون Body Medium EMP در سیستم تایپوگرافی تعریف نشده.

**Mitigation**: دقیقاً مطابق Figma پیاده‌سازی شود. اگر در آینده Body Medium EMP اضافه شد، فقط یک CSS variable تغییر می‌کند.

### Risk 2: Asterisk Size Difference in Small
**Risk**: در سایز Small، ستاره از سایز Caption (13px/1.3) استفاده می‌کند که با متن (12px/1.5) متفاوت است.

**Mitigation**: استایل‌های مستقل برای ستاره در سایز Small تعریف شود.

## File Structure

```
/components/label/
├── label.css          # Component styles (pure CSS)
├── index.html         # Demo page
└── tokens.json        # Design tokens (already created)
```
