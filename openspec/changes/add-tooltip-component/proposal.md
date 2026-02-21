# Change: Add Tooltip Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Tooltip قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit. تولتیپ یک پیام کوچک و مرتفع است و در زمانی که شخصی روی یک عنصر رابط کاربری مرتبط قرار می‌گیرد (hover) یا تمرکز می‌کند (focus)، اطلاعات غیر ضروری و متنی را ارائه می‌کند. تولتیپ باید برای ارائه اطلاعات ساده و مفید استفاده شود؛ از آن برای نمایش بازخورد سیستم استفاده نکنید. اگر نیاز به ارائه اطلاعات تعاملی دارید، به جای آن پاپ‌اور را امتحان کنید.

## What Changes
- افزودن کامپوننت Tooltip با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای نمایش/مخفی کردن و positioning
- پشتیبانی از **4 جهت** (Position):
  - **Top**: tooltip بالای trigger ظاهر می‌شود (فلش به سمت پایین)
  - **Bottom (Down)**: tooltip پایین trigger ظاهر می‌شود (فلش به سمت بالا)
  - **Right**: tooltip سمت راست trigger ظاهر می‌شود (فلش به سمت چپ)
  - **Left**: tooltip سمت چپ trigger ظاهر می‌شود (فلش به سمت راست)
- **ساختار محتوا**:
  - **بدنه tooltip**: مستطیل با گوشه‌های گرد و پس‌زمینه تیره (#364455)
  - **متن**: اطلاعات ساده و مفید — سفید، 14px، Medium
  - **فلش (arrow)**: مثلث کوچک به سمت trigger
- **رفتار نمایش**:
  - ظاهر شدن هنگام hover روی trigger
  - ظاهر شدن هنگام focus روی trigger
  - مخفی شدن هنگام خروج mouse یا از دست دادن focus
- استفاده از design tokens از فایل tokens.json
- پشتیبانی کامل از متن فارسی (RTL)

## Impact
- Affected specs: tooltip (new capability)
- **Dependencies**:
  - tokens.json (already created inside tooltip component)
- Affected code:
  - /components/tooltip/tooltip.css (new)
  - /components/tooltip/tooltip.js (new)
  - /components/tooltip/tokens.json (already created)
  - /components/tooltip/index.html (new - demo page)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (برای نمایش/مخفی کردن، positioning و مدیریت hover/focus)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <div class="tooltip" data-tooltip="اطلاعات ساده در مورد کلید" data-tooltip-position="right">
    <button class="btn btn--primary btn--large">متن پیشفرض</button>
  </div>
  ```
- **Position Management**: CSS modifier classes (`.tooltip--right`, `.tooltip--left`) یا `data-tooltip-position` attribute
- **Accessibility**: `role="tooltip"`, `aria-describedby`, keyboard accessible via focus
- **RTL Support**: Full support for Persian/Arabic text
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **فقط اطلاعاتی**: tooltip فقط برای نمایش اطلاعات ساده و متنی استفاده شود، نه برای محتوای تعاملی
2. **Non-blocking**: tooltip نباید مانع تعامل کاربر شود
3. **Hover و Focus**: tooltip فقط هنگام hover یا focus نمایش داده شود
4. **بدون تعامل داخلی**: محتوای tooltip قابل کلیک یا انتخاب نیست — برای محتوای تعاملی از Popover استفاده کنید
5. **Arrow الزامی**: فلش/مثلث کوچک همیشه به سمت trigger اشاره می‌کند
6. **یک خط متن**: tooltip برای پیام‌های کوتاه طراحی شده، نه متن‌های طولانی
7. **تأخیر نمایش**: امکان تنظیم تأخیر برای جلوگیری از نمایش ناخواسته
