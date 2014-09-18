---
title: مفهوم پایه
isChild: true
anchor: basic_concept
---

## مفهوم پایه {#basic_concept_title}

این مفهوم را می‌توان با یک نمونه ساده توضیح داد.

فرض کنید کلاس `Database` داریم که جهت استفاده از پایگاه‌داده به یک adapter نیاز دارد. adapter را در تابع سازنده نمونه‌سازی می‌کنیم. این کار عملیات آزمایش (test) را دشوار کرده و کلاس `Database` را به وجود adapter وابسته می‌سازد.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

این کد می‌تواند طوری نوشته شود که این میزان وابستگی را کاهش دهد.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

در اینجا برای کلاس `Database` یک وابستگی تعریف می‌کنیم، به جای آنکه در داخل تابع آن را فراخوانی کنیم. همچنین می‌توانستیم تابع جداگانه‌ای در نظر بگیریم که بر اساس ورودی‌های وابستگی مورد نظر (adapter) عمل کند، یا اگر عملگر `adapter$` به صورت `public` بود می‌توانستیم آن را مستقیم تنظیم کنیم.
