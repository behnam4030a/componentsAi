# Change: Add Label Component (Pure CSS)

## Why
ساخت یک کامپوننت Label قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. کامپوننت Label برای نمایش برچسب متنی در کنار یا بالای فیلدها (مثل Input، Select، Checkbox و ...) استفاده می‌شود. این کامپوننت نقش اطلاع‌رسانی دارد و رفتار تعاملی مستقل ندارد، اما ظاهر آن بسته به وضعیت‌هایی مثل required و disabled تغییر می‌کند.

## What Changes
- افزودن کامپوننت Label به صورت Pure CSS (بدون JavaScript)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 4 خصوصیت (Property):
  - **type**: وزن فونت برچسب — `regular` (weight 400) یا `semibold` (weight 500)
    - type فقط روی font-weight اثر می‌گذارد و نباید باعث تغییر رنگ، اندازه یا فاصله‌ها شود
    - semibold معمولاً برای تأکید بیشتر یا عناوین فرم استفاده می‌شود
  - **size**: اندازه تایپوگرافی — `small` (12px)، `medium` (14px)، `large` (16px)
    - size باید روی font-size و line-height اثر بگذارد
    - همه typeها باید در همه sizeها قابل استفاده باشند
  - **disabled**: مشخص می‌کند Label مربوط به یک فیلد غیرفعال است (`label--disabled`)
    - رنگ متن و required indicator به حالت disabled تغییر می‌کند (#bbbcbe)
    - Label خودش تعامل‌پذیر نیست اما visually باید با وضعیت disabled فیلد مرتبط هم‌راستا باشد
  - **required**: نمایش علامت ستاره (*) در کنار متن Label
    - required indicator بخشی از Label است و نباید مستقل مدیریت شود
    - جایگاه indicator: بعد از متن (سمت end — چپ در RTL، راست در LTR)
    - رنگ ستاره: #c50f1f (danger) در حالت عادی، #bbbcbe در حالت disabled
- **Color Rules**:
  - حالت عادی: رنگ پیش‌فرض #222323
  - disabled: رنگ #bbbcbe
  - Label state تعاملی (hover/focus) ندارد
- **Layout Rules**:
  - ساختار بصری: [label text] [required indicator (*)]
  - فاصله بین متن و indicator: 4px (از design tokens)
  - تراز عمودی indicator با baseline متن Label
  - سازگاری کامل با RTL/LTR
- **Behavior Notes**:
  - Label یک کامپوننت نمایشی است و نباید منطق تعاملی یا state مستقل داشته باشد
  - ارتباط Label با فیلد (for/id یا aria-labelledby) در لایه پیاده‌سازی انجام می‌شود
  - required بودن فقط یک نشانه بصری است و منطق اعتبارسنجی فرم را پیاده‌سازی نمی‌کند
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: label (new capability)
- **Dependencies**:
  - tokens.json (already created inside label component)
- Affected code:
  - /components/label/label.css (new)
  - /components/label/tokens.json (already created)
  - /components/label/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + native HTML `<label>` element (بدون JavaScript)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <!-- Basic label -->
  <label class="label label--medium">
    <span class="label__text">برچسب</span>
  </label>

  <!-- Required label -->
  <label class="label label--medium label--required">
    <span class="label__text">برچسب</span>
    <span class="label__required">*</span>
  </label>

  <!-- Semibold required label -->
  <label class="label label--medium label--semibold label--required">
    <span class="label__text">برچسب</span>
    <span class="label__required">*</span>
  </label>

  <!-- Disabled required label -->
  <label class="label label--medium label--required label--disabled">
    <span class="label__text">برچسب</span>
    <span class="label__required">*</span>
  </label>
  ```
- **Accessibility**: WCAG 2.1 Level AA (color contrast, semantic `<label>` element)
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **type فقط font-weight**: تغییر type نباید باعث تغییر رنگ، اندازه یا فاصله‌ها شود
2. **size فقط font-size و line-height**: size باید فقط روی font-size و line-height تأثیر بگذارد
3. **همه typeها در همه sizeها**: ترکیب هر type با هر size باید ممکن باشد
4. **disabled فقط بصری**: Label خودش تعامل‌پذیر نیست، فقط ظاهرش با فیلد مرتبط هم‌راستا می‌شود
5. **required فقط بصری**: منطق validation در Label پیاده‌سازی نمی‌شود
6. **بدون state تعاملی**: Label نباید hover/focus state داشته باشد
7. **required + disabled**: indicator همچنان نمایش داده می‌شود اما با استایل disabled
8. **تایپوگرافی ستاره در Small**: در سایز Small، ستاره 13px/1.3 (Caption) و متن 12px/1.5 (Body Small)
