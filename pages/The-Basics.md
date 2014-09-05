---
layout: page
title: مفاهیم مقدماتی
---

# مفاهیم مقدماتی

## عملگرهای مقایسه‌ای

معمولا از کاربرد صحیح این عملگرها در PHP چشم‌پوشی می‌شود و همین امر نتایج غیرمنتظره‌ای را به وجود می‌آورد. یکی از این مشکلات ریشه در مقایسه‌ی نوع عددی با منطقی دارد.

{% highlight php %}
<?php
$a = 5;   // 5 as an integer

var_dump($a == 5);       // compare value; return true
var_dump($a == '5');     // compare value (ignore type); return true
var_dump($a === 5);      // compare type/value (integer vs. integer); return true
var_dump($a === '5');    // compare type/value (integer vs. string); return false

/**
 * Strict comparisons
 */
if (strpos('testing', 'test')) {    // 'test' is found at position 0, which is interpreted as the boolean 'false'
    // code...
}

// vs

if (strpos('testing', 'test') !== false) {    // true, as strict comparison was made (0 !== false)
    // code...
}
{% endhighlight %}

* [عملگرهای مقایسه‌ای](http://php.net/manual/en/language.operators.comparison.php)
* [جدول عملگرهای مقایسه‌ای](http://php.net/manual/en/types.comparisons.php)

## عبارت‌های شرطی

### If

زمانی که از عبارت 'if/else' داخل تابع یا کلاس استفاده می‌شود، باور اشتباهی وجود دارد که حتما باید از 'else' در تمام موارد استفاده کنیم. اگر خروجی مقدار بازگشتی باشد در این صورت استفاده از 'else' ضرورتی ندارد چون که 'return' به تابع خاتمه می‌دهد.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// vs

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else is not necessary
}
{% endhighlight %}

* [عبارت شرطی If](http://php.net/manual/en/control-structures.if.php)

### Switch

عبارت‌های Switch جایگزین مناسبی برای 'if' و 'elseif' تودرتو هستند، اما باید به مواردی درباره‌ی آن‌ها توجه کرد:

- این عبارت‌ها تنها مقدار را مقایسه می‌کنند و نه نوع را (معادل با '==')
- این عبارت‌ها مورد به مورد به جستجو پرداخته تا نتیجه مورد نظر یافت شود در غیر اینصورت از مقدار پیش‌فرض استفاده می‌شود
- بدون 'break' این عبارت‌ها به اجرای تمام موردها پرداخته تا زمانی که به یک break یا return برسند
- داخل تابع، استفاده از 'return' نیاز به 'break' را کاهش داده چرا که به تابع خاتمه می‌دهد

{% highlight php %}
<?php
$answer = test(2);    // the code from both 'case 2' and 'case 3' will be implemented

function test($a)
{
    switch ($a) {
        case 1:
            // code...
            break;             // break is used to end the switch statement
        case 2:
            // code...         // with no break, comparison will continue to 'case 3'
        case 3:
            // code...
            return $result;    // within a function, 'return' will end the function
        default:
            // code...
            return $error;
    }
}
{% endhighlight %}

* [عبارت Switch](http://php.net/manual/en/control-structures.switch.php)
* [PHP switch](http://phpswitch.com/)

## فضای نام‌گذاری سراسری

هنگامی که از فضای نام‌گذاری استفاده می‌کنیم، شاید متوجه شده باشید که دسترسی به توابع داخلی توسط توابع هم‌نامی که شما می‌نویسید از بین می‌رود. برای حل این مشکل، قبل از نام تابع یک '\' قرار دهید چرا که اینکار منجر به فراخوانی تابع از فضای نام‌گذاری سراسری می‌کند.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Our function name is the same as an internal function.
                         // Execute the function from the global space by adding '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator is an internal class. Using its name without a backslash
                                         // will attempt to resolve it within your namespace.
}
{% endhighlight %}

* [فضای سراسری](http://php.net/manual/en/language.namespaces.global.php)
* [قوانین سراسری](http://php.net/manual/en/userlandnaming.rules.php)

## رشته‌ها

### چسباندن

- اگر خطی از کد شما بیش از طول طبیعی (۱۲۰ کاراکتر) ادامه دارد، آن خط را به قسمت‌های مساوی تبدیل کنید
- برای خوانایی کد بهتر است از عملگرهای الحاقی (مانند "string" . "string") به جای عملگرهای الحاقی - انتسابی (=.) استفاده کنید
- در زمان تعریف متغیر که مقدار طولانی دارد بهتر است از چند خط برای مقدار آن استفاده شود و خط‌ها به صورت دندانه‌دار باشند

{% highlight php %}
<?php
$a  = 'Multi-line example';    // concatenating assignment operator (.=)
$a .= "\n";
$a .= 'of what not to do';

// vs

$a = 'Multi-line example'      // concatenation operator (.)
    . "\n"                     // indenting new lines
    . 'of what to do';
{% endhighlight %}

* [عملگرهای رشته‌ای](http://php.net/manual/en/language.operators.string.php)

### گونه‌های رشته‌ای

این گونه‌ها از ویژگی‌های ثابت در جامعه‌ی PHP هستند، اما این قسمت به توضیح گونه‌های مختلف رشته‌ای و مزایای آن‌ها اشاره دارد.

#### اعلان تکی (')

این اعلان‌ها ساده‌ترین و سریع‌ترین روش تعریف رشته‌ها هستند. سرعت آن‌ها ریشه در PHP و نه بررسی رشته‌ها (چرا که متغیرها را بررسی نمی‌کنند) دارد. بهتر است در این موارد استفاده شوند:

- رشته‌هایی که نیاز به تجزیه و تحلیل ندارند
- نوشتن یا چاپ متغیر همانطور که هست

{% highlight php %}
<?php
echo 'This is my string, look at how pretty it is.';    // no need to parse a simple string

/**
 * Output:
 *
 * This is my string, look at how pretty it is.
 */
{% endhighlight %}

* [Single Quote](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.single)

#### اعلان دوتایی (")

این اعلان‌ها درباره‌ی کار با رشته‌ها بسیار مفید و کاربردی، اما با توجه به عملیات تجزیه و تحلیل که صورت می‌دهند کندتر هستند. بهتر است در این موارد استفاده شوند:

- رشته‌هایی که قصد 'Escape' کردن آن‌ها را داریم
- رشته‌هایی که شامل چندین متغیر در داخل خود هستند
- چسباندن رشته‌هایی که در چند خط پراکنده شده‌اند جهت خوانایی بیشتر

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // a single quotes example that uses multiple concatenating for
    . "\n"                                       // variables and escaped string
    . 'I love learning' . $code . '!';

// vs

echo "phptherightway is $adjective.\n I love learning $code!"  // Instead of multiple concatenating, double quotes
                                                               // enables us to use a parsable string
{% endhighlight %}

زمانی که با این اعلان‌ها کار می‌کنیم، ممکن است متغیرهایی وجود داشته باشند که داخل خود از کاراکترهای دیگری استفاده کرده باشند. این کار منجر به پنهان شدن متغیر می‌شود و PHP نمی‌تواند محتوای آن را به درستی نمایش دهد. برای حل این مشکل، می‌توان متغیر را داخل '{}' قرار داد.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice cannot be parsed

// vs

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice will be parsed

/**
 * Complex variables will also be parsed within curly brackets
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] will be parsed
{% endhighlight %}

* [Double Quotes](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.double)

#### نحو دستور Nowdoc

این ویژگی در نسخه‌ی 5.3 معرفی شده است و عملکردی مانند اعلان تکی (') دارد به جز اینکه می‌توان از آن در چند خط استفاده کرد بدون آنکه نیاز به چسباندن (الحاق) رشته‌ها باشد.

{% highlight php %}
<?php
$str = <<<'EOD'             // initialized by <<<
Example of string
spanning multiple lines
using nowdoc syntax.
$a does not parse.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using nowdoc syntax.
 * $a does not parse.
 */
{% endhighlight %}

* [Nowdoc Syntax](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.nowdoc)

#### نحو دستور Heredoc

این دستور عملکردی مانند اعلان دوتایی (") دارد به جز اینکه می‌توان از آن در چند خط استفاده کرد بدون آنکه نیاز به چسباندن (الحاق) رشته‌ها باشد.

{% highlight php %}
<?php
$a = 'Variables';

$str = <<<EOD               // initialized by <<<
Example of string
spanning multiple lines
using heredoc syntax.
$a are parsed.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Example of string
 * spanning multiple lines
 * using heredoc syntax.
 * Variables are parsed.
 */
{% endhighlight %}

* [Heredoc Syntax](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.heredoc)

## عملگرهای سه‌تایی

استفاده از این عملگرها به کوتاه شدن کد کمک می‌کند، اما معمولا از آن‌ها بیش از حد استفاده می‌شود. توصیه می‌شود از این عملگرها در یک خط و به صورت جداگانه استفاده شود.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';
{% endhighlight %}

در مقایسه، این نمونه کدی است که خوانا بودن را فدای تعداد خط می‌کند.

{% highlight php %}
<?php
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // excess nesting, sacrificing readability
{% endhighlight %}

به منظور بازگرداندن یک متغیر با استفاده از عملگرهای سه‌تایی از نحو صحیح آن استفاده کنید.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // this example will output an error

// vs

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // this example will return 'yay'

{% endhighlight %}

به یاد داشته باشید که برای بازگشت یک مقدار منطقی نیاز به استفاده از این عملگرها ندارید. برای نمونه می‌توان به مورد زیر اشاره کرد.

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? true : false; // Will return true or false if $a == 3

// vs

$a = 3;
return $a == 3; // Will return true or false if $a == 3

{% endhighlight %}

این مورد درباره‌ی سایر عملگرها نیز صادق است (=== و ==! و =! و == و ...)

#### استفاده از پرانتز به همراه عملگرهای سه‌تایی

زمانی که از عملگر سه‌تایی استفاده می‌کنیم، پرانتزها می‌توانند به خوانایی بیشتر کد کمک کنند. برای نمونه کدی که نیاز به پرانتز ندارد:

{% highlight php %}
<?php
$a = 3;
return ($a == 3) ? "yay" : "nope"; // return yay or nope if $a == 3

// vs

<?php
$a = 3;
return $a == 3 ? "yay" : "nope"; // return yay or nope if $a == 3
{% endhighlight %}

پرانتزگذاری باعث می‌شود بتوانیم قسمت‌های مختلف شرط را از یکدیگر جدا کنیم. مانند مثال زیر که زمانی مقدار صحیح برمی‌گرداند که هر دو عبارت (a$ == 3 && b$ == 4) و c$ == 5 صحیح باشند.

{% highlight php %}
<?php
return ($a == 3 && $b == 4) && $c == 5;
{% endhighlight %}

مثال دیگر کد زیر است که در صورتی صحیح بازمی‌گرداند که (a$ =! 3 AND b$ =! 4) یا (c$ == 5) صحیح باشد.

{% highlight php %}
<?php
return ($a != 3 && $b != 4) || $c == 5;
{% endhighlight %}

* [عملگرهای سه‌تایی](http://php.net/manual/en/language.operators.comparison.php)

## تعریف متغیرها

زمانی بود که برنامه‌نویسان برای خوانابودن کد خود متغیرهای بسیاری را تعریف می‌کردند. این کار در عمل باعث می‌شود حافظه‌ی بیشتری مصرف شود. برای نمونه کد زیر، فرض کنید یک رشته به صورت پیشفرض یک مگابایت حافظه می‌گیرد که اینکار با کپی کردن متغیر باعث می‌شود دو مگابایت حافظه مصرف شود.

{% highlight php %}
<?php
$about = 'A very long string of text';    // uses 2MB memory
echo $about;

// vs

echo 'A very long string of text';        // uses 1MB memory
{% endhighlight %}

* [نکاتی درباره‌ی بهبود سرعت](https://developers.google.com/speed/articles/optimizing-php)
