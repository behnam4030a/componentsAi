# Change: Add Tab Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Tab (تب) قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit.
تب (Tab) یعنی سوئیچ بین چند نمای هم‌سطح داخل یک صفحه — بدون اینکه کاربر از صفحه خارج شود.
این کامپوننت شامل دو نوع اصلی (Underline و Filled) و پشتیبانی از آیکن و badge است.

## What Changes
- افزودن کامپوننت Tab با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای مدیریت تغییر تب فعال

### ساختار کلی تب
کامپوننت تب از دو بخش تشکیل شده:
1. **Tab List (نوار تب)**: نوار افقی حاوی آیتم‌های تب — ارتفاع 48px، border-radius 8px، padding افقی 24px، gap 12px
2. **Tab Items (آیتم‌های تب)**: هر آیتم شامل متن، آیکن اختیاری و badge اختیاری — padding افقی 12px، عمودی 16px

### انواع (Variants) — بر اساس 4 صفحه Figma

#### 1. Tab 1 — Underline (خط زیر — پیش‌فرض)
- Container: پس‌زمینه سفید (#ffffff)، چینش آیتم‌ها `justify-end`
- تب فعال: خط زیر 2px سبز (#26a88c)، فونت `FA/Web/Caption EMP` — Medium (500)، رنگ متن #222323
- تب غیرفعال: بدون خط زیر، فونت `FA/Web/Caption` — Regular (400)، رنگ متن #59595a
- تب فعال تمام ارتفاع container را بگیرد (خط زیر در پایین container)

#### 2. Tab 2 — Filled (پر شده / Pill)
- Container: **بدون** پس‌زمینه سفید (شفاف)، چینش آیتم‌ها `justify-end`
- تب فعال: پس‌زمینه سبز (#26a88c)، فونت Medium (500)، رنگ متن سفید (#ffffff)، ارتفاع 38px، border-radius 8px
- تب غیرفعال: بدون پس‌زمینه، فونت Regular (400)، رنگ متن #59595a
- تب غیرفعال تمام ارتفاع container را بگیرد، تب فعال ارتفاع 38px

#### 3. Tab 3 — Underline + Icon (خط زیر با آیکن)
- مشابه Underline اما با آیکن SVG سایز 20px (در باکس 24px) بعد از متن (سمت چپ متن در RTL)
- فاصله آیکن تا متن: 10px (gap)
- Container: پس‌زمینه سفید، چینش `justify-center` (وسط‌چین)
- رنگ آیکن مطابق رنگ متن (فعال: #222323، غیرفعال: #59595a)

#### 4. Tab 4 — Underline + Badge (خط زیر با عدد)
- مشابه Underline اما تب فعال دارای badge عددی (مثلا "۳")
- سایز badge: 15×15px
- فاصله badge تا متن: 5px (gap)
- Container: پس‌زمینه سفید، چینش `justify-end`
- badge قبل از متن در HTML قرار می‌گیرد (در RTL سمت چپ متن نمایش می‌یابد)

### توکن‌های طراحی
- فونت: `Peyda(FaNum)`، سایز 13px، line-height 1.3
- فونت فعال: Medium (500) — استایل `FA/Web/Caption EMP`
- فونت غیرفعال: Regular (400) — استایل `FA/Web/Caption`
- رنگ‌ها: سبز برند #26a88c، متن فعال #222323، متن غیرفعال #59595a
- فاصله‌ها: container padding-x 24px، gap 12px، item padding-x 12px، item padding-y 16px

### امکانات
- **Click to switch**: کلیک روی هر تب آن را فعال می‌کند
- **Content panel**: هر تب می‌تواند به یک پنل محتوا متصل شود
- **Keyboard**: پشتیبانی از Arrow keys برای جابجایی بین تب‌ها
- **RTL**: پشتیبانی کامل از راست به چپ
- **Accessibility**: `role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`
- **Auto-init**: فعال‌سازی خودکار هنگام DOMContentLoaded

## Impact
- Affected specs: tab (new capability)
- **Dependencies**:
  - tokens.json (already created inside tab component)
- Affected code:
  - /components/tab/tab.css (new)
  - /components/tab/tab.js (new)
  - /components/tab/tokens.json (already created)
  - /components/tab/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (برای تغییر تب فعال، keyboard navigation و ARIA)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <!-- Underline Tabs (default) -->
  <div class="tab" data-tab-group="my-tabs">
    <div class="tab__list" role="tablist">
      <button class="tab__item tab__item--active" role="tab">جزئیات حساب</button>
      <button class="tab__item" role="tab">اطلاع رسانی</button>
      <button class="tab__item" role="tab">امنیت</button>
    </div>
  </div>

  <!-- Filled Tabs -->
  <div class="tab tab--filled" data-tab-group="my-tabs-2">
    <div class="tab__list" role="tablist">
      <button class="tab__item tab__item--active" role="tab">جزئیات حساب</button>
      <button class="tab__item" role="tab">اطلاع رسانی</button>
      <button class="tab__item" role="tab">امنیت</button>
    </div>
  </div>

  <!-- Underline Tabs with Icons -->
  <div class="tab" data-tab-group="my-tabs-3">
    <div class="tab__list" role="tablist">
      <button class="tab__item tab__item--active" role="tab">
        <span class="tab__icon"><svg>...</svg></span>
        <span class="tab__text">جزئیات حساب</span>
      </button>
      <button class="tab__item" role="tab">
        <span class="tab__icon"><svg>...</svg></span>
        <span class="tab__text">اطلاع رسانی</span>
      </button>
    </div>
  </div>

  <!-- Underline Tabs with Badge -->
  <div class="tab" data-tab-group="my-tabs-4">
    <div class="tab__list" role="tablist">
      <button class="tab__item tab__item--active" role="tab">
        <span class="tab__text">امنیت</span>
        <span class="tab__badge">۳</span>
      </button>
      <button class="tab__item" role="tab">اطلاع رسانی</button>
    </div>
  </div>

  <!-- Tab Panels (optional) -->
  <div class="tab__panel tab__panel--active" role="tabpanel">محتوای تب اول</div>
  <div class="tab__panel" role="tabpanel">محتوای تب دوم</div>
  ```
- **CSS Modifier Classes**:
  - `.tab--filled` — نوع پر شده (pill) — پیش‌فرض underline
  - `.tab__item--active` — تب فعال
- **BEM Elements**:
  - `.tab__list` — نوار حاوی آیتم‌ها
  - `.tab__item` — هر آیتم تب
  - `.tab__text` — متن تب (وقتی آیکن یا badge هم وجود دارد)
  - `.tab__icon` — آیکن تب (20px)
  - `.tab__badge` — badge عددی تب (15px)
- **JavaScript API**:
  - `Tab.activate(groupId, index)` — فعال کردن تب با index
  - `Tab.init(element)` — فعال‌سازی یک تب جدید
  - `Tab.initAll()` — فعال‌سازی همه تب‌ها
  - `Tab.onChange(groupId, fn)` — تنظیم callback تغییر تب
- **Accessibility**: WCAG 2.1 Level AA (`role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected`, Arrow keys)
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **فونت 13px**: سایز متن تب‌ها 13px با line-height 1.3 — استایل `FA/Web/Caption`
2. **ارتفاع container**: 48px با padding افقی 24px و gap 12px
3. **رنگ برند**: #26a88c برای خط زیر و پس‌زمینه filled
4. **رنگ متن فعال**: #222323 (در underline) یا #ffffff (در filled)
5. **رنگ متن غیرفعال**: #59595a
6. **Container سفید فقط در underline**: در filled پس‌زمینه سفید وجود ندارد
7. **ارتفاع filled فعال**: 38px (نه تمام ارتفاع container) با border-radius 8px
8. **چینش آیتم‌ها**: `justify-end` (تراز به سمت شروع در RTL) — در نوع آیکن‌دار `justify-center`
9. **آیکن**: سایز 20px (در باکس 24px) با gap 10px — بعد از متن (سمت چپ در RTL)
10. **Badge**: سایز 15×15px با gap 5px — قبل از متن در HTML (سمت چپ متن در RTL)
11. **RTL**: چینش آیتم‌ها از راست به چپ — flex row-reverse اتوماتیک
12. **تب فعال در underline**: تمام ارتفاع container — border-bottom در پایین container
