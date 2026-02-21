# Change: Add Textarea Component (Pure CSS)

## Why
ساخت یک کامپوننت Textarea قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. ناحیه متنی (Textarea) به کاربران امکان می‌دهد چندین خط متن آزاد را وارد کنند، مانند یک نظر. اگر فقط به دریافت یک خط اطلاعات نیاز باشد، از کامپوننت Input استفاده شود. این کامپوننت باید از design tokens استخراج شده از Figma پیروی کند و تمام stateها، سایزها و قابلیت resize تعریف شده در UI Kit را پشتیبانی نماید.

## What Changes
- افزودن کامپوننت Textarea به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 6 وضعیت تعاملی/سیستمی (State):
  - **Rest**: حالت پیش‌فرض
  - **Hover** (`:hover`): وقتی نشانگر روی textarea قرار می‌گیرد
  - **Focused** (`:focus-within`): وقتی فوکوس روی textarea است (cursor داخل فیلد)
  - **Error** (`.textarea--error`): وقتی ورودی نامعتبر است یا خطا دارد
  - **Disabled** (`disabled` attribute): وقتی textarea غیرفعال است
  - **ReadOnly** (`readonly` attribute): وقتی textarea قابل انتخاب/کپی هست اما قابل ویرایش نیست
- پشتیبانی از 3 سایز: Large (72px), Medium (64px), Small (36px)
  - size روی min-height، padding، font-size و line-height تأثیر می‌گذارد
- **Resize Handler** (قابلیت تغییر اندازه):
  - `resizeHandler = true`: کاربر می‌تواند اندازه textarea را تغییر دهد (فقط عمودی)؛ هندل resize قابل مشاهده
  - `resizeHandler = false`: تغییر اندازه غیرفعال؛ اندازه توسط layout کنترل می‌شود
  - در حالت disabled، resize غیرفعال است حتی اگر resizeHandler = true باشد
- **Accessible Indicator**: خط پایینی (1.5px) که بر اساس state تغییر می‌کند:
  - Rest: مخفی (opacity: 0)
  - Hover: قابل مشاهده (#59595a)
  - Focused: قابل مشاهده (#2abb9c)
  - Error/Disabled/ReadOnly: مخفی
- **State Priority** (در صورت همپوشانی): disabled > error > focused > hover > rest
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)
- **قوانین Typography و Placeholder مشابه Input**:
  - استایل متن واردشده و placeholder در هر state مشخص
  - تغییر state همزمان روی container، متن واردشده و placeholder اعمال می‌شود

## Impact
- Affected specs: textarea (new capability)
- **Dependencies**:
  - tokens.json (already created inside textarea component)
- Affected code:
  - /components/textarea/textarea.css (new)
  - /components/textarea/tokens.json (already created)
  - /components/textarea/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + native HTML `<textarea>` element (بدون JavaScript برای استایل‌دهی)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <div class="textarea textarea--large">
    <div class="textarea__container">
      <textarea class="textarea__field" placeholder="متن نگهدارنده"></textarea>
    </div>
    <span class="textarea__indicator"></span>
  </div>
  ```
- **State Management**: CSS-based (`:hover`, `:focus-within`, `[readonly]`, `:disabled`, `.textarea--error`)
- **Accessibility**: WCAG 2.1 Level AA (focus states, ARIA attributes, color contrast)
- **RTL Support**: Full support for Persian/Arabic text via CSS `direction` and flexbox
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State Priority**: disabled > error > focused > hover > rest
2. **Disabled Rules**: هیچ state تعاملی دیگری (hover/focused) نباید فعال شود؛ تایپ و تغییر مقدار غیرممکن؛ resize غیرفعال حتی اگر resizeHandler = true
3. **ReadOnly Rules**: امکان focus و انتخاب متن مجاز؛ تغییر مقدار غیرمجاز؛ ظاهر متفاوت (بدون border، پس‌زمینه خاکستری)
4. **Error Rules**: اگر همزمان فوکوس وجود داشته باشد، باید استایل ترکیبی "error + focused" اعمال شود (اگر تعریف شده). در غیر این صورت error اولویت بالاتر دارد و فوکوس حداقلی باقی می‌ماند
5. **Resize Handler Rules**: فعال/غیرفعال بودن resize نباید استایل stateها (رنگ‌ها/بوردر) را تغییر دهد
6. **Size Effects**: size باید min-height، padding داخلی، font-size و line-height متن واردشده، font-size و line-height placeholder را تغییر دهد
7. **State Affects All Elements**: تغییر state باید همزمان روی container، متن واردشده و placeholder اعمال شود
8. **Multi-line Field**: Textarea یک فیلد چندخطی است و باید امکان نمایش چند خط متن را داشته باشد
9. **Typography & Placeholder Rules Same as Input**: قوانین تایپوگرافی و placeholder مشابه کامپوننت Input
