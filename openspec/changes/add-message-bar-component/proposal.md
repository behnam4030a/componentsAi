# Change: Add Message Bar Component (CSS + JavaScript)

## Why
ساخت کامپوننت Message Bar (نوار پیام) برای سیستم طراحی FrontLayer EsanjUiKit.
نوار پیام اطلاعات مهمی را در مورد وضعیت کل محصول یا یک بخش انتقال می‌دهد، به عنوان مثال: وضعیت یک صفحه، صفحه گفتگو یا ذخیره یک تنظیم. این اطلاعات نباید به اقدام فوری از طرف کسی نیاز داشته باشد و هرگز نمی‌تواند برای فروش یا تبلیغ استفاده شود.

## What Changes
- افزودن کامپوننت Message Bar با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای نمایش/مخفی‌سازی و بستن پیام

### واریانت‌ها (بر اساس Figma)

#### 1. Info (اطلاع‌رسانی — آبی)
- پس‌زمینه: #f3f9fd (آبی روشن — blue tint_60)
- بوردر: 1px solid #0078d4 (آبی — blue primary)
- آیکن سمت راست: Info circle (دایره با علامت i) — سایز 40px، آیکن داخلی 24px
- متن: بولد (SemiBold 18px) + معمولی (Regular 18px) — رنگ #222323
- سمت چپ: لینک «بیشتر بدانید» با آیکن فلش چپ — فونت SemiBold 15px، رنگ #1a86d9

#### 2. Success (موفقیت — سبز)
- پس‌زمینه: #f1faf1 (سبز روشن — green tint_60)
- بوردر: 1px solid #107c10 (سبز — green primary)
- آیکن سمت راست: Check circle (تیک دایره‌ای) — سایز 40px، آیکن داخلی 24px
- متن: بولد (SemiBold 18px) + معمولی (Regular 18px) — رنگ #222323
- سمت چپ: دکمه بستن (X) — سایز 28px، آیکن داخلی 24px

#### 3. Warning (هشدار — نارنجی)
- پس‌زمینه: #fff9f5 (نارنجی روشن — orange tint_60)
- بوردر: 1px solid #f7630c (نارنجی — orange primary)
- آیکن سمت راست: Danger Triangle (مثلث هشدار) — سایز 40px، آیکن داخلی 24px
- متن: بولد (SemiBold 18px) + معمولی (Regular 18px) — رنگ #222323
- سمت چپ: دکمه بستن (X) — سایز 28px، آیکن داخلی 24px

#### 4. Danger (خطا — قرمز)
- پس‌زمینه: #fdf3f4 (قرمز روشن — cranberry tint_60)
- بوردر: 1px solid #c50f1f (قرمز — cranberry primary)
- آیکن سمت راست: Info circle (دایره با علامت i) — سایز 40px، آیکن داخلی 24px
- متن: بولد (SemiBold 18px) + معمولی (Regular 18px) — رنگ #222323
- سمت چپ: دکمه بستن (X) — سایز 28px، آیکن داخلی 24px

### ساختار کلی
کامپوننت از یک نوار افقی تشکیل شده با:
- **آیکن وضعیت** (سمت راست در RTL): نشان‌دهنده نوع پیام
- **متن پیام** (وسط): شامل بخش بولد (عنوان پیام) + بخش معمولی (توضیحات)
- **عمل** (سمت چپ در RTL): لینک «بیشتر بدانید» (Info) یا دکمه بستن X (Success, Warning, Danger)

### توکن‌های طراحی
- فونت: `Peyda(FaNum), sans-serif`
- سایز فونت متن: 18px (Regular و SemiBold)
- سایز فونت لینک: 15px (SemiBold)
- رنگ‌ها:
  - Info: bg #f3f9fd، stroke #0078d4، link #1a86d9
  - Success: bg #f1faf1، stroke #107c10
  - Warning: bg #fff9f5، stroke #f7630c
  - Danger: bg #fdf3f4، stroke #c50f1f
  - متن اصلی: #222323، متن ثانویه: #59595a
- فاصله‌ها: padding افقی 19px، padding عمودی 8px، gap محتوا 13px
- سایزها: border 1px، radius 10px، آیکن وضعیت 40px (inner 24px)، آیکن بستن 28px (inner 24px)
- line-height: 1.8

## Impact
- Affected specs: message-bar (new capability)
- **Dependencies**:
  - tokens.json (already created inside message-bar component)
- Affected code:
  - /components/message-bar/message-bar.css (new)
  - /components/message-bar/message-bar.js (new)
  - /components/message-bar/tokens.json (already created)
  - /components/message-bar/index.html (new - demo page)
  - /index.html (update - add message-bar CSS/JS links)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (مدیریت نمایش/بستن پیام)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <!-- Info Message Bar -->
  <div class="message-bar message-bar--info" data-message-bar>
    <div class="message-bar__content">
      <span class="message-bar__icon">
        <svg><!-- info circle icon --></svg>
      </span>
      <p class="message-bar__text">
        <strong class="message-bar__title">این یک پیام اطلاع رسانی است</strong>.
        در صورت نیاز، جزئیات بیشتری در اینجا آمده است.
      </p>
    </div>
    <a href="#" class="message-bar__link">
      <span class="message-bar__link-text">بیشتر بدانید</span>
      <span class="message-bar__link-icon">
        <svg><!-- caret left icon --></svg>
      </span>
    </a>
  </div>

  <!-- Success Message Bar -->
  <div class="message-bar message-bar--success" data-message-bar>
    <div class="message-bar__content">
      <span class="message-bar__icon">
        <svg><!-- check circle icon --></svg>
      </span>
      <p class="message-bar__text">
        <strong class="message-bar__title">موفقیت آمیز بود</strong>.
        در صورت نیاز، جزئیات بیشتری در اینجا آمده است.
      </p>
    </div>
    <button class="message-bar__close" aria-label="بستن">
      <svg><!-- close icon --></svg>
    </button>
  </div>

  <!-- Warning Message Bar -->
  <div class="message-bar message-bar--warning" data-message-bar>
    <div class="message-bar__content">
      <span class="message-bar__icon">
        <svg><!-- danger triangle icon --></svg>
      </span>
      <p class="message-bar__text">
        <strong class="message-bar__title">هشدار</strong>.
        توضیحات تکمیلی.
      </p>
    </div>
    <button class="message-bar__close" aria-label="بستن">
      <svg><!-- close icon --></svg>
    </button>
  </div>

  <!-- Danger Message Bar -->
  <div class="message-bar message-bar--danger" data-message-bar>
    <div class="message-bar__content">
      <span class="message-bar__icon">
        <svg><!-- info circle icon --></svg>
      </span>
      <p class="message-bar__text">
        <strong class="message-bar__title">خطا</strong>.
        توضیحات تکمیلی.
      </p>
    </div>
    <button class="message-bar__close" aria-label="بستن">
      <svg><!-- close icon --></svg>
    </button>
  </div>
  ```

- **CSS Modifier Classes**:
  - `.message-bar--info` — واریانت اطلاع‌رسانی (آبی)
  - `.message-bar--success` — واریانت موفقیت (سبز)
  - `.message-bar--warning` — واریانت هشدار (نارنجی)
  - `.message-bar--danger` — واریانت خطا (قرمز)
  - `.message-bar--hidden` — مخفی شده (بعد از بستن)

- **BEM Elements**:
  - `.message-bar` — wrapper اصلی
  - `.message-bar__content` — بخش آیکن + متن
  - `.message-bar__icon` — آیکن وضعیت
  - `.message-bar__text` — متن پیام
  - `.message-bar__title` — بخش بولد متن
  - `.message-bar__link` — لینک «بیشتر بدانید» (فقط Info)
  - `.message-bar__link-text` — متن لینک
  - `.message-bar__link-icon` — آیکن فلش لینک
  - `.message-bar__close` — دکمه بستن (Success, Warning, Danger)

- **JavaScript API**:
  - `MessageBar.init()` — فعال‌سازی همه message barها
  - `MessageBar.show(element)` — نمایش یک message bar
  - `MessageBar.hide(element)` — مخفی کردن یک message bar
  - `MessageBar.onClose(element, fn)` — callback بستن پیام

- **Accessibility**: `role="status"`، `aria-label` روی دکمه بستن
- **RTL Support**: پشتیبانی کامل — آیکن وضعیت سمت راست، عمل سمت چپ
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

### Responsive Breakpoints
کامپوننت با ۳ breakpoint واکنش‌گرا است:

#### Desktop (بالای 768px) — حالت پیش‌فرض Figma
- چینش: تک‌خطی افقی (آیکن + متن + عمل)
- فونت متن: 18px، فونت لینک: 15px
- آیکن وضعیت: 40px (inner 24px)
- padding: 8px 19px، gap: 13px

#### Tablet (480–767px)
- چینش: تک‌خطی فشرده
- فونت متن: 15px، فونت لینک: 13px
- آیکن وضعیت: 34px (inner 20px)
- padding: 8px 14px، gap: 10px

#### Mobile (زیر 480px)
- **Info**: لینک «بیشتر بدانید» به خط دوم منتقل می‌شود (flex-wrap)
- **Success, Warning, Danger**: تک‌خطی باقی می‌ماند، دکمه بستن بالا-چپ (align-items: flex-start)
- فونت متن: 14px، فونت لینک: 12px
- آیکن وضعیت: 28px (inner 18px)، آیکن بستن: 24px (inner 18px)
- padding: 10px 12px، gap: 8px

## Important Constraints
Based on Figma design system documentation:
1. **بوردر**: 1px solid — آبی (#0078d4) برای Info، سبز (#107c10) برای Success، نارنجی (#f7630c) برای Warning، قرمز (#c50f1f) برای Danger
2. **border-radius**: 10px
3. **ارتفاع**: auto (حداقل ~77px بر اساس محتوا)
4. **padding**: 8px عمودی، 19px افقی (desktop) — کاهشی در breakpointهای کوچکتر
5. **آیکن وضعیت**: container 40px، inner 24px (desktop) — مقیاس‌پذیر
6. **آیکن بستن**: container 28px، inner 24px (desktop) — مقیاس‌پذیر
7. **فونت متن**: Regular 18px + SemiBold 18px، line-height 1.8 (desktop) — مقیاس‌پذیر
8. **فونت لینک**: SemiBold 15px، line-height 1.8 (desktop) — مقیاس‌پذیر
9. **RTL**: آیکن وضعیت سمت راست، عمل (لینک/بستن) سمت چپ
10. **لینک Info**: رنگ #1a86d9 (آبی)، با آیکن فلش چپ
11. **عرض**: 100% (responsive)
12. **Responsive**: سه breakpoint — desktop (>768px)، tablet (480-767px)، mobile (<480px)
