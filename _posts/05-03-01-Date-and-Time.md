---
title: تاریخ و زمان
isChild: true
anchor: date_and_time
---

## تاریخ و زمان {#date_and_time_title}

برای خواندن، نوشتن و مقایسه‌ی تاریخ و زمان، از کلاس DateTime در PHP استفاده می‌شود. توابع مختلفی در رابطه با تاریخ و زمان وجود دارند اما ساختار شی‌گرا این کلاس به بیشتر نیازهای ما پاسخ می‌دهد. همچنین توانایی مدیریت منطقه‌های زمانی/جغرافیایی را نیز دارد که خارج از این مقدمه کوتاه است.

برای شروع، تنها کافی است تاریخ و زمان خام را به یک شی با استفاده از متد `()createFromFormat` تبدیل کرده یا جهت دریافت تاریخ و زمان فعلی از `new \DateTime` استفاده کنیم. با استفاده از متد `()format` می‌توان شی DateTime را به یک رشته‌ی قابل نمایش تبدیل کرد.
{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
{% endhighlight %}

محاسبات روی DateTime با استفاده از کلاس DateInterval قابل انجام است. کلاس DateTime متدهایی مانند `()add` و `()sub` دارد که از DateInterval به عنوان آرگومان استفاده می‌کنند. کدی ننویسید که به ازای هر روز تعداد ثانیه‌های ثابتی را درخواست کند چرا که تغییر در منطقه‌های زمانی/جغرافیایی این فرض را باطل می‌کند. در عوض، از بازه‌های زمانی استفاده کرده و برای محاسبه‌ی اختلاف زمانی از متد `()diff` استفاده کنید که مقدار بازگشتی آن DateInterval است و به راحتی می‌توان آن را نمایش داد.
{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new \DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

On DateTime objects you can use standard comparison:
{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before end!\n";
}
{% endhighlight %}

جهت پیمایش بین رخدادهای تکراری از کلاس DatePeriod استفاده کنید که دو شی DateTime را دریافت کرده (start و end) و با استفاده از بازه‌ی زمانی، تمام رخدادهای بین آن‌ها را محاسبه می‌کند. 
{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = \DateInterval::createFromDateString('first thursday');
$periodIterator = new \DatePeriod($start, $periodInterval, $end, \DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('m/d/Y') . ' ';
}
{% endhighlight %}

* [درباره‌ی DateTime بخوانید][datetime]
* [درباره‌ی نحوه‌ی نمایش تاریخ و زمان بخوانید][dateformat]

[datetime]: http://www.php.net/manual/book.datetime.php
[dateformat]: http://www.php.net/manual/function.date.php
