---
isChild: true
title: لایه‌های انتزاعی
anchor: databases_abstraction_layers
---

## لایه‌های انتزاعی {#databases_abstraction_layers_title}

بسیاری از فریم‌ورک‌ها لایه‌ی انتزاعی خود جهت برقراری ارتباط با پایگاه‌داده را به وجود می‌آورند که ممکن است بر اساس PDO باشد یا نه. این‌ها اغلب ویژگی‌هایی را که در یک پایگاه‌داده وجود ندارد پیاده‌سازی می‌کنند با قرار دادن پرس‌و‌جو شما در متدهای مختلف PHP، که اینکار امکان برقراری کامل حالت انتزاعی با پایگاه‌داده را فراهم می‌سازد و با عملیات ابتدایی PDO بسیار متفاوت است.
اینکار اندکی سربار به وجود می‌آورد اما اگر نرم‌افزار شما نیاز دارد با چندین پایگاه‌داده مختلف ارتباط داشته باشد، این سربار ارزشش را دارد.

برخی از این لایه‌های انتزاعی با استفاده از استانداردهای فضای‌نام‌گذاری [PSR-0][psr0] یا [PSR-4][psr4] ساخته شده‌اند و می‌توانند در بسیاری از نرم‌افزارها مورد استفاده قرار بگیرند:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]

[1]: http://www.php.net/manual/en/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/

[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
