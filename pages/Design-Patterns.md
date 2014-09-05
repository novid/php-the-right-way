---
layout: page
title: الگوهای طراحی
---

# الگوهای طراحی

راه‌های متفاوتی برای ساختار دادن به کد و پروژه وب شما وجود دارند، و شما می‌توانید هر طور که می‌خواهید ساختار پروژه را در نظر بگیرید. اما اگر از الگوهای مناسبی برای کد و ساختار پروژه استفاده کنید هم مدیریت آن آسان می‌شود هم دیگران ارتباط بهتری با پروژه برقرار می‌کنند.

* [الگوی معماری در ویکیپدیا](https://en.wikipedia.org/wiki/Architectural_pattern)
* [الگوی طراحی نرم‌افزار در ویکیپدیا](https://en.wikipedia.org/wiki/Software_design_pattern)

## Factory

یکی از پرکاربردترین الگوهای طراحی، factory نام دارد. در این الگو، خود کلاس شی مورد نظر شما را می‌سازد. مثال زیر را به عنوان یک الگوی factory در نظر بگیرید:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// have the factory create the Automobile object
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // outputs "Bugatti Veyron"
{% endhighlight %}

این کد از الگوی factory استفاده می‌کند تا یک شی از نوع اتومبیل بسازد. دو مزیت اصلی در این روش کدنویسی وجود دارد; اول اینکه اگر بخواهید کلاس اتومبیل را تغییر، نام‌گذاری مجدد یا جایگزین کنید تنها کافی است کد داخل factory را تغییر دهید، نه هر جا که از کلاس اتومبیل استفاده شده است. مزیت احتمالی دوم این است که اگر ساختن شی فرآیند پیچیده‌ای باشد شما می‌توانید تمام کار را در داخل factory انجام دهید، نه هر بار که خواستید یک نمونه شی جدید بسازید.

استفاده از الگوی factory همیشه لازم (یا عاقلانه) نیست. مثال مطرح شده اینقدر ساده است که نیاز به این الگو ندارد اما اگر شما در حال ساخت پروژه‌ی بزرگی هستید به دردتان می‌خورد.

* [الگوی Factory در ویکیپدیا](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

هنگام طراحی نرم‌افزارهای تحت وب، از لحاظ معماری و مفهومی بسیار معقول به نظر می‌رسد تا تنها به یک و فقط یک شی از کلاس خاصی دسترسی وجود داشته باشد. الگوی singleton به ما در این حالت کمک می‌کند.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Returns the *Singleton* instance of this class.
     *
     * @staticvar Singleton $instance The *Singleton* instances of this class.
     *
     * @return Singleton The *Singleton* instance.
     */
    public static function getInstance()
    {
        static $instance = null;
        if (null === $instance) {
            $instance = new static();
        }

        return $instance;
    }

    /**
     * Protected constructor to prevent creating a new instance of the
     * *Singleton* via the `new` operator from outside of this class.
     */
    protected function __construct()
    {
    }

    /**
     * Private clone method to prevent cloning of the instance of the
     * *Singleton* instance.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Private unserialize method to prevent unserializing of the *Singleton*
     * instance.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

کد بالا الگوی singleton را با استفاده از یک [متغیر *ایستا*](http://php.net/language.variables.scope#language.variables.scope.static) و متد ایستا با نام `()getInstance` پیاده‌سازی می‌کند.
به این موارد توجه کنید:

* سازنده [`construct__`](http://php.net/language.oop5.decon#object.construct) به صورت protected تعریف شده است تا از ایجاد یک شی جدید خارج از کلاس با استفاده از عملگر `new` جلوگیری کند.
* متد [`clone__`](http://php.net/language.oop5.cloning#object.clone) به صورت private تعریف شده است تا از کپی شدن شی با استفاده از عملگر [`clone`](http://php.net/language.oop5.cloning) جلوگیری کند.
* متد [`wakeup__`](http://php.net/language.oop5.magic#object.wakeup) به صورت private تعریف شده است تا از unserialize شدن یک نمونه یا شی از کلاس با استفاده از تابع سراسری [`()unserialize`](http://php.net/function.unserialize) جلوگیری کند.
* یک شی جدید با استفاده از [late static binding](http://php.net/language.oop5.late-static-bindings) در متد ایستا `()getInstance` با عملگر `static` ساخته شده است. این کار اجازه می‌دهد کلاس‌های دیگری از کلاس `Singleton` قابلیت ساخته‌شدن داشته باشند.

الگوی singleton زمانی بسیار مفید است که می‌خواهیم اطمینان یابیم تنها یک شی از کلاس مورد نظر در طول چرخه‌ی حیات نرم‌افزار وجود دارد. این زمانی اتفاق می‌افتد که شی سراسری (مانند یک کلاس جهت پیکربندی پروژه) یا منبعی اشتراکی (مانند یک صف رخداد) وجود داشته باشد.

در استفاده از این الگو باید احتیاط کنید چون حالتی با دسترسی سراسری در نرم‌افزار را به وجود می‌آورد، که منجر به کاهش قابلیت آزمایش روی کد می‌شود. در اکثر موارد، تزریق وابستگی (Dependency Injection) می‌تواند (و باید) به جای این الگو استفاده شود. استفاده از آن باعث می‌شود کد اضافه در نرم‌افزار ما بی‌دلیل به وجود نیاید زمانی که یک شی از یک منبع سراسری یا اشتراکی می‌خواهد استفاده کند.

* [الگوی Singleton در ویکیپدیا]

## Strategy

با استفاده از الگوی strategy شما نحوه‌ی پیاده‌سازی برخی از الگوریتم‌ها را در کلاس اصلی پنهان می‌سازید و اجازه نمی‌دهید کلاس‌های مشتق شده چگونه پیاده‌سازی شدن این الگوریتم‌ها را بدانند.
روش‌های پیاده‌سازی متفاوتی از این الگو وجود دارند که در ادامه به ساده‌ترین آن‌ها می‌پردازیم:

اولین قطعه کد خانواده‌ای از الگوریتم‌ها را نشان می‌دهد که با استفاده از آن‌ها می‌توان آرایه‌ای مرتب شده از داده‌ها (مانند ساختار JSON) را ایجاد کرد:

{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

با استفاده از این روش شما روشی زیبا و تمیز در کد خود به وجود می‌آورید که به سایر توسعه‌دهندگان اجازه می‌دهد از آن استفاده کنند و نوع خروجی خود را بر اساس نیازشان بسازند بدون آنکه به کد اصلی لطمه‌ای وارد شود.

خواهید دید که هر کلاس 'output' چگونه OutputInterface را پیاده‌سازی می‌کند که دو هدف را دنبال می‌کند، اول آنکه قواعد ساده‌ای را به وجود می‌آورد که هر کلاس فرزند باید از آن تبعیت کند. دوم آنکه با پیاده‌سازی یک رابط همگانی که با استفاده از [Type Hinting](http://php.net/manual/en/language.oop5.typehinting.php) به وجود می‌آید اطمینان حاصل می‌کند هر کلاس فرزند که این ویژگی‌ها را پیاده‌سازی خواهد کرد، از نوع صحیحی خواهد بود که در این مورد 'OutputInterface' خواهد بود.

قطعه کد بعد مشخص می‌کند چگونه کلاسی که الگوریتم‌های اصلی را پیاده‌سازی می‌کند می‌تواند عملکرد آن را در  زمان اجرا تغییر دهد:

{% highlight php %}
<?php

class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

کلاس بالا یک فیلد خصوصی دارد که در زمان اجرا باید از نوع 'OutputInterface' باشد تا با فراخوانی ()loadOutput متد ()load داخل آن صدا زده می‌شود.

{% highlight php %}
<?php

$client = new SomeClient();

// Want an array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Want some JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [الگوی Strategy در ویکیپدیا](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

زمانی که تنها یک نقطه ورود به نرم‌افزار تحت وب وجود داشته باشد و تمام درخواست‌ها از آنجا مدیریت شود، از این الگو استفاده شده است. این قطعه کد مسیول بارگذاری تمام پیشنیازها، پردازش تمام درخواست‌ها و ارسال پاسخ به مرورگر است. این الگو می‌تواند بسیار مفید باشد چرا که استفاده از ساختار ماژولار در کد را ممکن می‌سازد و به شما محیطی مرکزی برای مدیریت تمام درخواست‌ها به وجود می‌آورد (مانند بررسی صحت داده‌ی ورودی).

* [الگوی Front Controller در ویکیپدیا](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

الگوی MVC و خانواده‌های آن مانند HMVC و MVVM به شما اجازه می‌دهند کدتان را به قسمت‌های منطقی کوچکتری تقسیم کنید که هر کدام وظیفه‌ی خاصی انجام می‌دهند. Model به عنوان یک لایه‌ی دسترسی به داده عمل می‌کند که در آن داده طبق قالب‌های قابل استفاده در نرم‌افزار شما به آن فرستاده یا از آن بازمی‌گردد. Controller درخواست‌ها را مدیریت می‌کند، داده‌ی بازگشتی از Model را پردازش کرده و جهت ارسال پاسخ View را فراخوانی می‌کند. View همان قالب نهایی است که قرار است به عنوان پاسخ به مرورگر فرستاده شود (مانند html, xml و ...).

MVC عمومی‌ترین مدل معماری نرم‌افزار در محبوب‌ترین [فریم‌ورک‌های PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks) است.

درباره‌ی MVC و هم خانواده‌های آن بیشتر بدانید:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
