---
isChild: true
title: ارتباط با پایگاه‌داده
anchor: databases_interacting
---

## ارتباط با پایگاه‌داده {#databases_interacting_title}

زمانی که توسعه‌دهندگان شروع به یادگیری PHP می‌کنند، اغلب کد مربوط به بخش پایگاه‌داده را با کد مربوط به بخش نرم‌افزار خود مخلوط می‌کنند، مانند:

{% highlight php %}
<ul>
<?php
foreach ($db->query('SELECT * FROM table') as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>";
}
</ul>
{% endhighlight %}

این روش اشتباهی است بنا به دلایل مختلف، بیشتر به خاطر دشوار بودن عیب‌یابی، آزمایش و خواندن آن، که باعث می‌شود داده‌ی بسیاری به خروجی برود اگر برای آن حد خاصی مشخص نشده باشد.

با توجه به روش‌های دیگری که برای این مساله وجود دارد - مانند [برنامه‌نویسی شی‌گرا](/#object-oriented-programming) یا [برنامه‌نویسی تابعی](/#functional-programming) - بایستی این فرآیند به صورت جداگانه انجام شود.

ساده‌ترین روش را در نظر بگیرید:

{% highlight php %}
<?php
function getAllSomethings($db) {
    return $db->query('SELECT * FROM table');
}

foreach (getAllFoos() as $row) {
    echo "<li>".$row['field1']." - ".$row['field1']."</li>"; // BAD!!
}
{% endhighlight %}

این شروع خوبی است. آن دو مورد را داخل فایل‌های جداگانه قرار دهید تا جدایی بخش‌ها ملموس شود.

با ایجاد یک کلاس که متد شما را در بر می‌گیرد می‌توانید یک "Model" به وجود آورید. یک فایل ساده با پسوند `php.` جهت قراردادن خروجی خود به وجود آورید تا در اینجا به یک "View" برسید، که تقریبا نزدیک به [MVC] - یک معماری شی‌گرا برای اکثر [فریم‌ورک‌ها](/#frameworks_title) است.

**foo.php**

{% highlight php %}
<?php

$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8', 'username', 'password');

// Make your model available
include 'models/FooModel.php';

// Create an instance
$fooList = new FooModel($db);

// Show the view
include 'views/foo-list.php';
{% endhighlight %}


**models/FooModel.php**

{% highlight php %}
<?php
class Foo()
{
    protected $db;

    public function __construct(PDO $db)
    {
        $this->db = $db;
    }

    public function getAllFoos() {
        return $this->db->query('SELECT * FROM table');
    }
}
{% endhighlight %}

**views/foo-list.php**

{% highlight php %}
<? foreach ($fooList as $row): ?>
    <?= $row['field1'] ?> - <?= $row['field1'] ?>
<? endforeach ?>
{% endhighlight %}

این تقریبا مشابه کاری است که تمام فریم‌ورک‌ها انجام می‌دهند البته با کمی تفاوت. شما نیاز ندارید که این گام‌ها را مجدد تکرار کنید، اما زمانی که قصد [آزمایش کردن واحدی](/#unit-testing) از نرم‌افزار خود را دارید، قاطی کردن کدهای مختلف با یکدیگر برای شما مشکل‌ساز خواهد شد.

[PHPBridge] مقاله‌ی فوق‌العاده‌ای دارد با مضمون [ایجاد یک کلاس داده‌ای] که موضوعی بسیار مشابه به این را پوشش می‌دهد و برای توسعه‌دهندگانی که به تازگی می‌خواهند با پایگاه‌داده کار کنند، بسیار مناسب است.

[MVC]: http://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488
[PHPBridge]: http://phpbridge.org/
[Creating a Data Class]: http://phpbridge.org/intro-to-php/creating_a_data_class
