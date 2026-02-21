# Change: Add Link Component (CSS-only)

## Why
ساخت کامپوننت Link (لینک) برای سیستم طراحی FrontLayer EsanjUiKit.
لینک‌ها متن‌هایی تغییر ظاهر داده شده هستند که کاربر را به جایی دیگر هدایت می‌کنند — مکانی داخلی یا سایر اپلیکیشن‌ها و صفحات خارجی. این کامپوننت کلاس‌های CSS ارائه می‌دهد که استایل لینک‌ها را مطابق سیستم طراحی Figma اعمال می‌کند.

> از لینک‌ها برای تحریک کاربران برای اقدام استفاده نکنید، به جای آن یک دکمه شفاف را امتحان کنید.

## What Changes
- افزودن کامپوننت Link به صورت Pure CSS (بدون JavaScript)
- **2 سایز** مطابق با Figma: Large و Medium
- **استفاده از کامپوننت Typography** برای استایل‌های فونت (سایز، وزن، ارتفاع خط)
- کلاس `.link` فقط استایل‌های اختصاصی لینک را اضافه می‌کند (رنگ، خط زیر، cursor)

### Design Tokens (از Figma)
| Token | Value |
|-------|-------|
| Color (default) | `#0078d4` (Color/Shared/Blue/primary) |
| Text Decoration | `underline` |

### سایزها (از Typography)
| Size | Typography Class | Font Size | Weight | Line Height |
|------|------------------|-----------|--------|-------------|
| Large | `.typo--body-large-200` | 16px | Regular (400) | 2 |
| Medium | `.typo--body-medium-200` | 14px | Regular (400) | 2 |

### ساختار HTML
```html
<!-- لینک بزرگ -->
<a href="#" class="typo typo--body-large-200 link">لینک متن</a>

<!-- لینک متوسط -->
<a href="#" class="typo typo--body-medium-200 link">لینک متن</a>
```

### CSS Custom Properties
```css
:root {
  --link-color: #0078d4;
  --link-text-decoration: underline;
}
```

## Impact
- Affected specs: link (new capability)
- **Dependencies**: tokens.json (already created), typography component (existing)
- Affected code:
  - `components/link/link.css` (new)
  - `components/link/tokens.json` (already exists)
  - `components/link/index.html` (new — demo page)
  - `index.html` (update — add link CSS)

## Technical Details
- **Technology Stack**: CSS3 only (بدون JavaScript)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json — already created)
- **Typography Integration**: سایز، وزن و ارتفاع خط فونت از کامپوننت Typography ارث‌بری می‌شود. کلاس `.link` فقط مسئول color، text-decoration و cursor است.

### BEM Naming
- `.link` — کلاس اختصاصی لینک (color, text-decoration, cursor)
- سایزبندی از طریق کلاس‌های Typography: `.typo.typo--body-large-200` یا `.typo.typo--body-medium-200`

### RTL Support
- از Typography ارث‌بری می‌شود (text-align: right, RTL-first)

### Browser Support
- Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
