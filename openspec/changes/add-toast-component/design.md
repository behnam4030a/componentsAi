# Design Document: Toast Component

## Context
این کامپوننت Toast بخشی از سیستم طراحی FrontLayer EsanjUiKit است. Toast برای نمایش پیام‌های موقتی و غیرمسدودکننده (اعلان‌ها) به کاربر استفاده می‌شود. این پیام‌ها مفید و مرتبط هستند اما هرگز حیاتی نیستند. Toast معمولا برای تایید اقدام کاربر، اطلاع‌رسانی رویداد، یا نمایش وضعیت فرآیند استفاده می‌شود.

### Stakeholders
- توسعه‌دهندگان frontend که نیاز به سیستم اعلان دارند
- طراحان UI/UX که نیاز به consistency با Figma دارند
- تیم accessibility که نیاز به WCAG compliance دارد

### Constraints
- استایل‌ها با CSS پیاده‌سازی می‌شود
- رفتار تایمر و dismiss با JavaScript پیاده‌سازی می‌شود
- باید از design tokens استفاده کند (single source of truth)
- باید از RTL پشتیبانی کند
- باید accessible باشد (WCAG 2.1 Level AA)
- باید سبک و performant باشد
- منطق stacking و positioning خارج از scope این کامپوننت است

## Goals / Non-Goals

### Goals
- کامپوننت Toast با 4 واریانت وضعیت (Success, Danger, Warning, Neutral)
- ساختار محتوا: dismiss button, title, description (optional), status icon, timer indicator
- Timer Indicator با انیمیشن linear برای auto dismiss
- Manual Dismiss با دکمه ضربدر
- Shadow مخصوص هر واریانت
- پشتیبانی کامل RTL
- Accessibility features (role, keyboard dismiss, screen reader)
- استفاده از CSS custom properties برای theming
- API ساده: CSS classes + JavaScript API (`Toast.show()`, `Toast.init()`, `Toast.dismiss()`)

### Non-Goals
- پشتیبانی از Dark theme (فعلاً فقط Light theme)
- سیستم stacking/positioning (خارج از scope)
- انیمیشن ورود/خروج (می‌تواند توسط سیستم بالادستی اضافه شود)
- Toast queue management (خارج از scope)
- پشتیبانی از مرورگرهای قدیمی (IE11)
- Action buttons داخل Toast (مثل Undo)

## Decisions

### 1. Architecture Pattern: CSS + JavaScript
**Decision**: استایل‌ها با CSS و رفتار (تایمر، dismiss) با JavaScript

**Rationale**:
- Timer indicator نیاز به انیمیشن CSS `@keyframes` یا JavaScript timer دارد
- Dismiss button نیاز به event handler دارد
- Auto-remove بعد از اتمام تایمر نیاز به JavaScript دارد
- استایل‌های بصری کاملاً CSS-based هستند

**Alternatives Considered**:
- Pure CSS با `animation-delay`: محدودیت در کنترل pause/resume و callback
- Web Components: over-engineering برای این use case

### 2. HTML Structure
**Decision**: استفاده از ساختار flat با المان‌های semantic

```html
<div class="toast toast--success" role="status">
  <button class="toast__dismiss" aria-label="بستن">
    <svg><!-- close icon --></svg>
  </button>
  <div class="toast__inner">
    <div class="toast__content">
      <p class="toast__title">عنوان</p>
      <p class="toast__description">توضیحات</p>
    </div>
    <div class="toast__icon">
      <svg><!-- status icon --></svg>
    </div>
  </div>
  <div class="toast__progress">
    <div class="toast__progress-bar"></div>
  </div>
</div>
```

**Rationale**:
- `toast__dismiss` دکمه بستن — سمت start (راست در RTL)
- `toast__inner` کانتینر محتوا و آیکن — flex row
- `toast__content` عنوان و توضیحات — flex column
- `toast__icon` آیکن وضعیت در دایره رنگی — سمت end (چپ در RTL)
- `toast__progress` نوار پیشرفت تایمر — position absolute، پایین Toast
- ساختار بصری: [dismiss] [text content] [status icon] و در پایین [timer indicator]

### 3. Styling Strategy: CSS Custom Properties
**Decision**: استفاده از CSS Variables برای theming — مطابق الگوی سایر components

```css
:root {
  --toast-color-success-fg: #107c10;
  --toast-color-success-bg: #f1faf1;
  --toast-color-success-stroke: #9fd89f;
  --toast-color-success-bar: #107c10;
  --toast-shadow-success: 0px 4px 7px 0px rgba(16, 124, 16, 0.25);
  /* ... */
}
```

**Rationale**:
- مطابق با الگوی Input، Button، Tag و سایر components
- امکان override کردن توسط developer
- Runtime theming support

### 4. State Management: CSS Modifier Classes
**Decision**: هر واریانت با modifier class مشخص می‌شود

**State Mapping**:
- Success: `.toast--success`
- Danger: `.toast--danger`
- Warning: `.toast--warning`
- Neutral: `.toast--neutral`

**Rationale**:
- ساده و قابل فهم
- مطابق الگوی BEM
- state توسط JavaScript هنگام ایجاد Toast تعیین می‌شود

### 5. Timer Indicator: CSS Animation
**Decision**: استفاده از CSS `@keyframes` animation با `animation-timing-function: linear`

**Rationale**:
- انیمیشن نرم و performant (GPU-accelerated)
- `animation-duration` قابل تنظیم توسط CSS variable یا inline style
- `animationend` event برای callback حذف خودکار
- قابل pause/resume با `animation-play-state` (در صورت نیاز آینده)

### 6. Shadow per Variant
**Decision**: هر واریانت shadow مخصوص خود را دارد با رنگ متناسب

**Rationale**:
- مطابق طراحی Figma
- Shadow رنگی باعث تمایز بصری بیشتر بین واریانت‌ها می‌شود

### 7. Accessibility: role="status" / role="alert"
**Decision**: استفاده از `role="status"` برای Success/Neutral و `role="alert"` برای Danger/Warning

**Rationale**:
- `role="status"` برای اطلاع‌رسانی غیرفوری (polite)
- `role="alert"` برای پیام‌های مهم‌تر (assertive)
- Screen reader به صورت خودکار محتوا را اعلام می‌کند
- Toast نباید فوکوس را از کاربر بگیرد

### 8. Programmatic API: Toast.show()
**Decision**: ارائه متد `Toast.show(options)` برای ایجاد و نمایش Toast با یک خط کد

```javascript
Toast.show({
  variant: 'success',
  title: 'عملیات موفق بود',
  description: 'تغییرات ذخیره شد.',
  duration: 3000,
  container: document.getElementById('myContainer')
});
```

**Rationale**:
- توسعه‌دهنده نیازی به ساخت دستی HTML ندارد
- آیکن‌های پیش‌فرض، role و ساختار HTML به صورت خودکار تنظیم می‌شوند
- Container در صورت نبود به صورت خودکار ساخته می‌شود (`id="toast-container"`)
- المان Toast بازگردانده می‌شود برای کنترل بیشتر (مثلاً `Toast.dismiss()`)
- `Toast.init()` و `Toast.dismiss()` همچنان برای سناریوهای پیشرفته (HTML دستی) موجودند

**Alternatives Considered**:
- فقط `Toast.init()`: توسعه‌دهنده باید HTML کامل را دستی بسازد — پیچیده و خطاپذیر
- Template literals: نیاز به ES6+ — سازگاری کمتر با مرورگرهای قدیمی

## CSS Class Naming Convention

استفاده از BEM (Block Element Modifier):

```css
.toast { }                      /* Block */
.toast__dismiss { }             /* Element: close button */
.toast__inner { }               /* Element: content + icon container */
.toast__content { }             /* Element: title + description */
.toast__title { }               /* Element: title text */
.toast__description { }         /* Element: description text */
.toast__icon { }                /* Element: status icon circle */
.toast__progress { }            /* Element: progress bar container */
.toast__progress-bar { }        /* Element: progress bar fill */

.toast--success { }             /* Modifier: Success variant */
.toast--danger { }              /* Modifier: Danger variant */
.toast--warning { }             /* Modifier: Warning variant */
.toast--neutral { }             /* Modifier: Neutral variant */
```

## Risks / Trade-offs

### Risk 1: CSS Animation vs JavaScript Timer
**Risk**: CSS animation ممکن است در برخی مرورگرها دقت timing متفاوتی داشته باشد

**Mitigation**:
- استفاده از `animationend` event به جای `setTimeout` برای sync بودن با animation
- Fallback به JavaScript timer در صورت عدم پشتیبانی

### Risk 2: Multiple Toast Instances
**Risk**: چندین Toast همزمان ممکن است overlap کنند

**Mitigation**:
- Stacking و positioning خارج از scope این کامپوننت است
- مستندسازی نحوه استفاده از Toast container برای مدیریت موقعیت

### Risk 3: Timer and Dismiss Interaction
**Risk**: تداخل بین animation end و manual dismiss

**Mitigation**:
- حذف event listener بعد از dismiss دستی
- چک کردن وجود المان قبل از حذف

### Risk 4: Accessibility with Auto-dismiss
**Risk**: کاربران screen reader ممکن است قبل از خواندن پیام، Toast حذف شود

**Mitigation**:
- `role="status"` / `role="alert"` اطمینان از اعلام پیام
- مدت زمان پیش‌فرض کافی برای خواندن (5 ثانیه پیشنهادی)
- امکان تنظیم مدت زمان توسط developer

## Migration Plan

### Phase 1: Initial Implementation
1. ساخت CSS component
2. ساخت JavaScript API (تایمر، dismiss)
3. تست در demo page
4. مستندسازی

### Phase 2: Integration
1. استفاده در یک feature واقعی
2. جمع‌آوری feedback
3. رفع bugs و بهبودها
