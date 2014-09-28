---
title: پایگاه‌داده
anchor: databases
---

# پایگاه داده {#databases_title}

بسیاری از مواقع کد شما از یک پایگاه‌داده استفاده می‌کند تا اطلاعات را ذخیره کند. شما با گزینه‌های مختلفی جهت تعامل با پایگاه‌داده رو‌به‌رو هستید. روش توصیه شده تا **نسخه PHP 5.1.0** استفاده از درایورهایی مانند [mysqli] و [pgsql] و [mssql] و ... بود.

استفاده از این درایورها بسیار مناسب است به شرط آنکه برنامه‌ی شما تنها با _یک_ پایگاه‌داده سروکار داشته باشد، اگر،‌برای نمونه، به طور همزمان از MySQL و MSSQL استفاده می‌کنید، یا نیاز به برقراری ارتباط با Oracle دارید، آنگاه قادر نخواهید بود از این درایورها استفاده کنید. اینجاست که باید برای هر درایور کد جداگانه‌ای بنویسید &mdash; که این کار بیهوده‌ای است.

## افزونه‌ی MySQL

افزونه‌ی [mysql] دیگر توسعه داده نمی‌شود و [پایان عمر آن در نسخه PHP 5.5.0 به طور رسمی اعلام شده است]، بدین معنی که در نسخه‌های بعدی حذف خواهد شد. اگر در برنامه‌ی خود از تابع‌هایی که با `*_mysql` شروع می‌شوند استفاده می‌کنید، مانند `()mysql_connect` و `()mysql_query`، این‌ها در نسخه‌های بعدی PHP قابل استفاده نخواهند بود. این بدان معنی است که باید آن‌ها را با گزینه‌های مناسب‌تری مانند [mysqli] یا [PDO] جایگزین کنید و بهتر است که این کار را اکنون انجام دهید تا بعدها مجبور نباشید این تغییرات را با عجله انجام دهید.

**اگر از ابتدا نرم‌افزاری را شروع کرده‌اید به طور حتم نباید از افزونه‌ی [mysql] استفاده کنید: در عوض از [افزونه‌ی MySQLi][mysqli] یا PDO استفاده کنید.**

* [PHP: انتخاب API مناسب برای MySQL](http://php.net/manual/en/mysqlinfo.api.choosing.php)
* [آموزش PDO برای توسعه‌دهندگان MySQL](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)


## افزونه‌ی PDO

PDO یک کتابخانه‌ی انتزاعی جهت برقراری ارتباط با پایگاه‌داده‌های مختلف است &mdash; که از نسخه‌ی PHP 5.1.0 قابل دسترس است. برای نمونه، شما می‌توانید از کد یکسانی جهت برقراری ارتباط با MySQL یا SQLite استفاده کنید:

{% highlight php %}
// PDO + MySQL
$pdo = new PDO('mysql:host=example.com;dbname=database', 'user', 'password');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);

// PDO + SQLite
$pdo = new PDO('sqlite:/path/db/foo.sqlite');
$statement = $pdo->query("SELECT some\_field FROM some\_table");
$row = $statement->fetch(PDO::FETCH_ASSOC);
echo htmlentities($row['some_field']);
{% endhighlight %}

PDO پرس‌وجوهای SQL را ترجمه نمی‌کند یا ویژگی‌های خاص هر پایگاه‌داده را شبیه‌سازی نمی‌کند; تنها برای اتصال به چند پایگاه‌داده از طریق یک API طراحی شده است.

از همه مهم‌تر، `PDO` این امکان را می‌دهد تا داده‌های ورودی به نرم‌افزار را با روش‌های امن وارد پایگاه‌داده کنید که اینکار منجر به جلوگیری از حملات SQL Injection می‌گردد.

فرض کنید اسکریپت PHP یک ID از نوع عددی را به عنوان پارامتر می‌پذیرد. از این ID جهت فراخوانی کاربر از پایگاه‌داده استفاده می‌شود. قطعه کد پایین روش `اشتباه` پیاده‌سازی اینکار است:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

اینطور کدنویسی وحشتناک است. شما پارامتری را به طور مستقیم وارد پایگاه‌داده می‌کنید بدون آنکه آن را بررسی کنید. اینکار باعث می‌شود در کسری از ثانیه، مورد حمله قرار بگیرید با استفاده از روشی به نام [SQL Injection](http://wiki.hashphp.org/Validation). فقط تصور کنید فرد مهاجم عبارتی مانند `http://domain.com/?id=1%3BDELETE+FROM+users` را فراخوانی کند. اینکار متغیر ‍‍`GET_$` را با مقدار `1;DELETE FROM users` تنظیم می‌کند که باعث می‌شود اطلاعات تمام کاربران شما از بین برود! شما باید با استفاده از انقیاد پارامتر در PDO داده‌ی ورودی را بررسی کنید.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:/path/db/users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Automatically sanitized by PDO
$stmt->execute();
{% endhighlight %}

این کد صحیح است، چرا که با استفاده از انقیاد پارامتر روی عبارت PDO کار می‌کند. اینکار باعث می‌شود داده‌ی ورودی قبل از اینکه وارد پایگاه‌داده شود بررسی شده و احتمال خطر SQL Injection را از بین می‌برد.

* [درباره‌ی PDO بیشتر بدانید]

باید آگاه باشید که برقراری ارتباط با پایگاه‌داده از منابع سیستم استفاده می‌کند و اگر این ارتباط پایان نیابد، این منابع به صورت خودکار آزاد نمی‌شوند. با استفاده از PDO این اطمینان را دارید که زمان خاتمه‌ی ارتباط، شی مربوط به پایگاه‌داده از بین می‌رود و تمام منابع آن باز می‌گردد. اگر اینکار را به صورت واضح انجام ندهید، PHP به صورت خودکار هنگام خاتمه‌ی اسکریپت ارتباط پایگاه‌داده را قطع می‌کند مگر اینکه ار یک ارتباط پایدار استفاه کرده باشید.

* [درباره‌ی برقراری ارتباط با استفاده از PDO بیشتر بدانید]

[درباره‌ی PDO بیشتر بدانید]: http://www.php.net/manual/en/book.pdo.php
[درباره‌ی برقراری ارتباط با استفاده از PDO بیشتر بدانید]: http://php.net/manual/en/pdo.connections.php
[پایان عمر آن در نسخه PHP 5.5.0 به طور رسمی اعلام شده است]: http://php.net/manual/en/migration55.deprecated.php
[SQL Injection]: http://wiki.hashphp.org/Validation

[pdo]: http://php.net/pdo
[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[mssql]: http://php.net/mssql
