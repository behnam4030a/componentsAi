# مشخصات کامپوننت Button

## ADDED Requirements

### Requirement: هدف و موارد استفاده کامپوننت Button
کامپوننت Button SHALL برای ایجاد اقدام یا رویداد در رابط کاربری استفاده شود، نه برای ناوبری.

#### Scenario: دکمه برای اقدامات مهم
- **زمانی که** کاربر نیاز به ارسال فرم، ایجاد تغییر یا حرکت به مرحله بعد دارد
- **آنگاه** از کامپوننت Button برای این اقدامات مهم استفاده شود

#### Scenario: عدم استفاده برای ناوبری
- **زمانی که** کاربر نیاز به رفتن به صفحه یا مکان دیگری دارد
- **آنگاه** از کامپوننت Link به جای Button استفاده شود

---

### Requirement: انواع ظاهری دکمه (Type Variants)
کامپوننت Button SHALL شش نوع بصری را پشتیبانی کند: Primary، AI، Secondary، Subtle، Outline و Transparent. Type فقط SHALL روی استایل بصری (رنگ، پس‌زمینه، border، شدت سایه) تأثیر بگذارد و نSHALL ساختار (padding، radius، تایپوگرافی) را تغییر دهد مگر آنچه در سیستم طراحی تعریف شده باشد.

#### Scenario: استفاده از CSS classes برای type
- **زمانی که** توسعه‌دهنده نوع دکمه را مشخص کند
- **آنگاه** از CSS class مربوطه استفاده شود: `btn--primary`، `btn--ai`، `btn--secondary`، `btn--subtle`، `btn--outline`، `btn--transparent`

#### Scenario: رندر دکمه Primary
- **زمانی که** class `btn--primary` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه رنگ برند (#26a88c)، متن سفید و افکت سایه primary داشته باشد

#### Scenario: رندر دکمه AI
- **زمانی که** class `btn--ai` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه رنگ AI (#7160e8)، متن سفید و افکت سایه AI داشته باشد

#### Scenario: رندر دکمه Secondary
- **زمانی که** class `btn--secondary` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه سفید، متن تیره، border و سایه secondary داشته باشد

#### Scenario: رندر دکمه Subtle
- **زمانی که** class `btn--subtle` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه سفید، متن تیره و بدون border باشد

#### Scenario: رندر دکمه Outline
- **زمانی که** class `btn--outline` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه شفاف، متن تیره و فقط border داشته باشد

#### Scenario: رندر دکمه Transparent
- **زمانی که** class `btn--transparent` اعمال شود
- **آنگاه** دکمه SHALL پس‌زمینه شفاف، متن به رنگ برند و بدون border باشد

#### Scenario: Type فقط روی استایل تأثیر می‌گذارد
- **زمانی که** هر type به هر size اعمال شود
- **آنگاه** type فقط SHALL ویژگی‌های بصری (رنگ‌ها، سایه‌ها، borderها) را تغییر دهد بدون تأثیر روی ابعاد یا ساختار

#### Scenario: همه Typeها در همه Sizeها کار می‌کنند
- **زمانی که** هر type با هر size مشخص شود
- **آنگاه** دکمه SHALL بدون تداخل به درستی رندر شود

---

### Requirement: سایزهای مختلف دکمه (Size Variants)
کامپوننت Button SHALL سه سایز را پشتیبانی کند: Small، Medium و Large. Size SHALL روی ارتفاع، padding افقی/عمودی، اندازه فونت، line-height، فاصله بین آیکن و متن، و اندازه آیکن تأثیر بگذارد.

#### Scenario: استفاده از CSS classes برای size
- **زمانی که** توسعه‌دهنده سایز دکمه را مشخص کند
- **آنگاه** از CSS class مربوطه استفاده شود: `btn--small`، `btn--medium`، `btn--large`

#### Scenario: سایز Small
- **زمانی که** class `btn--small` اعمال شود
- **آنگاه** دکمه SHALL height=24px، paddingX=8px، fontSize=12px و gap و icon size مناسب داشته باشد

#### Scenario: سایز Medium
- **زمانی که** class `btn--medium` اعمال شود
- **آنگاه** دکمه SHALL height=37px، paddingX=12px، fontSize=14px و gap و icon size مناسب داشته باشد

#### Scenario: سایز Large
- **زمانی که** class `btn--large` اعمال شود
- **آنگاه** دکمه SHALL height=45px، paddingX=16px، fontSize=14px و gap و icon size مناسب داشته باشد

#### Scenario: Size روی تمام ویژگی‌های ابعادی تأثیر می‌گذارد
- **زمانی که** size تغییر کند
- **آنگاه** دکمه SHALL height، padding، font size، line-height، gap آیکن-متن و icon size را به‌روزرسانی کند

#### Scenario: Size روی رفتار state تأثیر نمی‌گذارد
- **زمانی که** size تغییر کند
- **آنگاه** رفتار state و معنای type SHALL بدون تغییر باقی بماند

---

### Requirement: مدیریت وضعیت‌های دکمه (State Management)
کامپوننت Button SHALL چهار وضعیت بصری را با CSS pseudo-classes و modifier classes پشتیبانی کند.

#### Scenario: حالت Rest
- **زمانی که** هیچ تعاملی رخ ندهد
- **آنگاه** دکمه SHALL رنگ‌های حالت rest را از design tokens نمایش دهد

#### Scenario: حالت Hover
- **زمانی که** کاربر روی دکمه hover کند (`:hover`)
- **آنگاه** دکمه SHALL رنگ‌های حالت hover را با transition نرم نمایش دهد

#### Scenario: حالت Pressed
- **زمانی که** کاربر دکمه را فشار دهد (`:active`)
- **آنگاه** دکمه SHALL رنگ‌های حالت pressed را نمایش دهد

#### Scenario: حالت Selected
- **زمانی که** class `btn--selected` اعمال شود
- **آنگاه** دکمه SHALL رنگ‌های حالت selected را نمایش دهد و `aria-pressed="true"` داشته باشد

#### Scenario: حالت Disabled
- **زمانی که** class `btn--disabled` اعمال شود و attribute `disabled` موجود باشد
- **آنگاه** دکمه SHALL بصری کمرنگ، غیرتعاملی و دارای aria-disabled="true" باشد

#### Scenario: ترکیب Selected + Hover
- **زمانی که** دکمه selected باشد و کاربر روی آن hover کند
- **آنگاه** دکمه SHALL استایل ترکیبی "selected + hover" را نمایش دهد

#### Scenario: Pressed همیشه اولویت دارد
- **زمانی که** دکمه فشرده شود (`:active`)
- **آنگاه** حالت pressed SHALL بصری بر تمام حالت‌های دیگر غالب باشد

---

### Requirement: یکپارچگی آیکن
کامپوننت Button SHALL از آیکن‌ها به صورت inline HTML (SVG یا Icon Component) پشتیبانی کند.

#### Scenario: آیکن با ساختار HTML
- **زمانی که** دکمه نیاز به نمایش آیکن دارد
- **آنگاه** آیکن SHALL در یک `<span class="btn__icon">` درون `<span class="btn__inner">` قرار بگیرد

#### Scenario: وراثت رنگ آیکن
- **زمانی که** آیکن SVG با `fill="currentColor"` استفاده شود
- **آنگاه** رنگ آیکن SHALL دقیقاً با رنگ متن دکمه مطابقت داشته باشد

---

### Requirement: موقعیت و چیدمان آیکن
کامپوننت Button SHALL آیکن‌ها را قبل و/یا بعد از متن دکمه با موقعیت‌یابی صحیح RTL/LTR پشتیبانی کند.

#### Scenario: آیکن قبل از متن
- **زمانی که** `<span class="btn__icon">` قبل از `<span class="btn__text">` قرار بگیرد
- **آنگاه** آیکن SHALL در سمت شروع (start) متن قرار گیرد (راست در RTL، چپ در LTR)

#### Scenario: آیکن بعد از متن
- **زمانی که** `<span class="btn__icon">` بعد از `<span class="btn__text">` قرار بگیرد
- **آنگاه** آیکن SHALL در سمت پایان (end) متن قرار گیرد

#### Scenario: فاصله آیکن تا متن
- **زمانی که** آیکن و متن هر دو موجود باشند
- **آنگاه** فاصله بین آیکن و متن SHALL از `gap` در `.btn__inner` تعیین شود

#### Scenario: دکمه فقط آیکن
- **زمانی که** فقط آیکن بدون متن ارائه شده باشد
- **آنگاه** دکمه SHALL با class `btn--icon-only` و padding مساوی رندر شود

#### Scenario: تراز عمودی
- **زمانی که** آیکن و متن رندر شوند
- **آنگاه** تمام عناصر SHALL در مرکز عمودی درون دکمه تراز شوند

---

### Requirement: پشتیبانی از متن راست‌به‌چپ (RTL)
کامپوننت Button SHALL متن راست‌به‌چپ (RTL) را با CSS `direction` property پشتیبانی کند.

#### Scenario: RTL با dir attribute
- **زمانی که** المان والد یا خود دکمه `dir="rtl"` داشته باشد
- **آنگاه** دکمه SHALL چیدمان RTL با موقعیت‌یابی صحیح آیکن‌ها داشته باشد

#### Scenario: LTR با dir attribute
- **زمانی که** المان والد یا خود دکمه `dir="ltr"` داشته باشد
- **آنگاه** دکمه SHALL چیدمان LTR داشته باشد

---

### Requirement: مدیریت فوکوس
کامپوننت Button SHALL نشانگر فوکوس قابل مشاهده برای ناوبری صفحه‌کلید ارائه دهد. فوکوس SHALL مستقل از state باشد و خارج از مرز دکمه رندر شود بدون ایجاد جابجایی چیدمان.

#### Scenario: حلقه فوکوس در ناوبری صفحه‌کلید
- **زمانی که** دکمه از طریق صفحه‌کلید (Tab) فوکوس بگیرد
- **آنگاه** دکمه SHALL حلقه فوکوس را طبق type دکمه نمایش دهد (`:focus-visible`)

#### Scenario: عدم نمایش حلقه فوکوس با کلیک موس
- **زمانی که** دکمه از طریق کلیک موس فوکوس بگیرد
- **آنگاه** دکمه نSHALL حلقه فوکوس نمایش دهد (با استفاده از `:focus-visible`)

#### Scenario: فوکوس مستقل از state است
- **زمانی که** دکمه فوکوس داشته باشد
- **آنگاه** حلقه فوکوس SHALL صرف‌نظر از state (rest، hover، pressed، selected) قابل مشاهده باشد

#### Scenario: فوکوس خارج از مرز رندر می‌شود
- **زمانی که** حلقه فوکوس نمایش داده شود
- **آنگاه** حلقه SHALL خارج از border دکمه رندر شود تا جابجایی چیدمان ایجاد نکند

---

### Requirement: دسترسی‌پذیری (WCAG 2.1 سطح AA)
کامپوننت Button SHALL دسترسی‌پذیر باشد و با استانداردهای WCAG 2.1 سطح AA مطابقت داشته باشد.

#### Scenario: برچسب ARIA
- **زمانی که** متن دکمه ارائه شود
- **آنگاه** دکمه SHALL نام دسترسی‌پذیر از طریق محتوای متنی یا aria-label داشته باشد

#### Scenario: حالت فشرده ARIA برای selected
- **زمانی که** دکمه در حالت selected باشد
- **آنگاه** دکمه SHALL دارای aria-pressed="true" باشد

#### Scenario: حالت غیرفعال ARIA
- **زمانی که** دکمه غیرفعال باشد
- **آنگاه** دکمه SHALL دارای `disabled` attribute و/یا `aria-disabled="true"` باشد

#### Scenario: کنتراست رنگ
- **زمانی که** دکمه در هر ترکیب type/state رندر شود
- **آنگاه** متن SHALL حداقل نسبت کنتراست 4.5:1 با پس‌زمینه داشته باشد

#### Scenario: قابلیت ناوبری با صفحه‌کلید
- **زمانی که** دکمه غیرفعال نباشد
- **آنگاه** دکمه SHALL قابل دسترسی با صفحه‌کلید (Tab, Enter, Space) باشد

---

### Requirement: یکپارچگی با Design Token
کامپوننت Button SHALL از design tokens موجود در tokens.json به عنوان منبع واحد حقیقت استفاده کند.

#### Scenario: ویژگی‌های سفارشی CSS
- **زمانی که** tokens بارگذاری شود
- **آنگاه** کامپوننت SHALL از CSS custom properties در `:root` استفاده کند

#### Scenario: بازنویسی token
- **زمانی که** توسعه‌دهنده ویژگی سفارشی CSS را بازنویسی کند
- **آنگاه** کامپوننت SHALL مقدار بازنویسی شده را رعایت کند

---

### Requirement: عملکرد
کامپوننت Button SHALL سبک و با عملکرد خوب باشد.

#### Scenario: اندازه bundle
- **زمانی که** کامپوننت bundle شود
- **آنگاه** اندازه CSS SHALL کمتر از 10KB فشرده‌نشده باشد

---

### Requirement: سازگاری با مرورگرها
کامپوننت Button SHALL در مرورگرهای مدرن کار کند.

#### Scenario: مرورگرهای پشتیبانی شده
- **زمانی که** کامپوننت در Chrome 90+، Firefox 88+، Safari 14+، Edge 90+ استفاده شود
- **آنگاه** کامپوننت SHALL بدون polyfill کار کند

---

### Requirement: پشتیبانی از لینک‌ها (Link Support)
کامپوننت Button SHALL از المان‌های `<a>` (لینک) علاوه بر `<button>` پشتیبانی کند تا لینک‌هایی با ظاهر دکمه ایجاد شوند.

#### Scenario: استفاده از لینک با ظاهر دکمه
- **زمانی که** توسعه‌دهنده CSS class `btn` را روی یک `<a>` element اعمال کند
- **آنگاه** لینک SHALL همان ظاهر بصری دکمه را داشته باشد

#### Scenario: حفظ href در لینک‌ها
- **زمانی که** یک `<a>` با class `btn` استفاده شود
- **آنگاه** attribute `href` و رفتار ناوبری پیش‌فرض لینک SHALL حفظ شود

#### Scenario: مثال استفاده لینک
- **زمانی که** توسعه‌دهنده کد زیر را بنویسد:
```html
<a href="page.html" class="btn btn--primary btn--large">
  برو به صفحه دیگر
</a>
```
- **آنگاه** یک لینک با ظاهر دکمه Primary و سایز Large ایجاد شود که با کلیک به `page.html` منتقل شود
