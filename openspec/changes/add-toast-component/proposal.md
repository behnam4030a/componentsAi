# Change: Add Toast Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Toast قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit. کامپوننت Toast برای نمایش پیام‌های موقتی و غیرمسدودکننده به کاربر استفاده می‌شود. Toast معمولا برای اطلاع‌رسانی نتیجه یک عمل (موفق، خطا، هشدار یا خنثی) نمایش داده می‌شود و بعد از مدت مشخصی به‌صورت خودکار حذف می‌گردد یا توسط کاربر بسته می‌شود. اطلاعات موجود در Toast مفید و مرتبط است اما هرگز حیاتی نیست.

## What Changes
- افزودن کامپوننت Toast با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای تایمر، dismiss و ایجاد دینامیک (`Toast.show()`)
- پشتیبانی از 4 واریانت وضعیت (State):
  - **Success**: عملیات موفقیت‌آمیز (سبز)
  - **Danger**: خطا یا اخطار بحرانی (قرمز)
  - **Warning**: هشدار (نارنجی)
  - **Neutral**: اطلاع‌رسانی خنثی (خاکستری)
- **ساختار محتوا**:
  - **dismiss button** (آیکن ضربدر): بستن دستی Toast
  - **title**: متن اصلی Toast (الزامی)
  - **description**: متن توضیحی (اختیاری)
  - **status icon**: آیکن وضعیت در دایره رنگی (بر اساس state)
  - **timer indicator**: نوار پیشرفت پایینی (auto dismiss)
- **Timer Indicator (Auto Dismiss)**:
  - نوار افقی در پایین Toast از حالت پر (full) به خالی (empty)
  - حرکت پیوسته و یکنواخت (linear)
  - رنگ نوار بر اساس state تعیین می‌شود
  - پس از اتمام تایمر، Toast خودکار حذف می‌شود
- **Manual Dismiss**:
  - کلیک روی dismiss button: تایمر متوقف و Toast فوراً حذف می‌شود
  - منطق حذف (state management) خارج از خود کامپوننت است
- **Shadow**: هر واریانت shadow مخصوص خود را دارد
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: toast (new capability)
- **Dependencies**:
  - tokens.json (already created inside toast component)
- Affected code:
  - /components/toast/toast.css (new)
  - /components/toast/toast.js (new)
  - /components/toast/tokens.json (already created)
  - /components/toast/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (برای تایمر، dismiss، ایجاد دینامیک با `Toast.show()` و مدیریت نمایش)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <div class="toast toast--success" role="status">
    <button class="toast__dismiss" aria-label="بستن">
      <svg><!-- close icon --></svg>
    </button>
    <div class="toast__inner">
      <div class="toast__content">
        <p class="toast__title">عنوان اعلان موفقیت</p>
        <p class="toast__description">متن توضیحی اختیاری</p>
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
- **State Management**: CSS modifier classes (`.toast--success`, `.toast--danger`, `.toast--warning`, `.toast--neutral`)
- **Programmatic API**: `Toast.show({ variant, title, description, duration, container })` — ساخت کامل Toast با یک خط کد. آیکن‌ها، role و HTML به صورت خودکار تنظیم می‌شوند.
- **Accessibility**: WCAG 2.1 Level AA (role="status"/"alert", keyboard dismiss, screen reader support)
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State determines colors**: state تعیین‌کننده رنگ‌های اصلی Toast شامل timer indicator، آیکن وضعیت و تاکیدات بصری (border/shadow/accent)
2. **Typography fixed across states**: محتوای متنی (title و description) از نظر ساختار ثابت است و فقط رنگ‌ها با state تغییر می‌کنند
3. **Timer Rules**: حرکت نوار باید linear باشد؛ تایمر فقط نشانگر زمان است و نباید layout را تغییر دهد
4. **Non-blocking**: Toast غیرمسدودکننده است و نباید فوکوس را از کاربر بگیرد
5. **No hover/focus on Toast itself**: فقط dismiss button حالت hover/focus دارد
6. **Icon Rules**: رنگ آیکن از قوانین رنگ Toast تبعیت می‌کند و نباید مستقل تعیین شود
7. **Description optional**: در صورت نبود description، layout باید بدون فضای خالی اضافی تنظیم شود
8. **Multiple instances**: Toast می‌تواند همزمان چند نمونه فعال داشته باشد
9. **Stacking/positioning out of scope**: ترتیب نمایش و محل نمایش خارج از محدوده این کامپوننت است
10. **Animation non-interference**: انیمیشن ورود/خروج نباید با تایمر تداخل داشته باشد
