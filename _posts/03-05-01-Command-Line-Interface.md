---
title: رابط خط فرمان
isChild: true
anchor: command_line_interface
---

## رابط خط فرمان {#command_line_interface_title}

هدف اصلی از توسعه‌ی PHP ایجاد نرم‌افزارهای تحت وب است اما می‌توان از آن در نرم‌افزارهای خط فرمان (CLI) استفاده کرد. برنامه‌های خط فرمان مبتنی بر PHP می‌توانند در تست، توسعه و مدیریت نرم‌افزار، مورد استفاده قرار گیرند.

این گونه نرم‌افزارها بسیار قدرتمند هستند چرا که شما می‌توانید به صورت مستقیم با کد ارتباط برقرار کنید و نیازی به رابط گرافیکی تحت وب نیست، فقط اطمینان حاصل کنید نرم‌افزار خط فرمان شما در محیط عمومی قرار نداشته باشد!

اجرای PHP از خط فرمان:

{% highlight bash %}
> php -i
{% endhighlight %}

گزینه `i-` تنظیمات محیط PHP را نمایش می‌دهد درست مانند تابع [`phpinfo`][phpinfo].

گزینه `a-` یک پوسته (Shell) تعاملی را فراهم می‌آورد، شبیه به IRB در Ruby یا پوسته‌ی تعاملی در Python. همچنین [گزینه‌های][cli-options] کاربردی دیگری نیز وجود دارند.

بیایید یک برنامه‌ی ساده "Hello, $name" بنویسیم. جهت آزمایش، فایل `hello.php` را طبق خطوط زیر ایجاد کنید.

{% highlight php %}
<?php
if ($argc != 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

بر اساس آرگومان‌هایی که اسکریپت شما با آن اجرا می‌شود، PHP دو متغیر مخصوص را راه‌اندازی می‌کند. [`argc$`][argc] یک متغیر عددی که *تعداد* آرگومان‌ها را مشخص می‌کند و [`argv$`][argv] یک متغیر از نوع آرایه که *مقدار* هر آرگومان را ذخیره می‌کند. اولین آرگومان همیشه نام فایل اسکریپت است، در اینجا `hello.php`.

عبارت `()exit` به همراه یک عدد غیر صفر به کار رفته است که به پوسته اعلام می‌کند فرمان دریافت‌شده نامعتبر است. کدهای متداول برای این عبارت از [این قسمت][exit-codes] قابل دسترسی هستند.

برای اجرای اسکریپت بالا، از خط فرمان:

{% highlight bash %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [درباره‌ی اجرای PHP از خط فرمان بیشتر بدانید][php-cli]
 * [درباره‌ی اجرای PHP از خطر فرمان در سیستم عامل ویندوز بیشتر بدانید][php-cli-windows]

[phpinfo]: http://php.net/manual/en/function.phpinfo.php
[cli-options]: http://www.php.net/manual/en/features.commandline.options.php
[argc]: http://php.net/manual/en/reserved.variables.argc.php
[argv]: http://php.net/manual/en/reserved.variables.argv.php
[php-cli]: http://php.net/manual/en/features.commandline.php
[php-cli-windows]: http://www.php.net/manual/en/install.windows.commandline.php
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits
