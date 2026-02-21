# Change: Update Tab — Hover State, Colored Variant, Mobile Scroll

## Why
طبق Figma (node 1867-1240)، کامپوننت Tab سه رفتار ندارد که در طراحی مشخص شده:
۱. در hover رنگ متن تب تغییر نمی‌کند
۲. variant با متن رنگی (brand) برای تب فعال وجود ندارد
۳. در موبایل تب‌های overflow اسکرول افقی ندارند

## What Changes
- **ADDED** hover state: رنگ متن تب غیرفعال در hover به brand (#26a88c) تغییر می‌کند
- **ADDED** `.tab--colored` modifier: تب فعال به جای متن تیره (#222323)، متن brand (#26a88c) دارد
- **ADDED** mobile horizontal scroll: `.tab__list` روی موبایل `overflow-x: auto` می‌گیرد

## Impact
- Affected specs: tab
- Affected code: `components/tab/tab.css`, `components/tab/index.html`
