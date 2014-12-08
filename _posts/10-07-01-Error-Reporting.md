---
title: گزارش خطا
isChild: true
anchor: error_reporting
---

## گزارش خطا {#error_reporting_title}

ثبت و گزارش خطا روشی مناسب جهت عیب‌یابی نرم‌افزار است اما در صورتی که اقدامات لازم جهت محرمانه بودن این خطاها صورت نگیرد می‌تواند منجر به فاش شدن ساختار نرم‌افزار شما گردد. برای اینکه این مشکل به وجود نیاید باید تنظیمات متفاوتی در محیط توسعه در مقایسه با محیط نهایی نرم‌افزار داشته باشید.

### محیط توسعه

جهت نمایش تمام خطاهای موجود در محیط *توسعه*، تنظیمات زیر را در فایل `php.ini` انجام دهید:

    display_errors = On
    display_startup_errors = On
    error_reporting = -1
    log_errors = On

> استفاده از `1-` تمام خطاهای موجود را نمایش می‌دهد، حتی آن‌هایی که در نسخه‌های بعدی PHP به وجود بیایند. ثابت `E_ALL` رفتاری مشابه به این عملکرد را در نسخه‌ی PHP 5.4 دارد. - [php.net](http://php.net/manual/function.error-reporting.php)

سطح خطا `E_STRICT` در نسخه‌ی PHP 5.3.0 معرفی شد و قسمتی از `E_ALL` نیست، اگرچه در نسخه‌ی PHP 5.4.0 به قسمتی از `E_ALL` تبدیل شد. این به چه معناست؟ در نسخه‌ی PHP 5.3 اگر بخواهید تمام خطاهای موجود را ببینید باید از `1-` یا `E_ALL | E_STRICT` استفاه کنید.

**گزارش خطا با توجه به نسخه‌های مختلف PHP**

* &lt; 5.3 `-1` یا `E_ALL`
* &nbsp; 5.3 `-1` یا `E_ALL | E_STRICT`
* &gt; 5.3 `-1` یا `E_ALL`

### محیط نهایی

جهت پنهان‌سازی تمام خطاهای موجود در محیط *نهایی*، تنظیمات زیر را در فایل `php.ini` انجام دهید:

    display_errors = Off
    display_startup_errors = Off
    error_reporting = E_ALL
    log_errors = On

با استفاده از این تنظیمات، خطاها کماکان در سرور ثبت می‌شوند اما به کاربر نمایش داده نمی‌شوند. برای اطلاعات بیشتر درباره‌ی این تنظیمات، راهنمای رسمی PHP را مشاهده کنید:
With these settings in production, errors will still be logged to the error logs for the web server, but will not be 
shown to the user. For more information on these settings, see the PHP manual:

* [error_reporting](http://php.net/manual/errorfunc.configuration.php#ini.error-reporting)
* [display_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-errors)
* [display_startup_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-startup-errors)
* [log_errors](http://php.net/manual/errorfunc.configuration.php#ini.log-errors)
