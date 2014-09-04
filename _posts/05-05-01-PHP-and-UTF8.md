---
title: کار با UTF-8
isChild: true
anchor: php_and_utf8
---

## کار با UTF-8 {#php_and_utf8_title}

محتوای اولیه‌ی این بخش توسط [Alex Cabal](https://alexcabal.com/) در مجموعه‌ی [بهترین عادت‌های کدنویسی در PHP](https://phpbestpractices.org/#utf-8) نوشته شده است که در اینجا به عنوان مقدمه‌ی مقاله‌ی ما قرار دارد.

### راهکار ثابتی وجود ندارد. دقت کرده، به جزییات توجه کنید و یکپارچه عمل کنید.

هم اکنون PHP در سطح پایین از یونیکد پشتیبانی نمی‌کند. روش‌هایی وجود دارد تا اطمینان حاصل کنیم تمام رشته‌های UTF-8 به درستی پردازش می‌شوند اما این روش‌ها آسان نیستند و لایه‌های مختلفی از یک نرم‌افزار تحت وب را شامل می‌شوند، از HTML به SQL به PHP. در ادامه آن‌ها را توضیح می‌دهیم.

### UTF-8 در PHP

عملیات پایه روی رشته‌ها، مانند چسباندن دو رشته به یکدیگر یا تخصیص به متغیرها، به عملکرد خاصی رو UFT-8 احتیاج ندارد. با این وجود، بیشتر توابع رشته‌ای، مانند `()strpos` و `()strlen`، به توجه خاصی نیازمند هستند. این توابع معمولا یک معادل `*_mb` نیز دارند: مانند `()mb_strpos` و `()mb_strlen`. توابع `*_mb` با استفاده از [افزونه‌ی Multibyte String] قابل دسترس هستند و به طور خاص برای کار روی رشته‌های یونیکد طراحی شده‌اند.

هر زمان که با رشته‌های یونیکد سروکار دارید باید از توابع `*_mb` استفاده کنید. اگر از `()substr` در یک رشته‌ی UTF-8 استفاده کنید، به احتمال زیاد خروجی شامل کاراکترهای آشفته خواهد بود. در این حالت باید از معادل این تابع یعنی `()mb_substr` استفاده کنید.

مشکل اینجاست که باید یادمان باشد در تمام مدت پروژه از توابع `*_mb` استفاده کنیم. اگر حتی یکبار هم فراموش کنید، احتمال دارد که رشته‌ی یونیکد شما در پردازش‌های بعدی دچار آشفتگی شود.

البته تمام توابع رشته‌ای معادل `*_mb` ندارند و این از بدشانسی شماست که برای عملکرد مورد نظرتان، این معادل‌ها وجود نداشته باشند.

باید از تابع `()mb_internal_encoding` در ابتدای هر اسکریپت PHP (یا اسکریپت سراسری) و از تابع `()mb_http_output` درست بعد از اینکه اسکریپت خروجی را به مرورگر می‌فرستد، استفاده کنید. اینکار موجب می‌شود که در آینده از مشکلات بسیاری جلوگیری کنید.

به علاوه، بسیاری از توابع رشته‌ای در PHP یک پارامتر اختیاری دریافت می‌کنند که نحوه‌ی کدگذاری کاراکترها را مشخص می‌کند. اگر این پارامتر را تعریف می‌کنید حتما باید UTF-8 باشد. برای نمونه، `()htmlentities` گزینه‌ای برای کدگذاری کاراکتر دارد و شما همیشه باید از UTF-8 برای آن استفاده کنید. توجه کنید که از PHP 5.4.0، کدگذاری پیشفرض کاراکترها برای `()htmlentities` و `()htmlspecialchars` با استفاده از UTF-8 صورت می‌گیرد.

در نهایت، اگر نرم‌افزار شما در سرورهای مختلفی قرار دارد و اطمینان ندارید که افزونه‌ی `mbstring` فعال خواهد بود، استفاده از بسته‌ی [patchwork/utf8] در Composer را مد نظر قرار دهید. این بسته در صورت فعال بودن `mbstring` از آن استفاده می‌کند، در غیر اینصورت از توابع عادی رشته‌ای استفاده خواهد کرد.

[افزونه‌ی Multibyte String]: http://php.net/manual/en/book.mbstring.php
[patchwork/utf8]: https://packagist.org/packages/patchwork/utf8

### UTF-8 در MySQL

اگر اسکریپت PHP شما به MySQL دسترسی دارد، احتمال دارد رشته‌های شما به صورت UTF-8 در پایگاه‌داده ذخیره نشوند، هر چند گام‌های بالا را انجام داده باشید.

جهت اطمینان از ذخیره‌سازی رشته‌ها به صورت UTF-8، باید پایگاه‌داده و جدول‌های شما از ساختار `utf8mb4` پشتیبانی کنند و در رشته‌ی اتصال PDO نیز از `utf8mb4` استفاده کنید. به مثال زیر توجه کنید. این مورد _بسیار حایز اهمیت_ است.

توجه کنید که باید از مجموعه کاراکتر `utf8mb4` جهت پشتیبانی کامل از UTF-8 استفاده کنید نه از `utf8`! به قسمت مطاله‌ی بیشتر مراجعه کنید تا دلیل آن را بدانید.

### UTF-8 در مرورگر

از تابع `()mb_http_output` استفاده کنید تا اطمینان یابید اسکریپت PHP خروجی را به صورت UTF-8 به مرورگر می‌فرستد.

اینکار باعث می‌شود به مرورگر گفته شود صفحه را با توجه به ساختار UTF-8 نمایش دهد. روش قدیمی برای انجام اینکار استفاده از [تگ `<meta>` به همراه charset](http://htmlpurifier.org/docs/enduser-utf8.html) بود که در تگ `<head>` قرار می‌گرفت. این روش هم اکنون نیز معتبر است اما تنظیم این ویژگی در قسمت `Content-Type` از header بسیار [سریع‌تر](https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly) است.

{% highlight php %}
<?php
// Tell PHP that we're using UTF-8 strings until the end of the script
mb_internal_encoding('UTF-8');
 
// Tell PHP that we'll be outputting UTF-8 to the browser
mb_http_output('UTF-8');
 
// Our UTF-8 test string
$string = 'Êl síla erin lû e-govaned vîn.';
 
// Transform the string in some way with a multibyte function
// Note how we cut the string at a non-Ascii character for demonstration purposes
$string = mb_substr($string, 0, 15);
 
// Connect to a database to store the transformed string
// See the PDO example in this document for more information
// Note the `set names utf8mb4` commmand!
$link = new \PDO(   
                    'mysql:host=your-hostname;dbname=your-db;charset=utf8mb4',
                    'your-username',
                    'your-password',
                    array(
                        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_EXCEPTION,
                        \PDO::ATTR_PERSISTENT => false
                    )
                );
 
// Store our transformed string as UTF-8 in our database
// Your DB and tables are in the utf8mb4 character set and collation, right?
$handle = $link->prepare('insert into ElvishSentences (Id, Body) values (?, ?)');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->bindValue(2, $string);
$handle->execute();
 
// Retrieve the string we just stored to prove it was stored correctly
$handle = $link->prepare('select * from ElvishSentences where Id = ?');
$handle->bindValue(1, 1, PDO::PARAM_INT);
$handle->execute();
 
// Store the result into an object that we'll output later in our HTML
$result = $handle->fetchAll(\PDO::FETCH_OBJ);

header('Content-Type: text/html; charset=utf-8');
?><!doctype html>
<html>
    <head>
        <title>UTF-8 test page</title>
    </head>
    <body>
        <?php
        foreach($result as $row){
            print($row->Body);  // This should correctly output our transformed UTF-8 string to the browser
        }
        ?>
    </body>
</html>
{% endhighlight %}

### مطالعه‌ی بیشتر

* [PHP Manual: String Operations](http://php.net/manual/en/language.operators.string.php)
* [PHP Manual: String Functions](http://php.net/manual/en/ref.strings.php)
    * [`strpos()`](http://php.net/manual/en/function.strpos.php)
    * [`strlen()`](http://php.net/manual/en/function.strlen.php)
    * [`substr()`](http://php.net/manual/en/function.substr.php)
* [PHP Manual: Multibyte String Functions](http://php.net/manual/en/ref.mbstring.php)
    * [`mb_strpos()`](http://php.net/manual/en/function.mb-strpos.php)
    * [`mb_strlen()`](http://php.net/manual/en/function.mb-strlen.php)
    * [`mb_substr()`](http://php.net/manual/en/function.mb-substr.php)
    * [`mb_internal_encoding()`](http://php.net/manual/en/function.mb-internal-encoding.php)
    * [`mb_http_output()`](http://php.net/manual/en/function.mb-http-output.php)
    * [`htmlentities()`](http://php.net/manual/en/function.htmlentities.php)
    * [`htmlspecialchars()`](http://www.php.net/manual/en/function.htmlspecialchars.php)
* [PHP UTF-8 Cheatsheet](http://blog.loftdigital.com/blog/php-utf-8-cheatsheet)
* [Stack Overflow: What factors make PHP Unicode-incompatible?](http://stackoverflow.com/questions/571694/what-factors-make-php-unicode-incompatible)
* [Stack Overflow: Best practices in PHP and MySQL with international strings](http://stackoverflow.com/questions/140728/best-practices-in-php-and-mysql-with-international-strings)
* [How to support full Unicode in MySQL databases](http://mathiasbynens.be/notes/mysql-utf8mb4)
* [Brining Unicode to PHP with Portable UTF-8](http://www.sitepoint.com/bringing-unicode-to-php-with-portable-utf8/)
