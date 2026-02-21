# Design Document: Tooltip Component

## Context
این کامپوننت Tooltip بخشی از سیستم طراحی FrontLayer EsanjUiKit است. تولتیپ یک پیام کوچک و مرتفع است که هنگام hover یا focus روی یک عنصر، اطلاعات غیر ضروری و متنی را ارائه می‌کند. تولتیپ برای ارائه اطلاعات ساده و مفید استفاده می‌شود و نباید برای بازخورد سیستم یا اطلاعات تعاملی به کار رود.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به نمایش راهنمای hover دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- استایل‌ها با CSS پیاده‌سازی می‌شود
- رفتار نمایش/مخفی با JavaScript پیاده‌سازی می‌شود
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- کامپوننت Tooltip با 4 جهت: Top، Bottom، Right و Left
- نمایش هنگام hover و focus
- Arrow/فلش به سمت trigger
- Accessible با `role="tooltip"` و `aria-describedby`
- پشتیبانی RTL
- تأخیر قابل تنظیم برای نمایش
- استفاده از CSS custom properties برای theming
- API ساده: data attributes + JavaScript API

### Non-Goals
- Auto-positioning (تشخیص خودکار بهترین جهت بر اساس viewport)
- محتوای تعاملی (لینک، دکمه) — از Popover استفاده کنید
- محتوای چند خطی یا rich text
- پشتیبانی از Dark theme (فعلاً فقط یک تم تیره)
- انیمیشن پیچیده ورود/خروج
- Auto-positioning (تشخیص خودکار بهترین جهت)

## Decisions

### 1. Architecture Pattern: CSS + JavaScript
**Decision**: استایل‌ها با CSS و رفتار (show/hide، delay) با JavaScript

**Rationale**:
- نمایش/مخفی کردن نیاز به hover و focus event handling دارد
- تأخیر نمایش نیاز به setTimeout دارد
- ARIA attributes باید به صورت دینامیک تنظیم شوند
- استایل‌های بصری کاملاً CSS-based هستند

**Alternatives Considered**:
- Pure CSS (با `:hover` و `::after`): محدودیت در accessibility و delay control
- CSS `popover` API: پشتیبانی محدود در مرورگرها

### 2. Usage Pattern: Data Attributes
**Decision**: استفاده از `data-tooltip` برای متن و `data-tooltip-position` برای جهت

```html
<div class="tooltip" data-tooltip="متن tooltip" data-tooltip-position="right">
  <button>trigger</button>
</div>
```

**Rationale**:
- ساده‌ترین API برای استفاده
- بدون نیاز به markup اضافی
- JavaScript tooltip bubble را به صورت خودکار می‌سازد
- مطابق الگوی رایج tooltip libraries

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables برای theming

```css
:root {
  --tooltip-color-bg: #364455;
  --tooltip-color-text: #ffffff;
  --tooltip-font-size: 14px;
  --tooltip-radius: 4px;
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Toast، Select و سایر components
- امکان override توسط developer

### 4. Position Management: CSS Modifier Classes
**Decision**: دو جهت با modifier class

- Top: `.tooltip--top` — tooltip بالای trigger
- Bottom: `.tooltip--bottom` — tooltip پایین trigger
- Right: `.tooltip--right` — tooltip سمت راست trigger
- Left: `.tooltip--left` — tooltip سمت چپ trigger

**Rationale**:
- مطابق طراحی Figma — چهار واریانت "Tooltip Top"، "Tooltip Down"، "Tooltip Right" و "Tooltip Left"
- ساده و قابل فهم
- Arrow position بر اساس جهت تنظیم می‌شود

### 5. Accessibility: role="tooltip"
**Decision**: استفاده از WAI-ARIA tooltip pattern

**Rationale**:
- `role="tooltip"` روی bubble
- `aria-describedby` روی trigger برای اتصال به tooltip
- نمایش هنگام focus برای keyboard users
- screen reader محتوای tooltip را اعلام می‌کند

### 6. Show/Hide Behavior
**Decision**: نمایش هنگام hover/focus با تأخیر اختیاری

**Rationale**:
- `mouseenter` → نمایش (با تأخیر اختیاری)
- `mouseleave` → مخفی
- `focusin` → نمایش
- `focusout` → مخفی
- تأخیر پیش‌فرض 0ms با قابلیت تنظیم با `data-tooltip-delay`

## CSS Class Naming Convention

```css
.tooltip { }                   /* Block: wrapper */
.tooltip__bubble { }           /* Element: tooltip bubble */
.tooltip__arrow { }            /* Element: arrow/triangle (child of bubble) */

.tooltip--top { }              /* Modifier: top position */
.tooltip--bottom { }           /* Modifier: bottom position */
.tooltip--right { }            /* Modifier: right position */
.tooltip--left { }             /* Modifier: left position */
.tooltip--visible { }          /* Modifier: visible state */
```

## Risks / Trade-offs

### Risk 1: Tooltip Clipping
**Risk**: tooltip ممکن است از لبه viewport خارج شود

**Mitigation**:
- `max-width` برای جلوگیری از عریض شدن بیش از حد
- مستندسازی محدودیت (auto-positioning خارج از scope)

### Risk 2: Touch Devices
**Risk**: hover در دستگاه‌های لمسی کار نمی‌کند

**Mitigation**:
- Focus-based نمایش به عنوان fallback
- مستندسازی محدودیت touch

### Risk 3: Nested Interactive Elements
**Risk**: tooltip نباید محتوای تعاملی داشته باشد

**Mitigation**:
- مستندسازی: برای محتوای تعاملی از Popover استفاده کنید
- tooltip فقط متن ساده می‌پذیرد

## Migration Plan

### Phase 1: Initial Implementation
1. ساخت CSS component
2. ساخت JavaScript API
3. تست در demo page
4. مستندسازی
