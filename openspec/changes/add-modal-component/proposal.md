# Change: Add Modal Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Modal (مودال) قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit. مودال برای وارد کردن اطلاعات، فرم‌ها و عملیات‌هایی که نیاز به تمرکز کاربر دارند استفاده می‌شود. این کامپوننت شامل نسخه دسکتاپ و موبایل با رفتارهای متفاوت است.

## What Changes
- افزودن کامپوننت Modal با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای باز/بسته شدن، انیمیشن و مدیریت overlay

### ساختار کلی مودال
مودال از سه بخش اصلی تشکیل شده:
1. **Overlay (پس‌زمینه تیره)**: لایه نیمه‌شفاف پشت مودال با گرادیانت
2. **Header (هدر تیره)**: شامل عنوان، آیکن و دکمه بستن — پس‌زمینه تیره (#222323)
3. **Body (بدنه سفید)**: شامل محتوای فرم و دکمه‌های عملیاتی — پس‌زمینه سفید

### نسخه دسکتاپ
- مودال از **سمت راست** وارد صفحه می‌شود (slide-in from right)
- عرض ثابت: **500px**
- ارتفاع: تمام ارتفاع viewport با فاصله 16px از بالا و پایین
- دکمه خروج (×) در بالای هدر
- دکمه اصلی (Primary) در پایین بدنه — عرض کامل
- هدر padding: 24px یکنواخت
- بدنه padding: 24px
- عنوان: فونت SemiBold، سایز 20px

### نسخه موبایل
- مودال از **سمت پایین** وارد صفحه می‌شود (slide-up from bottom)
- عرض: **100%** صفحه
- ارتفاع: بسته به حجم محتوا — امکان قرار گرفتن در بالا، وسط یا پایین صفحه
- هدر padding: افقی 16px، عمودی 24px
- بدنه padding: 16px
- عنوان: فونت Medium، سایز 18px

### سایزها (Size Variants)
- **کوچک (Small)**: عرض 400px (دسکتاپ)
- **متوسط (Medium)**: عرض 500px (دسکتاپ) — پیش‌فرض
- **بزرگ (Large)**: عرض 600px (دسکتاپ)
- در موبایل هر سه سایز عرض 100% می‌شوند

### امکانات
- **Overlay**: کلیک روی overlay مودال را می‌بندد
- **دکمه بستن (×)**: همیشه در هدر قابل مشاهده
- **انیمیشن**: slide-in هنگام باز شدن، slide-out هنگام بسته شدن
- **Scroll**: بدنه مودال در صورت بلند بودن محتوا اسکرول می‌شود
- **Keyboard**: کلید Escape مودال را می‌بندد
- **Focus Trap**: فوکوس در مودال باز محدود می‌شود
- **Body Lock**: هنگام باز بودن مودال، اسکرول صفحه قفل می‌شود
- **Responsive**: تغییر خودکار از نسخه دسکتاپ به موبایل بر اساس عرض صفحه

### توکن‌های طراحی
- استفاده از design tokens موجود در tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: modal (new capability)
- **Dependencies**:
  - tokens.json (already created inside modal component)
  - button component (برای دکمه‌های عملیاتی)
- Affected code:
  - /components/modal/modal.css (new)
  - /components/modal/modal.js (new)
  - /components/modal/tokens.json (already created)
  - /components/modal/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (برای overlay، باز/بسته شدن، انیمیشن، focus trap و keyboard navigation)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <!-- Modal -->
  <div class="modal" id="my-modal">
    <div class="modal__overlay"></div>
    <div class="modal__container">
      <div class="modal__header">
        <button class="modal__close" type="button" aria-label="بستن">
          <svg><!-- close icon --></svg>
        </button>
        <div class="modal__title-block">
          <h2 class="modal__title">عنوان مودال</h2>
          <div class="modal__icon-holder">
            <svg><!-- icon --></svg>
          </div>
        </div>
      </div>
      <div class="modal__body">
        <div class="modal__content">
          <!-- محتوای فرم -->
        </div>
        <div class="modal__actions">
          <button class="btn btn--primary btn--large" style="width:100%">
            تایید
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- باز کردن مودال -->
  <script>
    Modal.open('my-modal');
  </script>
  ```
- **CSS Modifier Classes**:
  - `.modal--sm` / `.modal--md` / `.modal--lg` — سایزها
  - `.modal--open` — مودال باز
  - `.modal--closing` — انیمیشن بسته شدن
- **JavaScript API**:
  - `Modal.open(id)` — باز کردن مودال
  - `Modal.close(id)` — بسته کردن مودال
  - `Modal.closeAll()` — بستن همه مودال‌ها
- **Accessibility**: WCAG 2.1 Level AA (`role="dialog"`, `aria-modal="true"`, `aria-labelledby`, focus trap, Escape key)
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **دسکتاپ از راست وارد می‌شود**: مودال از سمت راست صفحه اسلاید می‌شود
2. **موبایل از پایین وارد می‌شود**: مودال از سمت پایین صفحه اسلاید می‌شود
3. **هدر همیشه تیره است**: پس‌زمینه #222323 با متن سفید
4. **بدنه همیشه سفید است**: پس‌زمینه #ffffff
5. **آیکن‌هولدر**: مربع 54px با پس‌زمینه #2c2d2d و border #454546
6. **Container padding**: لایه بیرونی 4px — ایجاد فاصله بین هدر/بدنه و لبه‌های container
7. **دکمه بستن**: آیکن × سایز 24px در سمت چپ هدر (RTL)
8. **Overlay gradient**: از rgba(0,0,0,0.05) تا rgba(34,35,35,0.3)
9. **Shadow**: -3px 0px 5px 0px rgba(0,0,0,0.1) — سایه سمت چپ
10. **Responsive breakpoint**: در عرض کمتر از 768px نسخه موبایل نمایش داده شود
11. **موبایل بسته به حجم محتوا**: امکان قرار گرفتن در بالا، وسط یا پایین صفحه
