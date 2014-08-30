---
isChild: true
anchor: windows_setup
---

## نصب در ویندوز {#windows_setup_title}

در ویندوز نسخه‌های مختلفی از PHP وجود دارد. شما می‌توانید از [باینری‌های مخصوص ویندوز][php-downloads] یا فایل‌های msi استفاده کنید. فایل‌های msi از نسخه‌ی PHP 5.3.0 به بعد توسعه داده نشدند.

به منظور یادگیری و استفاده شخصی می‌توانید از وب سرور پیش فرض PHP که از نسخه‌ی 5.4 به بالا قابل دسترسی است استفاده کنید. اگر تمایل دارید از بسته‌های کاملی که شامل یک وب سرور کامل و پایگاه داده‌ی MySQL هستند استفاده کنید ابزارهایی مانند [Web Platform Installer][wpi] و [Zend Server CE][zsce] و [XAMPP][xampp] و [EasyPHP][easyphp] و [WAMP][wamp] وجود دارند که به سرعت می‌توانید کار را با آن‌ها آغاز کنید. توجه داشته باشید، این ابزارها نسب به محیط اصلی سرور کمی متفاوت عمل می‌کنند و شما باید متوجه تغییرات آن‌ها در مقایسه با محیط سرورهای مبتنی بر لینوکس باشید.

اگر قصد دارید محیط اصلی توسعه نرم‌افزار تحت وب در ویندوز را پیاده‌سازی کنید بنابراین IIS7 بهترین گزینه برای شماست. شما می‌توانید از پلاگین [phpmanager][phpmanager] جهت پیکربندی PHP در ویندوز استفاده کنید. IIS7 به صورت پیش فرض با FastCGI ارایه می‌شود، تنها کافی است PHP را به صورت یک کنترل‌کننده در آن تنظیم کنید. جهت پشتیبانی و دسترسی به منابع بیشتر [وبسایت iis.net بخشی مختص][dedicated area on iis.net][php-iis] به PHP به دارد.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/en/products/server-ce/
[xampp]: http://www.apachefriends.org/en/xampp.html
[easyphp]: http://www.easyphp.org/
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
