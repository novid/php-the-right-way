---
title: استفاده از متغیرهای سراسری
isChild: true
anchor: register_globals
---

## استفاده از متغیرهای سراسری {#register_globals_title}

**تذکر:** از نسخه‌ی PHP 5.4.0 به بالا پیکربندی `register_globals` حذف و غیرقابل استفاده است و در فرآیند برورزسانی یک نرم‌افزار قدیمی به صورت یک اخطار نمایش داده می‌شود.

زمانی که این پیکربندی فعال باشد، منجر به در دسترس بودن تمام متغیرهای سراسری (مانند `GET_$`، `POST_$`، و `REQUEST_$`) در تمام حوزه‌های نرم‌افزار شما خواهد بود که این امر به مشکلات امنیتی بسیار دامن می‌زند و هیچ روشی وجود ندارد که بتوان تعیین کرد داده‌ی ورودی از کدام قسمت وارد نرم‌افزار شده است.

برای نمونه: متغیر `$_GET['foo']` با استفاده از `foo$` نیز قابل دسترسی است، که ممکن است منجر به تعریف متغیرهای نامشخص گردد. اگر از PHP 5.4.0 به پایین استفاده می‌کنید __اطمینان حاصل کنید__ که `register_globals` __غیرفعال باشد__.

* [درباره‌ی register_globals بیشتر بدانید](http://www.php.net/manual/en/security.globals.php)
