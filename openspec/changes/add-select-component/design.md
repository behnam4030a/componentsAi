# Design Document: Select Component

## Context
این کامپوننت Select بخشی از سیستم طراحی FrontLayer EsanjUiKit است. Select برای انتخاب مقدار از میان گزینه‌های موجود استفاده می‌شود. سلکت‌ها یک انتخاب را مشخص می‌کنند و معمولاً وضعیت یا رفتار بعدی سیستم را تعیین می‌کنند. این کامپوننت شامل 4 نوع (Basic، Primary، Multiple، Tagify) و 3 اندازه (Small، Medium، Large) است.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به dropdown و selection دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- استایل‌ها با CSS پیاده‌سازی می‌شود
- رفتار dropdown، search و انتخاب با JavaScript پیاده‌سازی می‌شود
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد

## Goals / Non-Goals

### Goals
- کامپوننت Select با 4 نوع: Basic، Primary (Single)، Multiple، Tagify
- پشتیبانی از 3 اندازه: Small، Medium، Large
- وضعیت‌ها: Rest، Active/Focused، Selected، Disabled
- Dropdown با لیست آیتم‌ها و highlight انتخاب
- فیلد جستجو در نوع Basic
- سیستم تگ برای Primary (بنفش) و Multiple/Tagify (خاکستری)
- Keyboard navigation کامل
- پشتیبانی RTL
- Accessibility features (role, aria attributes, keyboard)
- استفاده از CSS custom properties برای theming

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- Async/remote data loading (lazy loading آیتم‌ها)
- Virtualized list برای هزاران آیتم
- Drag & drop برای ترتیب تگ‌ها
- پشتیبانی از مرورگرهای قدیمی (IE11)
- Grouped options (گروه‌بندی آیتم‌ها)
- Custom option rendering (آیتم‌ها فقط متنی هستند)

## Decisions

### 1. Architecture Pattern: CSS + JavaScript
**Decision**: استایل‌ها با CSS و رفتار (dropdown toggle، search، selection، tag management) با JavaScript

**Rationale**:
- Dropdown باز/بسته شدن نیاز به event handling دارد
- Search و فیلتر آیتم‌ها نیاز به JavaScript دارد
- مدیریت تگ‌ها (اضافه/حذف) نیاز به DOM manipulation دارد
- Keyboard navigation نیاز به JavaScript event listeners دارد
- استایل‌های بصری کاملاً CSS-based هستند

**Alternatives Considered**:
- Pure CSS dropdown (با `:focus-within`): محدودیت در search و keyboard navigation
- Web Components: over-engineering برای این use case

### 2. HTML Structure
**Decision**: استفاده از ساختار semantic با trigger + dropdown pattern

```html
<div class="select select--basic" data-type="basic">
  <button class="select__trigger" aria-haspopup="listbox" aria-expanded="false">
    <span class="select__value">انتخاب کنید</span>
    <svg class="select__chevron"><!-- chevron --></svg>
  </button>
  <div class="select__dropdown">
    <div class="select__search">
      <input type="text" class="select__search-input" placeholder="جستجو..." />
    </div>
    <ul class="select__list" role="listbox">
      <li class="select__item" role="option">آیتم</li>
    </ul>
  </div>
</div>
```

**Rationale**:
- `select__trigger`: دکمه/ناحیه کلیک‌پذیر برای باز کردن dropdown
- `select__value`: نمایش مقدار انتخاب شده (در Basic) یا placeholder
- `select__tags`: کانتینر تگ‌ها (در Primary/Multiple/Tagify)
- `select__chevron`: آیکن فلش — چرخش 180 درجه در حالت open
- `select__dropdown`: کانتینر dropdown — position absolute
- `select__search`: فیلد جستجو (فقط در Basic)
- `select__list`: لیست آیتم‌ها — role="listbox"
- `select__item`: هر آیتم — role="option"

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables برای theming — مطابق الگوی سایر components

```css
:root {
  --select-color-bg: #ffffff;
  --select-color-text: #59595a;
  --select-color-title: #222323;
  --select-color-disabled-text: #bbbcbe;
  --select-color-placeholder: #59595a;
  --select-color-stroke-rest: #e2e4e6;
  --select-color-stroke-hover: #d8dadc;
  --select-color-stroke-search: #cacbcd;
  --select-color-stroke-disabled: #dddfe1;
  --select-color-accent: #8a38f5;
  --select-color-accent-bg: rgba(138, 56, 245, 0.05);
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Toast، Input، Button و سایر components
- امکان override کردن توسط developer
- Runtime theming support

### 4. Type Management: CSS Modifier Classes
**Decision**: هر نوع با modifier class مشخص می‌شود

**Type Mapping**:
- Basic: `.select--basic`
- Primary (Single): `.select--primary`
- Multiple: `.select--multiple`
- Tagify: `.select--tagify`

**State Classes**:
- Active/Focused: `.select--active`
- Open: `.select--open`
- Disabled: `.select--disabled`

**Rationale**:
- ساده و قابل فهم
- مطابق الگوی BEM
- state توسط JavaScript مدیریت می‌شود

### 5. Tag System
**Decision**: دو نوع تگ با استایل متفاوت

- **Single Tag** (Primary): پس‌زمینه `rgba(138,56,245,0.05)`، متن `#8a38f5`
- **Multiple Tags** (Multiple/Tagify): پس‌زمینه `rgba(89,89,90,0.05)`، متن `#59595a`

**Rationale**:
- مطابق طراحی Figma
- تمایز بصری بین انتخاب تکی و چندگانه
- آیکن حذف روی هر تگ برای UX بهتر

### 6. Search Functionality
**Decision**: فیلد جستجو فقط در نوع Basic وجود دارد

**Rationale**:
- مطابق طراحی Figma — فقط Basic دارای search input است
- Primary و Multiple معمولاً آیتم‌های کمتری دارند
- سادگی پیاده‌سازی و UX

### 7. Dropdown Positioning
**Decision**: استفاده از `position: absolute` نسبت به container

**Rationale**:
- Dropdown خارج از flow اصلی قرار می‌گیرد
- Layout صفحه تغییر نمی‌کند
- Shadow و border-radius مستقل اعمال می‌شود
- z-index مناسب برای نمایش روی سایر المان‌ها

### 8. Accessibility: ARIA Pattern
**Decision**: استفاده از Listbox pattern (WAI-ARIA)

**Rationale**:
- `role="listbox"` برای لیست آیتم‌ها
- `role="option"` برای هر آیتم
- `aria-selected` برای آیتم انتخاب شده
- `aria-haspopup="listbox"` روی trigger
- `aria-expanded` برای وضعیت dropdown
- `aria-activedescendant` برای keyboard navigation
- Screen reader به صورت خودکار آیتم‌ها را اعلام می‌کند

### 9. Size Variants
**Decision**: سه اندازه با CSS modifier classes

- Small: `.select--sm`
- Medium: `.select--md` (پیش‌فرض)
- Large: `.select--lg`

**Rationale**:
- مطابق طراحی Figma — سه اندازه: کوچک، متوسط، بزرگ
- تغییر اندازه trigger height، font-size و padding
- مطابق الگوی سایر components

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier):

```css
.select { }                        /* Block */
.select__trigger { }               /* Element: trigger/button */
.select__value { }                 /* Element: displayed value text */
.select__placeholder { }           /* Element: placeholder text */
.select__tags { }                  /* Element: tags container */
.select__tag { }                   /* Element: individual tag */
.select__tag-close { }             /* Element: tag close button */
.select__chevron { }               /* Element: chevron icon */
.select__dropdown { }              /* Element: dropdown panel */
.select__search { }                /* Element: search container */
.select__search-input { }          /* Element: search input */
.select__list { }                  /* Element: items list */
.select__item { }                  /* Element: single item */
.select__scrollbar { }             /* Element: custom scrollbar */

.select--basic { }                 /* Modifier: Basic type */
.select--primary { }               /* Modifier: Primary/Single type */
.select--multiple { }              /* Modifier: Multiple type */
.select--tagify { }                /* Modifier: Tagify type */
.select--sm { }                    /* Modifier: Small size */
.select--md { }                    /* Modifier: Medium size (default) */
.select--lg { }                    /* Modifier: Large size */
.select--active { }                /* Modifier: Active/Focused state */
.select--open { }                  /* Modifier: Dropdown open */
.select--disabled { }              /* Modifier: Disabled state */
.select__item--selected { }        /* Modifier: Selected item */
.select__item--highlighted { }     /* Modifier: Keyboard highlighted item */
.select__tag--single { }           /* Modifier: Single (purple) tag */
.select__tag--multiple { }         /* Modifier: Multiple (gray) tag */
```

## Risks / Trade-offs

### Risk 1: Dropdown Overflow
**Risk**: Dropdown ممکن است از viewport خارج شود

**Mitigation**:
- استفاده از `max-height` با scroll برای dropdown
- Positioning logic در JavaScript (اگر لازم باشد flip بشود)
- مستندسازی نحوه استفاده از container با overflow visible

### Risk 2: Search Performance
**Risk**: جستجو در لیست بلند ممکن است کند باشد

**Mitigation**:
- فیلتر ساده با `textContent.includes()` — کافی برای لیست‌های معمولی
- Async data loading خارج از scope — مستندسازی شده

### Risk 3: Keyboard Navigation Complexity
**Risk**: مدیریت keyboard navigation بین trigger، search و items پیچیده است

**Mitigation**:
- پیاده‌سازی مرحله‌ای: ابتدا mouse، سپس keyboard
- استفاده از aria-activedescendant pattern
- Focus management دقیق

### Risk 4: Tag Overflow in Trigger
**Risk**: تعداد زیاد تگ ممکن است trigger را بشکند

**Mitigation**:
- `overflow: hidden` روی trigger
- Max height برای ناحیه تگ‌ها
- Scroll یا wrap برای تگ‌های اضافی

### Risk 5: Accessibility with Custom Select
**Risk**: Custom select ذاتاً accessibility issues بیشتری نسبت به native `<select>` دارد

**Mitigation**:
- پیروی دقیق از WAI-ARIA Listbox pattern
- Keyboard navigation کامل (Arrow keys، Enter، Escape، Tab)
- Screen reader testing

## Migration Plan

### Phase 1: Initial Implementation
1. ساخت CSS component (custom properties، trigger، dropdown، items، tags)
2. ساخت JavaScript API (dropdown toggle، selection، tag management)
3. تست در demo page
4. مستندسازی

### Phase 2: Enhanced Features
1. اضافه کردن search functionality
2. Keyboard navigation
3. Size variants
4. Tagify variant

### Phase 3: Integration
1. استفاده در یک feature واقعی
2. جمع‌آوری feedback
3. رفع bugs و بهبودها
