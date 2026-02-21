# Change: Add Table Component (CSS + JavaScript)

## Why
ساخت یک کامپوننت Table (جدول) قابل استفاده مجدد برای سیستم طراحی FrontLayer EsanjUiKit.
جدول یعنی نمایش داده‌ی ساخت‌یافته در قالب ردیف و ستون؛ ابزار اصلی برای وقتی که کاربر باید مقایسه کند، اسکن سریع انجام دهد، و روی داده‌ها عمل انجام دهد.
این کامپوننت شامل ۵ حالت (Default, Hover, Click, Selected, Setting) و بخش‌های مختلف (Toolbar, Search, Header, Body, Pagination, Action Bar) است.

## What Changes
- افزودن کامپوننت Table با CSS + JavaScript
- **روش استفاده**: استفاده مستقیم در HTML با CSS classes (BEM naming) + JavaScript API برای مدیریت انتخاب ردیف، پیجینیشن و عملیات دسته‌ای

### ساختار کلی جدول
کامپوننت جدول از ۶ بخش اصلی تشکیل شده:

1. **Tile Header (نوار عنوان)**: شامل عنوان + تعداد + دکمه‌های عملیات (افزودن، بارگذاری گروهی، فیلتر)
2. **Search Box (جستجو)**: فیلد جستجو با آیکن — زیر نوار عنوان
3. **Table Head (سرستون)**: ستون‌های هدر با آیکن و متن — ارتفاع 55px
4. **Table Body (بدنه)**: ردیف‌های داده — ارتفاع هر ردیف 60px — شامل متن، تگ وضعیت، نوار پیشرفت، چک‌باکس
5. **Pagination (صفحه‌بندی)**: دکمه‌های شماره صفحه + انتخاب تعداد ردیف
6. **Action Bar (نوار عملیات)**: نوار پایین برای عملیات دسته‌ای روی ردیف‌های انتخاب شده

### حالت‌ها (States) — بر اساس ۵ صفحه Figma

#### 1. Default — حالت پیش‌فرض
- ردیف‌ها: پس‌زمینه سفید (#ffffff)، border-bottom 1px #e2e4e6
- چک‌باکس‌ها: unchecked، سایز 28px، border 1px #626364، radius 4px
- تگ وضعیت: «فعال» یا «غیرفعال» — bg #f6f8fa، border 2px سفید، radius 8px، ارتفاع 32px
- نوار پیشرفت: «X از Y انجام شده» — عرض 120px، ارتفاع 3px، bg #e2e4e6، fill #26a88c، radius 360px

#### 2. Hover — حالت هاور
- ردیف هاور شده: پس‌زمینه #f6f8fa + خط سبز عمودی 3px در سمت چپ ردیف (border-right در RTL)
- آیکن سه‌نقطه (⋮) در سمت چپ‌ترین ستون ردیف هاور شده نمایش می‌یابد
- سایر ردیف‌ها: بدون تغییر

#### 3. Click — حالت کلیک
- مشابه Hover اما با حالت فشرده/کلیک شده
- خط سبز عمودی + آیکن سه‌نقطه — مشابه هاور
- ردیف کلیک شده: پس‌زمینه #f6f8fa

#### 4. Selected — حالت انتخاب شده
- ردیف‌های انتخاب شده: چک‌باکس checked (bg سبز #26a88c، آیکن سفید)
- پس‌زمینه ردیف‌های انتخاب شده: بدون تغییر رنگ (سفید) اما با border/outline برند
- چندین ردیف قابل انتخاب همزمان

#### 5. Setting — حالت تنظیمات (عملیات دسته‌ای)
- مشابه Selected اما با نوار عملیات (Action Bar) در پایین جدول
- نوار عملیات: پس‌زمینه تیره (#222323)، متن سفید
- نمایش تعداد ردیف‌های انتخاب شده: «۳ ردیف انتخاب شده»
- دکمه‌های عملیات: افزودن آزمون، افزودن به گروه، اعطای دسترسی به مدیران، تغییر وضعیت، حذف کاربران

### بخش‌های جدول — جزئیات طراحی

#### Tile Header (نوار عنوان)
- ارتفاع: auto، padding: 16px 24px، پس‌زمینه سفید، gap 24px
- **عنوان** (سمت راست): فونت SemiBold 20px #222323 — مثال: «لیست کاربران»
- **جداکننده نقطه**: دایره 4px — بین عنوان و تعداد
- **تعداد** (بعد از نقطه): فونت Regular 13px #222323 — مثال: «تعداد: ۴۷ نفر»
- **دکمه‌ها** (سمت چپ):
  - **افزودن کاربر جدید**: bg #26a88c، border #1d836d، متن سفید Medium 14px، آیکن Plus 18px، ارتفاع 45px، radius 8px، shadow inset
  - **بارگذاری گروهی**: bg سفید، border #e2e4e6، متن #222323 Medium 14px، آیکن Upload 18px، ارتفاع 45px، radius 8px
  - **خط جداکننده عمودی**: ارتفاع 30px بین دکمه‌ها
  - **فیلتر**: مشابه بارگذاری گروهی — آیکن Filter 18px

#### Search Box (جستجو)
- ارتفاع: 45px، پس‌زمینه سفید، border #e2e4e6، radius 8px
- آیکن جستجو: 20px (در container 24px)
- Placeholder: «جستجو...» — فونت Regular 14px #59595a
- padding: 0 16px

#### Table Head (سرستون)
- ارتفاع: 55px، پس‌زمینه سفید، border-bottom 1px #e2e4e6
- هر ستون: padding 16px، gap 8px بین آیکن و متن
- متن هدر: فونت Regular 13px #59595a، white-space nowrap
- آیکن هدر: از مجموعه Iconly Pro — سایز متناسب
- **ستون‌ها** (از راست به چپ در RTL):
  1. چک‌باکس (عرض ~52px)
  2. نام و نام خانوادگی (آیکن User)
  3. کد اختصاصی (آیکن Barcode)
  4. شماره تماس (آیکن Phone)
  5. وضعیت آزمون (آیکن Document)
  6. وضعیت (آیکن Setting)

#### Table Body (بدنه)
- هر ردیف: ارتفاع 60px، پس‌زمینه سفید، border-bottom 1px #e2e4e6
- هر سلول: padding 16px (یا px 16px py 18px)
- متن سلول: فونت Regular 14px #222323، line-height 2
- چینش: `align-items: center`، `justify-content: flex-end` (RTL)

#### Status Tag (تگ وضعیت)
- «فعال»: bg #f6f8fa، border 2px سفید، متن #222323، radius 8px، ارتفاع 32px، padding 0 8px
- «غیرفعال»: همان استایل — فقط متن متفاوت (رنگ یکسان)
- فونت: Regular 14px

#### Progress Bar (نوار پیشرفت)
- متن: «X از Y انجام شده» — فونت Regular 14px #222323
- نوار: عرض 120px، ارتفاع 3px، پس‌زمینه #e2e4e6، fill #26a88c
- radius: 360px (pill)، gap 4px بین متن و نوار
- عرض fill متناسب با نسبت X/Y

#### Pagination (صفحه‌بندی)
- padding: 16px 24px
- **دکمه‌های صفحه** (سمت چپ):
  - سایز: 37×37px، radius 8px، border 1px #e2e4e6، bg سفید
  - فونت: Regular 14px #222323
  - shadow: 0px 1px 2px rgba(0,0,0,0.06)
  - **صفحه فعال**: bg #26a88c، متن سفید، border #1d836d
  - دکمه‌های ناوبری: «، ‹، ›، »» (اول، قبل، بعد، آخر)
  - «...» برای صفحات میانی
- **انتخاب تعداد ردیف** (سمت راست): «۱۰ ردیف در هر صفحه ‹» — فونت Regular 14px #222323، border #e2e4e6، radius 8px

#### Action Bar (نوار عملیات دسته‌ای)
- نمایش: فقط وقتی حداقل یک ردیف انتخاب شده
- پس‌زمینه: #222323 (تیره)
- ارتفاع: auto، padding: 12px 24px
- **تعداد انتخاب** (سمت راست): «۳ ردیف انتخاب شده» — فونت Regular 14px سفید + آیکن checkbox سبز
- **دکمه‌های عملیات** (سمت چپ): هر کدام با آیکن + متن — فونت Regular 13px سفید، gap 24px
  - افزودن آزمون، افزودن به گروه، اعطای دسترسی به مدیران، تغییر وضعیت، حذف کاربران

### توکن‌های طراحی
- فونت: `Peyda(FaNum)`
- سایزهای فونت: 20px (عنوان SemiBold)، 14px (بدنه/دکمه Regular/Medium)، 13px (هدر/caption Regular)
- رنگ‌ها: برند #26a88c، برند stroke #1d836d، متن اصلی #222323، متن ثانویه #59595a، stroke #e2e4e6، accessible stroke #626364، light bg #f6f8fa
- فاصله‌ها: cell padding 16px، header gap 24px، button gap 8px، pagination gap 8px
- سایزها: header row 55px، body row 60px، checkbox 28px، tag 32px، pagination btn 37px، progress 120×3px، toolbar btn 45px
- radius: table 8px، checkbox 4px، tag 8px، button 8px، progress 360px

## Impact
- Affected specs: table (new capability)
- **Dependencies**:
  - tokens.json (already created inside table component)
  - کامپوننت checkbox (قبلاً ساخته شده — استفاده مجدد یا پیاده‌سازی inline)
- Affected code:
  - /components/table/table.css (new)
  - /components/table/table.js (new)
  - /components/table/tokens.json (already created)
  - /components/table/index.html (new - demo page)
  - /index.html (update - add table CSS/JS links)

## Technical Details
- **Technology Stack**: CSS3 + JavaScript (مدیریت انتخاب ردیف، پیجینیشن، سرچ، عملیات دسته‌ای)
- **Design Tokens**: Extracted from Figma via MCP (tokens.json)
- **Usage Pattern**:
  ```html
  <div class="table-container" data-table="users">
    <!-- Tile Header -->
    <div class="table__header">
      <div class="table__title-section">
        <h2 class="table__title">لیست کاربران</h2>
        <span class="table__dot"></span>
        <span class="table__count">تعداد: ۴۷ نفر</span>
      </div>
      <div class="table__actions">
        <button class="table__btn table__btn--filter">
          <span class="table__btn-icon"><svg>...</svg></span>
          <span class="table__btn-text">فیلتر</span>
        </button>
        <span class="table__divider"></span>
        <button class="table__btn table__btn--secondary">
          <span class="table__btn-icon"><svg>...</svg></span>
          <span class="table__btn-text">بارگذاری گروهی</span>
        </button>
        <button class="table__btn table__btn--primary">
          <span class="table__btn-icon"><svg>...</svg></span>
          <span class="table__btn-text">افزودن کاربر جدید</span>
        </button>
      </div>
    </div>

    <!-- Search Box -->
    <div class="table__search">
      <span class="table__search-icon"><svg>...</svg></span>
      <input type="text" class="table__search-input" placeholder="جستجو...">
    </div>

    <!-- Table -->
    <table class="table__grid">
      <thead class="table__thead">
        <tr class="table__row table__row--head">
          <th class="table__cell table__cell--checkbox">
            <input type="checkbox" class="table__checkbox">
          </th>
          <th class="table__cell">
            <span class="table__cell-icon"><svg>...</svg></span>
            <span class="table__cell-text">نام و نام خانوادگی</span>
          </th>
          <!-- ... more columns -->
        </tr>
      </thead>
      <tbody class="table__tbody">
        <tr class="table__row">
          <td class="table__cell table__cell--checkbox">
            <input type="checkbox" class="table__checkbox">
          </td>
          <td class="table__cell">علی میرهادی</td>
          <td class="table__cell">۱۲۵۴۹۸۵۳۱۶</td>
          <td class="table__cell">۰۹۲۱۵۸۶۳۶۲۲</td>
          <td class="table__cell">
            <div class="table__progress">
              <span class="table__progress-text">۳ از ۴ انجام شده</span>
              <div class="table__progress-bar">
                <div class="table__progress-fill" style="width:75%"></div>
              </div>
            </div>
          </td>
          <td class="table__cell">
            <span class="table__tag">فعال</span>
          </td>
        </tr>
        <!-- ... more rows -->
      </tbody>
    </table>

    <!-- Pagination -->
    <div class="table__pagination">
      <div class="table__page-size">
        <span>۱۰ ردیف در هر صفحه</span>
        <span class="table__page-size-arrow">‹</span>
      </div>
      <div class="table__page-numbers">
        <button class="table__page-btn">»</button>
        <button class="table__page-btn">›</button>
        <button class="table__page-btn">۵</button>
        <button class="table__page-btn">...</button>
        <button class="table__page-btn">۳</button>
        <button class="table__page-btn table__page-btn--active">۲</button>
        <button class="table__page-btn">۱</button>
        <button class="table__page-btn">‹</button>
        <button class="table__page-btn">«</button>
      </div>
    </div>

    <!-- Action Bar (hidden by default) -->
    <div class="table__action-bar">
      <div class="table__action-count">
        <span class="table__action-icon"><svg>...</svg></span>
        <span>۳ ردیف انتخاب شده</span>
      </div>
      <div class="table__action-buttons">
        <button class="table__action-btn">
          <span class="table__action-btn-icon"><svg>...</svg></span>
          <span>افزودن آزمون</span>
        </button>
        <!-- ... more action buttons -->
      </div>
    </div>
  </div>
  ```

- **CSS Modifier Classes**:
  - `.table__row--hover` — ردیف هاور شده (با JS روی hover اضافه می‌شود)
  - `.table__row--selected` — ردیف انتخاب شده
  - `.table__btn--primary` — دکمه اصلی (سبز)
  - `.table__btn--secondary` — دکمه ثانویه (سفید)
  - `.table__btn--filter` — دکمه فیلتر
  - `.table__page-btn--active` — صفحه فعال (سبز)
  - `.table__tag--active` — تگ فعال (اختیاری)
  - `.table__tag--inactive` — تگ غیرفعال (اختیاری)
  - `.table__action-bar--visible` — نمایش نوار عملیات

- **BEM Elements**:
  - `.table-container` — wrapper اصلی
  - `.table__header` — نوار عنوان
  - `.table__title` — عنوان جدول
  - `.table__count` — تعداد آیتم‌ها
  - `.table__actions` — دکمه‌های عملیات
  - `.table__btn` — دکمه toolbar
  - `.table__divider` — خط جداکننده عمودی
  - `.table__search` — باکس جستجو
  - `.table__grid` — عنصر `<table>`
  - `.table__thead` — `<thead>`
  - `.table__tbody` — `<tbody>`
  - `.table__row` — `<tr>`
  - `.table__cell` — `<th>` یا `<td>`
  - `.table__checkbox` — چک‌باکس ردیف
  - `.table__tag` — تگ وضعیت
  - `.table__progress` — container نوار پیشرفت
  - `.table__progress-bar` — نوار پس‌زمینه
  - `.table__progress-fill` — نوار پر شده
  - `.table__pagination` — بخش صفحه‌بندی
  - `.table__page-btn` — دکمه صفحه
  - `.table__page-size` — انتخاب تعداد ردیف
  - `.table__action-bar` — نوار عملیات دسته‌ای
  - `.table__action-btn` — دکمه عملیات

- **JavaScript API**:
  - `Table.init(element)` — فعال‌سازی یک جدول
  - `Table.initAll()` — فعال‌سازی همه جدول‌ها
  - `Table.getSelected(tableId)` — دریافت ردیف‌های انتخاب شده
  - `Table.selectAll(tableId)` — انتخاب همه ردیف‌ها
  - `Table.deselectAll(tableId)` — لغو انتخاب همه
  - `Table.goToPage(tableId, page)` — رفتن به صفحه مشخص
  - `Table.onSelect(tableId, fn)` — callback انتخاب ردیف
  - `Table.onPageChange(tableId, fn)` — callback تغییر صفحه

- **Accessibility**: `role="table"`, `role="row"`, `role="columnheader"`, `role="cell"`, `aria-selected`, `aria-sort`
- **RTL Support**: پشتیبانی کامل — چینش از راست به چپ
- **Browser Support**: Modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)

## Important Constraints
Based on Figma design system documentation:
1. **فونت عنوان**: SemiBold 20px #222323
2. **فونت هدر**: Regular 13px #59595a با آیکن
3. **فونت بدنه**: Regular 14px #222323
4. **فونت دکمه**: Medium 14px
5. **ارتفاع هدر**: 55px، ارتفاع ردیف: 60px
6. **چک‌باکس**: 28px با border 1px #626364 و radius 4px
7. **تگ وضعیت**: ارتفاع 32px، bg #f6f8fa، border 2px سفید، radius 8px
8. **نوار پیشرفت**: عرض 120px، ارتفاع 3px، radius 360px (pill)
9. **دکمه پیجینیشن**: 37×37px، radius 8px، shadow 0px 1px 2px rgba(0,0,0,0.06)
10. **صفحه فعال**: bg #26a88c، متن سفید، border #1d836d
11. **نوار عملیات**: bg #222323، متن سفید، فقط وقتی ردیف انتخاب شده
12. **هاور ردیف**: bg #f6f8fa + خط سبز عمودی 3px سمت چپ + آیکن سه‌نقطه
13. **RTL**: چینش آیتم‌ها از راست به چپ — ستون چک‌باکس سمت راست
14. **عرض جدول**: 100% (حداکثر 1104px در Figma)
15. **Toolbar height**: دکمه‌ها 45px، padding 16px 24px
16. **Search height**: 45px، radius 8px
