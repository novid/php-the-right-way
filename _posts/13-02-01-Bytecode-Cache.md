---
title: ذخیره‌سازی Bytecode
isChild: true
anchor: bytecode_cache
---

## ذخیره‌سازی Bytecode {#bytecode_cache_title}

زمانی که یک فایل PHP اجرا می‌شود، در پشت صحنه ابتدا به یک فایل bytecode یا opcode کامپایل شده، سپس این فایل bytecode اجرا می‌شود. اگر فایل PHP تغییر نکند، خروجی bytecode همیشه ثابت خواهد بود. این بدان معناست که عملیات کامپایل در این صورت فقط منابع پردازنده را هدر می‌دهد.

این دقیقا جایی است که ذخیره‌سازی Bytecode به میان می‌آید. این عمل منجر به نگهداری فایل bytecode در حافظه شده و از کامپایل مجدد و بیهوده‌ی آن جلوگیری می‌کند. پیاده‌سازی این نوع ذخیره‌سازی تنها چند دقیقه زمان می‌برد و بعد از آن متوجه افزایش سرعت نرم‌افزار خواهید شد. حقیقتا دلیلی وجود ندارد که از آن استفاده نکنیم.

با انتشار PHP 5.5، یک ذخیره‌ساز درونی به نام [OPcache](http://php.net/manual/en/book.opcache.php) وجود دارد. البته برای نسخه‌های قبل از آن نیز موجود بود.

سایر ذخیره‌سازهای Bytecode عبارتند از:

* [APC](http://php.net/manual/en/book.apc.php) (برای PHP 5.4 و قبل از آن)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (قسمتی از زِند سرور)
* [WinCache](http://www.iis.net/download/wincacheforphp) (افزونه‌ای برای ویندوز سرور)
