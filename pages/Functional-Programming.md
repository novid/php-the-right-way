---
layout: page
title: برنامه‌نویسی تابعی در PHP
---

# برنامه‌نویسی تابعی در PHP

PHP از توابعی پشتیبانی می‌کند که می‌توانند به متغیرها انتساب داده شوند. چه توسط کاربر تعریف شده باشند چه داخلی باشند، می‌توانند توسط یک متغیر فراخوانی شوند. توابع می‌توانند به عنوان یک آرگومان به سایر توابع فرستاده شوند (قابلیتی که به آن توابع مرتبه-بالا گفته می‌شود) و هر تابعی می‌تواند توابعی دیگری را به عنوان خروجی بازگرداند.

بازگشت (Recursion)، قابلیتی که به یک تابع اجازه می‌دهد خود را فراخوانی کند، توسط زبان پشتیبانی می‌شود اما بیشتر کد PHP روی تکرار (Iteration) تاکید دارد.

توابع بی‌نام جدید (که از Closure پشتیبانی می‌کنند) از PHP 5.3 به بعد (۲۰۰۹) وجود دارند.

نسخه‌ی 5.4 از PHP قابلیت اتصال Closure به قلمرو شی (Object's Scope) را اضافه کرده و همچنین پشتیبانی از فراخوانی‌هایی با توابع بی‌نام را بهبود بخشیده است.

یکی از کاربردهای اصلی این توابع در زمان پیاده‌سازی الگوی استراتژی است. تابع از پیش تعریف شده‌ی `array_filter` یک آرایه به عنوان ورودی (داده) و یک تابع (یک استراتژی یا فراخوان) می‌گیرد که روی هر یک از خانه‌های آرایه اعمال می‌شود.

{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// Creates a new anonymous function and assigns it to a variable
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// Built-in array_filter accepts both the data and the function
$output = array_filter($input, $filter_even);

// The function doesn't need to be assigned to a variable. This is valid too:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

یک closure تابعی بی‌نام است که می‌تواند به متغیرهای خارج از حوزه‌ی خود دسترسی داشته بدون اینکه نیاز به متغیر سراسری باشد. در تعریف، closure تابعی است با چند آرگومان بسته (ثابت) توسط محیطی که در آن تعریف شده است. closure در محیط‌هایی که محدودیت برای متغیرها وجود دارد، کاربردی است.

در مثال بعد، از closure برای ایجاد تابعی استفاده می‌کنیم که یک به عنوان یک فیلتر برای `array_filter` به کار خواهد رفت.

{% highlight php %}
<?php
/**
 * Creates an anonymous filter function accepting items > $min
 *
 * Returns a single filter out of a family of "greater than n" filters
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Use array_filter on a input with a selected filter function
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // items > 3
{% endhighlight %}

هر فیلتر (تابع) تنها مقادیری را قبول می‌کند که از یک مقدار حداقل بیشتر هستند. تنها فیلتری که توسط `criteria_greater_than` باز می‌گردد closure است با آرگومان `min$` که در محیط تعریف شده است (که به عنوان آرگومان به `criteria_greater_than` موقع فراخوانی ارسال شده است).

این نوع فراخوانی (early binding) به صورت پیشفرض برای وارد کردن متغیر `min$` در تابع ساخته شده، به کار می‌رود. کتابخانه‌ای را در نظر بگیرید () که در آن از closure برای دسترسی به متغیرهایی استفاده می‌شود که در زمان فراخوانی تابعی بی‌نام می‌توان از آن‌ها استفاده کرد.

* [درباره‌ی توابع بی‌نام بیشتر بخوانید][anonymous-functions]
* [جزیییات بیشتر درباره‌ی Closure RFC][closures-rfc]
* [درباره‌ی فراخوانی پویا توابع با استفاده از `call_user_func_array` بیشتر بخوانید][call-user-func-array]

[anonymous-functions]: http://www.php.net/manual/en/functions.anonymous.php
[call-user-func-array]: http://php.net/manual/en/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
