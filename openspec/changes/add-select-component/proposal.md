# Change: Add Select Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Select قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit. کامپوننت Select برای انتخاب مقدار از میان گزینه‌های موجود استفاده می‌شود و معمولاً وضعیت یا رفتار بعدی سیستم را تعیین می‌کند. سلکت‌ها یک انتخاب را مشخص می‌کنند و در فرم‌ها و تنظیمات مختلف کاربرد گسترده‌ای دارند.

## What Changes
- افزودن کامپوننت Select با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای dropdown، search، انتخاب آیتم و مدیریت تگ‌ها
- پشتیبانی از 4 نوع اصلی (Type):
  - **Basic**: انتخاب ساده — نمایش متنی مقدار انتخاب شده، دارای فیلد جستجو در dropdown
  - **Primary (Single Select)**: انتخاب تکی با تگ — نمایش مقدار انتخاب شده به صورت تگ بنفش با قابلیت حذف
  - **Multiple**: انتخاب چندگانه — نمایش مقادیر انتخاب شده به صورت تگ‌های خاکستری با قابلیت حذف
  - **Tagify**: مشابه Multiple با آیکن close-square به جای close-remove
- پشتیبانی از **3 اندازه** (Size): کوچک (Small)، متوسط (Medium)، بزرگ (Large)
- **وضعیت‌ها (States)**:
  - **Rest**: حالت پیش‌فرض — border خاکستری
  - **Active/Focused**: border بنفش (#8a38f5) + shadow بنفش
  - **Selected**: نمایش مقدار انتخاب شده (متن یا تگ)
  - **Disabled**: پس‌زمینه خاکستری، غیرفعال
- **Dropdown**:
  - لیست آیتم‌ها با shadow مخصوص
  - آیتم انتخاب شده با پس‌زمینه بنفش و متن بنفش
  - فیلد جستجو (در نوع Basic)
  - Scrollbar سفارشی (در نوع Basic)
- **تگ‌ها**:
  - تگ تکی (Primary): پس‌زمینه بنفش روشن، متن بنفش
  - تگ چندگانه (Multiple): پس‌زمینه خاکستری روشن، متن خاکستری
  - آیکن حذف روی هر تگ
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: select (new capability)
- **Dependencies**:
  - tokens.json (already created inside select component)
- Affected code:
  - /components/select/select.css (new)
  - /components/select/select.js (new)
  - /components/select/tokens.json (already created)
  - /components/select/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (برای dropdown toggle، search، انتخاب آیتم، مدیریت تگ و keyboard navigation)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <!-- Basic Select -->
  <div class="select select--basic" data-type="basic">
    <button class="select__trigger" aria-haspopup="listbox">
      <span class="select__value">انتخاب کنید</span>
      <svg class="select__chevron"><!-- chevron icon --></svg>
    </button>
    <div class="select__dropdown">
      <div class="select__search">
        <input type="text" class="select__search-input" placeholder="جستجو..." />
      </div>
      <ul class="select__list" role="listbox">
        <li class="select__item" role="option">گزینه اول</li>
        <li class="select__item select__item--selected" role="option" aria-selected="true">گزینه دوم</li>
        <li class="select__item" role="option">گزینه سوم</li>
      </ul>
    </div>
  </div>

  <!-- Primary (Single) Select -->
  <div class="select select--primary" data-type="primary">
    <div class="select__trigger" aria-haspopup="listbox">
      <div class="select__tags">
        <span class="select__tag select__tag--single">
          گزینه انتخاب شده
          <button class="select__tag-close" aria-label="حذف">
            <svg><!-- close icon --></svg>
          </button>
        </span>
      </div>
      <svg class="select__chevron"><!-- chevron icon --></svg>
    </div>
    <div class="select__dropdown">
      <ul class="select__list" role="listbox">
        <li class="select__item" role="option">گزینه اول</li>
      </ul>
    </div>
  </div>

  <!-- Multiple Select -->
  <div class="select select--multiple" data-type="multiple">
    <div class="select__trigger" aria-haspopup="listbox">
      <div class="select__tags">
        <span class="select__tag select__tag--multiple">
          گزینه ۱
          <button class="select__tag-close" aria-label="حذف">
            <svg><!-- close icon --></svg>
          </button>
        </span>
        <span class="select__tag select__tag--multiple">
          گزینه ۲
          <button class="select__tag-close" aria-label="حذف">
            <svg><!-- close icon --></svg>
          </button>
        </span>
      </div>
      <svg class="select__chevron"><!-- chevron icon --></svg>
    </div>
    <div class="select__dropdown">
      <ul class="select__list" role="listbox" aria-multiselectable="true">
        <li class="select__item select__item--selected" role="option" aria-selected="true">گزینه ۱</li>
        <li class="select__item select__item--selected" role="option" aria-selected="true">گزینه ۲</li>
        <li class="select__item" role="option">گزینه ۳</li>
      </ul>
    </div>
  </div>
  ```
- **Type Management**: CSS modifier classes (`.select--basic`, `.select--primary`, `.select--multiple`, `.select--tagify`)
- **State Management**: CSS classes (`.select--active`, `.select--disabled`, `.select--open`)
- **Accessibility**: WCAG 2.1 Level AA (`role="listbox"`, `role="option"`, `aria-selected`, `aria-haspopup`, `aria-expanded`, keyboard navigation)
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **Type determines tag style**: Basic نشان‌دهنده متن ساده، Primary تگ بنفش، Multiple تگ‌های خاکستری، Tagify مشابه Multiple با آیکن متفاوت
2. **Active state consistent**: همه تایپ‌ها در حالت active/focused دارای border بنفش (#8a38f5) و shadow بنفش هستند
3. **Disabled blocks interaction**: در حالت disabled هیچ تعاملی ممکن نیست — پس‌زمینه و رنگ متن تغییر می‌کند
4. **Selected item highlight**: آیتم انتخاب شده در dropdown با پس‌زمینه بنفش روشن و متن بنفش مشخص می‌شود
5. **Search only in Basic**: فیلد جستجو فقط در نوع Basic وجود دارد
6. **Scrollbar only in Basic**: اسکرول‌بار سفارشی فقط در نوع Basic نمایش داده می‌شود
7. **Tag close removes selection**: کلیک روی آیکن حذف تگ، آن گزینه را از انتخاب خارج می‌کند
8. **Dropdown outside of flow**: dropdown باید خارج از flow اصلی قرار گیرد تا layout صفحه را تغییر ندهد
9. **Single select in Primary**: در نوع Primary فقط یک آیتم قابل انتخاب است
10. **Multi select in Multiple/Tagify**: در نوع Multiple و Tagify چند آیتم قابل انتخاب هستند
