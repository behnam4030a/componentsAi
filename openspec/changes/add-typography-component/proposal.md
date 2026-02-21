# Change: Add Typography Component (CSS-only)

## Why
ساخت کامپوننت Typography (تایپوگرافی) برای سیستم طراحی FrontLayer EsanjUiKit.
تایپوگرافی «سیستم کنترل متن» در UI است — نه فقط انتخاب فونت. این کامپوننت مجموعه‌ای از کلاس‌های CSS utility ارائه می‌دهد که تمام استایل‌های متنی سیستم طراحی را پوشش می‌دهد و در تمام دمو صفحات بقیه کامپوننت‌ها استفاده خواهد شد.

## What Changes
- افزودن کامپوننت Typography به صورت Pure CSS (بدون JavaScript)
- **22 استایل متنی** مطابق با Figma: از display تا button-small
- ارائه کلاس‌های utility با نام‌گذاری BEM: `.typo` (base) + `.typo--{style-name}` (modifier)
- بروزرسانی دمو صفحات تمام کامپوننت‌های موجود برای استفاده از Typography

### فونت پایه
- Family: `Peyda(FaNum), sans-serif`

### دسته‌بندی استایل‌ها

#### Display & Title (نمایشی و عنوان بزرگ)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| display | Bold (700) | 58px | 75px |
| large-title | SemiBold (600) | 40px | 52px |

#### Headings (سرتیترها)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| heading-1 | Bold (700) | 32px | 1.3 |
| heading-2 | SemiBold (600) | 28px | 1.3 |
| heading-3 | SemiBold (600) | 24px | 1.3 |
| heading-4 | SemiBold (600) | 20px | 1.3 |
| heading-5 | Medium (500) | 18px | 1.3 |
| heading-6 | Medium (500) | 16px | 1.3 |

#### Body Large (متن بدنه بزرگ — 16px)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| body-large-200 | Regular (400) | 16px | 2 |
| body-large-150 | Regular (400) | 16px | 1.5 |
| body-large-emp | Medium (500) | 16px | 1.5 |

#### Body Medium (متن بدنه متوسط — 14px)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| body-medium-200 | Regular (400) | 14px | 2 |
| body-medium-150 | Regular (400) | 14px | 1.5 |
| body-medium-emp | Medium (500) | 14px | 1.5 |

#### Body Small (متن بدنه کوچک — 12px)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| body-small-200 | Regular (400) | 12px | 2 |
| body-small-150 | Regular (400) | 12px | 1.5 |
| body-small-emp | Medium (500) | 12px | 1.5 |

#### Caption (زیرنویس — 13px)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| caption | Regular (400) | 13px | 1.3 |
| caption-emp | Medium (500) | 13px | 1.3 |

#### Button (دکمه)
| Style | Weight | Size | Line Height |
|-------|--------|------|-------------|
| button-large | Medium (500) | 14px | 1.4 |
| button-medium | Medium (500) | 14px | 1.4 |
| button-small | Medium (500) | 12px | 1.4 |

### الگوی نام‌گذاری variant ها
- **200** = فاصله خطوط زیاد (line-height: 2) — برای متن‌های طولانی و پاراگراف‌ها
- **150** = فاصله خطوط معمولی (line-height: 1.5) — برای متن‌های عادی
- **emp** (emphasis) = وزن Medium بجای Regular — برای تأکید

### ساختار HTML
```html
<!-- عنوان display -->
<h1 class="typo typo--display">عنوان اصلی</h1>

<!-- سرتیتر -->
<h2 class="typo typo--heading-1">سرتیتر اول</h2>

<!-- متن بدنه -->
<p class="typo typo--body-medium-150">متن بدنه با فاصله خطوط معمولی</p>

<!-- متن تأکیدی -->
<p class="typo typo--body-medium-emp">متن بدنه تأکیدی</p>

<!-- زیرنویس -->
<span class="typo typo--caption">متن زیرنویس</span>
```

### CSS Custom Properties
هر استایل از طریق CSS custom properties تعریف می‌شود تا قابلیت override داشته باشد:
```css
:root {
  --typo-font-family: 'Peyda(FaNum)', sans-serif;
  --typo-display-size: 58px;
  --typo-display-weight: 700;
  --typo-display-line-height: 75px;
  /* ... */
}
```

## Impact
- Affected specs: typography (new capability)
- **Dependencies**: tokens.json (already created)
- Affected code:
  - `/components/typography/typography.css` (new)
  - `/components/typography/tokens.json` (already exists)
  - `/components/typography/index.html` (new — demo page)
  - `/index.html` (update — add typography CSS link)
  - تمام `components/*/index.html` (update — اضافه کردن link به typography.css برای استفاده در دموها)

## Technical Details
- **Technology Stack**: CSS3 only (بدون JavaScript — کامپوننت فقط CSS utility classes است)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json — already created)
- **CSS-only**: این کامپوننت هیچ JavaScript ندارد

### BEM Naming
- `.typo` — کلاس پایه (font-family + direction + letter-spacing)
- `.typo--display` تا `.typo--button-small` — modifier classes (هر کدام font-size, font-weight, line-height)

### RTL Support
- text-align: right به صورت پیش‌فرض (RTL-first)
- پشتیبانی از `[dir="ltr"]` برای text-align: left

### Browser Support
- Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **فونت واحد**: تمام استایل‌ها از فونت `Peyda(FaNum)` استفاده می‌کنند
2. **letterSpacing**: صفر برای تمام استایل‌ها
3. **lineHeight**: display و large-title مقدار پیکسلی دارند (75px, 52px)، بقیه ratio (1.3, 1.4, 1.5, 2)
4. **وزن‌های مورد استفاده**: Regular (400), Medium (500), SemiBold (600), Bold (700)
5. **سایزهای مورد استفاده**: 12px, 13px, 14px, 16px, 18px, 20px, 24px, 28px, 32px, 40px, 58px
