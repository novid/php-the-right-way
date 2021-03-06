---
title: ایجاد و راه‌اندازی نرم‌افزار خود
isChild: true
anchor: building_and_deploying_your_application
---

## ایجاد و راه‌اندازی نرم‌افزار خود {#building_and_deploying_your_application_title}

اگر تغییرات مربوط به پایگاه‌داده را دستی انجام می‌دهید یا آزمون‌های نوشته شده را به صورت دستی اجرا می‌کنید، بهتر است دوباره بیندیشید! با انجام هر کار به صورت دستی در هر نسخه‌ از نرم‌افزار خود احتمال بروز خطای مهلک افزایش می‌یابد. خواه تغییر کوچکی اعمال کنید یا با یک فرآیند ساخت پیچیده روبه‌رو باشید، [خودکارسازی فرآیند تولید](http://en.wikipedia.org/wiki/Build_automation) به کمک شما می‌آید.

از میان کارهایی که قصد خودکارسازی آن‌ها را دارید می‌توان به موارد زیر اشاره کرد:

* مدیریت وابستگی
* کامپایل کردن و کم حجم ساختن منابع مورد نیاز
* اجرای آزمون‌های مختلف
* ایجاد مستندات گوناگون
* بسته‌بندی و طبقه‌بندی نرم‌افزار
* راه‌اندازی نهایی

### ابزارهای خودکارسازی فرآیند تولید

این ابزارها معمولا از تعدادی اسکریپت تشکیل شده‌اند که فرآیند توسعه‌ی نرم‌افزار را آسان می‌کنند. ابزار تولید، بخشی از نرم‌افزار شما نیست، بلکه از بیرون آن را مدیریت می‌کند.

ابزارهای اُپِن سورس بسیاری در این رابطه وجود دارند، که برخی از آن‌ها نیز با PHP نوشته شده‌اند. این نباید منجر به استفاده نکردن از آن‌ها شود، اگر برای کار خاصی مورد نیاز باشند. چند نمونه عبارتند از:

[Phing](http://www.phing.info) متداول‌ترین ابزار مورد استفاده در خودکارسازی فرآیند تولید است که در دنیای PHP بسیار مورد استفاده قرار می‌گیرد. با استفاده از Phing شما می‌توانید کنترل بسته‌بندی، راه‌اندازی و اجرای آزمون‌ها را تنها از یک فایل XML مدیریت کنید. این ابزار (که مبتنی بر [Apache Ant](http://ant.apache.org/) است) فعالیت‌های بسیاری را جهت نصب و بروزرسانی نرم‌افزار تحت وب فراهم می‌آورد و امکان توسعه‌پذیری بالایی دارد، که می‌توان با استفاده از خود PHP اینکار را انجام داد.

[Capistrano](https://github.com/capistrano/capistrano/wiki) یک سیستم *متوسط-به-بالا برای برنامه‌نویسان* است که اجازه‌ی اجرای فرما‌ن‌های مختلف را به روشی ساخت‌یافته، روی یک یا چند ماشین می‌دهد. اگرچه به منظور توسعه‌ی برنامه‌های Ruby on Rails ایجاد شده است اما بسیاری **موفق شده‌اند PHP را روی آن توسعه دهند**. استفاده کاربردی از Capistrano مستلزم داشتن دانش کافی درباره‌ی Ruby on Rails است.

برای توسعه‌دهندگانی که قصد استفاده از Capistrano روی نرم‌افزار PHP خود را دارند، نوشته‌ی Dave Gardner با عنوان [توسعه‌ی PHP با Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/) نقطه‌ی آغاز مناسبی است.

[Chef](http://www.opscode.com/chef/) بیش از یک چارچوب راه‌اندازی کاربرد دارد، یک سیستم بسیار قدرتمند براساس Ruby است که نه تنها برای توسعه‌ی نرم‌افزار کاربرد دارد بلکه زیرساخت اولیه یک یا چند سرور را می‌تواند پیاده‌سازی کند.

منابع Chef برای توسعه‌دهندگان PHP:

* [مجموعه وبلاگ درباره‌ی پیاده‌سازی LAMP با استفاده از Chef](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [کتاب راهنمای Chef با تمرکز بر نصب PHP 5.3 و سیستم مدیریت بسته PEAR](https://github.com/opscode-cookbooks/php)

مطالعه‌ی بیشتر:

* [فرآیند خودکارسازی پروژه با استفاده از Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)
* [Maven](http://maven.apache.org/) ، چارچوب تولید مبتنی بر Ant و اینکه [چگونه با PHP استفاده شود](http://www.php-maven.org/)

### Continuous Integration

> یک فرآیند توسعه‌ی نرم‌افزار است که طی آن اعضای یک تیم کار روزانه‌ی خود را با سایر اعضا یکپارچه می‌سازند، که ممکن است این عمل چند  مرتبه در روز صورت گیرد. بسیاری از تیم‌ها به این نتیجه رسیده‌اند که این عمل منجر به یکپارچگی بیشتری در محصول نهایی خواهد شد و به تیم این اجازه را می‌دهد که در زمان کوتاه‌تری فرآیند توسعه را سپری کنند.

*-- Martin Fowler*

روش‌های مختلفی جهت پیاده‌سازی این فرآیند در PHP وجود دارد. اخیرا [Travis CI](https://travis-ci.org/) موفق شده است این تکنیک را در بسیاری از پروژه‌ها پیاده‌سازی کند، حتی پروژه‌های کوچک. Travis CI یک سرویس آنلاین است که در اختیار جامعه‌ی اِپِن سورس قرار دارد. این ابزار با GitHub یکپارچه شده است و پشتیبانی خوبی از زبان‌های برنامه‌نویسی موجود، از جمله PHP دارد.

مطالعه‌ی بیشتر:

* [یکپارچگی مداوم با Jenkins](http://jenkins-ci.org/)
* [یکپارچگی مداوم با PHPCI](http://www.phptesting.org/)
* [یکپارچگی مداوم با Teamcity](http://www.jetbrains.com/teamcity/)
