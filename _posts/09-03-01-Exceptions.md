---
title: استثنا
isChild: true
anchor: exceptions
---

## استثنا {#exceptions_title}

استثناها بخشی استاندارد در اکثر زبان‌های برنامه‌نویسی هستند، اما اغلب در PHP نادیده گرفته می‌شوند. زبان‌هایی مانند روبی که دارای خطایابی سنگین هستند، هر زمان اتفاقی در آن‌ها بیفتد (یک درخواست HTTP ناقص به پایان برسد، پرس و جو از پایگاه داده اشتباه باشد یا حتی یک فایل تصویری پیدا نشود) بلافاصله با ایجاد و نمایش آن خطا شما را مطلع می‌سازند.

اما PHP با اینطور مسائل به روشی سهل‌انگارانه برخورد می‌کند، مانند فراخوانی تابع `()file_get_contents` که در صورت پیدا نکردن فایل یک عبارت `FALSE` و یک هشدار باز می‌گرداند. بسیاری از چارچوب‌های نرم‌افزاری قدیمی‌ PHP مانند CodeIgniter تنها یک مقدار false باز می‌گردانند یا آن را در سیستم داخلی خود ذخیره کرده و در نهایت با استفاده از متدی مانند `()this->upload->get_error$` کاربر را در جریان خطا قرار می‌دهند. مشکل اینجاست برای اینکه درک کنید این متد چه نوع خطایی را گزارش می‌دهد باید در مستندات دنبال آن بگردید به جای اینکه از اسم و روش نامگذاری آن متوجه نوع خطا شوید.

مشکل دیگر با کلاس‌هایی است که به صورت خودکار خطا را در نمایشگر نشان می‌دهند و بلافاصله فرآیند اجرا خاتمه می‌یابد. با اینکار شما توانایی مدیریت خطا توسط سایر توسعه‌دهندگان را نادیده می‌گیرید. استثناها باید ایجاد شوند تا یک توسعه‌دهنده از بروز خطا آگاهی یابد، سپس آن‌ها هستند که تصمیم می‌گیرند چگونه خطا را مدیریت کنند. برای نمونه:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // The validation failed
}
catch(Fuel\Email\SendingFailedException $e)
{
    // The driver could not send the email
}
finally
{
    // Executed regardless of whether an exception has been thrown, and before normal execution resumes
}
{% endhighlight %}

### استثناها در کتابخانه‌ی استاندارد PHP

کلاس عمومی `Exception` زمینه‌ی خطایابی محدودی برای توسعه‌دهنده ایجاد می‌کند. اگرچه، برای غلبه بر این محدودیت، این امکان وجود دارد از کلاس اصلی `Execption` ارث‌بری کنیم:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

این بدان معنی است که می‌توانید حالت‌های مختلفی جهت بررسی خطا در این کلاس تعریف کنید. این کار منجر به تولید **بسیاری** موارد استثنا خواهد شد، که برخی از آن‌ها به صورت کلی توسط [افزونه SPL][splext] نادیده گرفته می‌شوند.

برای نمونه اگر از تابع `()call__` استفاده کنید و طی آن یک متد نامعتبر فراخوانی شود به جای اینکه یک استثنا از نوع استاندارد ایجاد شود، می‌توانید به راحتی از استثنایی مانند `throw new BadMethodCallException` استفاده کنید.

* [درباره‌ی استثناها بیشتر بخوانید][exceptions]
* [درباره‌ی افزونه‌ی SPL بیشتر بخوانید][splexe]
* [استفاده‌ی تودرتو از استثناها در PHP][nesting-exceptions-in-php]
* [بهترین روش‌های استفاده از استثنا در PHP5.3][exception-best-practices53]

[exceptions]: http://php.net/manual/en/language.exceptions.php
[splexe]: http://php.net/manual/en/spl.exceptions.php
[splext]: /#standard_php_library
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
