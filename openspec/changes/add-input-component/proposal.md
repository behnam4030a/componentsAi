# Change: Add Input Component (Pure CSS)

## Why
ساخت یک کامپوننت Input قابل استفاده مجدد با CSS برای سیستم طراحی FrontLayer EsanjUiKit. اینپوت‌ها به کاربران اجازه می‌دهند تا داده‌های متنی کوتاه و آزاد را وارد کنند. این کامپوننت باید از design tokens استخراج شده از Figma پیروی کند و تمام stateها، سایزها و قابلیت‌های آیکن تعریف شده در UI Kit را پشتیبانی نماید.

## What Changes
- افزودن کامپوننت Input به صورت Pure CSS (بدون JavaScript برای استایل‌دهی)
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming)
- پشتیبانی از 6 وضعیت تعاملی/سیستمی (State):
  - **Rest**: حالت پیش‌فرض
  - **Hover** (`:hover`): وقتی نشانگر روی input قرار می‌گیرد
  - **Focused** (`:focus-within`): وقتی cursor داخل فیلد است
  - **Error** (`.input--error`): وقتی ورودی نامعتبر است یا خطا دارد
  - **Disabled** (`disabled` attribute): وقتی input غیرفعال است
  - **ReadOnly** (`readonly` attribute): وقتی input قابل انتخاب/کپی هست اما قابل ویرایش نیست
- پشتیبانی از 3 سایز: Large (45px), Medium (37px), Small (24px)
  - size روی height, padding, font-size, line-height, gap, icon size و divider size تأثیر می‌گذارد
- **Icon Integration** (با Icon Component):
  - `beforeTextIcon`: آیکن قبل از متن (سمت start — راست در RTL)
  - `afterTextIcon`: آیکن بعد از متن (سمت end — چپ در RTL)
  - رنگ آیکن از قوانین state تبعیت می‌کند (مشابه رنگ placeholder)
  - اندازه آیکن از طریق mapping از Input.size به Icon.size تعیین می‌شود
  - Divider عمودی بین beforeTextIcon و متن نمایش داده می‌شود
- **Accessible Indicator**: خط پایینی (1.5px) که بر اساس state تغییر می‌کند:
  - Rest: مخفی
  - Hover: قابل مشاهده (#c0c1c3)
  - Focused: قابل مشاهده (#2abb9c)
  - Error/Disabled/ReadOnly: مخفی
- **State Priority** (در صورت همپوشانی): disabled > error > focused > hover > rest
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: input (new capability)
- **Dependencies**:
  - tokens.json (already created inside input component)
- Affected code:
  - /components/input/input.css (new)
  - /components/input/tokens.json (already created)
  - /components/input/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + native HTML `<input>` element (بدون JavaScript برای استایل‌دهی)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <div class="input input--large">
    <div class="input__container">
      <span class="input__icon input__icon--before"><!-- icon --></span>
      <span class="input__divider"></span>
      <input type="text" class="input__field" placeholder="متن نگهدارنده" />
      <span class="input__icon input__icon--after"><!-- icon --></span>
    </div>
    <span class="input__indicator"></span>
  </div>
  ```
- **State Management**: CSS-based (`:hover`, `:focus-within`, `[readonly]`, `:disabled`, `.input--error`)
- **Accessibility**: WCAG 2.1 Level AA (focus states, ARIA attributes, color contrast)
- **RTL Support**: Full support for Persian/Arabic text via CSS `direction` and flexbox
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **State Priority**: disabled > error > focused > hover > rest
2. **Disabled Rules**: هیچ state تعاملی دیگری (hover/focused) نباید فعال شود؛ کلیک و تایپ غیرممکن
3. **ReadOnly Rules**: امکان focus و انتخاب متن مجاز؛ تغییر مقدار غیرمجاز؛ ظاهر متفاوت (بدون border، پس‌زمینه خاکستری)
4. **Error Rules**: error اولویت بالاتر از focused دارد؛ استایل ترکیبی error+focused در صورت تعریف
5. **Icon Integration**: آیکن‌ها باید با Icon Component رندر شوند؛ Input فقط جایگذاری و فاصله/تراز را کنترل می‌کند
6. **Size Effects**: size باید height, padding, font-size, line-height, gap, icon size و divider size را تغییر دهد
7. **State Affects All Elements**: تغییر state باید همزمان روی container، متن، placeholder و آیکن‌ها اعمال شود
8. **Not for Multi-line**: برای جمع‌آوری بیش از یک خط اطلاعات، از Textarea استفاده شود
