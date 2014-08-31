---
title: راهنمای سبک کدنویسی
anchor: code_style_guide
---

# راهنمای سَبک کدنویسی  {#code_style_guide_title}

جامعه‌ی PHP بزرگ و پراکنده است که از کتابخانه‌ها، فریم‌ورک‌ها و اجزای گوناگونی تشکیل شده است. برای توسعه‌دهندگان PHP امری طبیعی است که بخشی از این ابزار را در پروژه‌های خود به کار ببرند. از این رو، بسیار مهم است که کد PHP از یک سبک استاندارد (تا آنجا که امکان دارد) طبعیت کند تا توسعه‌دهندگان بتوانند به سادگی از کتابخانه‌های مختلف در پروژه‌ی خود استفاده کنند.

[گروه تعاملی فریم‌ورک PHP][fig] مجموعه‌ای از سبک‌ها را تهیه و آماده کرده است. تمام آن‌ها مربوط به کدنویسی نمی‌شوند، اما آن‌هایی که هستند عبارتند از:

* [PSR-0][psr0]
* [PSR-1][psr1]
* [PSR-2][psr2]
* [PSR-4][psr4]
این توصیه‌ها تقریبا مجموعه‌ای از قوانین هستند که پروژه‌هایی نظیر Drupal، Zend، Symfony، CakePHP و بسیاری دیگر از آن‌ها استفاده می‌کنند. شما می‌توانید از آن‌ها در پروژه‌های خود استفاده کنید، یا همان سبک کدنویسی خود را ادامه دهید.

در حقیقت باید طوری کد بنویسید که از یک استاندارد شناخته‌شده طبعیت کند. این استاندارد می‌تواند هر ترکیبی از PSRها یا یکی از استانداردهای ایجاد شده توسط PEAR یا Zend باشد. این بدان معنی است که سایر توسعه‌دهندگان به سادگی بتوانند با کد شما ارتباط برقرار کنند، و نرم‌افزارهایی که از اجزای جداگانه تشکیل شده‌اند با یکدیگر سازگاری داشته باشند.

* [درباره PSR-0 بیشتر بدانید][psr0]
* [درباره PSR-1 بیشتر بدانید][psr1]
* [درباره PSR-2 بیشتر بدانید][psr2]
* [درباره PSR-4 بیشتر بدانید][psr4]
* [استانداردهای کدنویسی PEAR][pear-cs]
* [استانداردهای کدنویسی Zend][zend-cs]
* [استانداردهای کدنویسی Symfony][symfony-cs]

شما می‌توانید از ابزاری مانند [PHP CodeSniffer][phpcs] برای بررسی هر یک از این استانداردها، یا از افزونه‌هایی برای ویرایشگرهای متن مانند [Sublime Text 2][st-cs] استفاده کنید.

همچنین ابزار [PHP Coding Standards Fixer][phpcsfixer] که توسط Fabien Potencier توسعه داده شده، به صورت خودکار کد شما را نسبت به این استانداردها بررسی می‌کند و تغییرات لازم را انجام می‌دهد، لازم هم نیست شما این کار را به صورت دستی انجام دهید.

انگلیسی زبان اصلی برای تمام نمادها و ساختار کد است. کامنت‌ها می‌توانند به هر زبانی که برنامه‌نویسان در پروژه با آن آشنا هستند، نوشته شوند.

[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
