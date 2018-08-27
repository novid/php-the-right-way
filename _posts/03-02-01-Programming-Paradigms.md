---
title: الگوهای برنامه‌نویسی
isChild: true
anchor: programming_paradigms
---

## الگوهای برنامه‌نویسی {#programming_paradigms_title}

PHP زبانی انعطاف پذیر و پویا است که از تکنیک‌های برنامه‌نویسی مختلفی پشتیبانی می‌کند. طی سال‌ها تغییرات زیادی در آن ایجاد شده است که می‌توان به موارد زیر اشاره کرد:

* مدل شی‌گرا در نسخه‌ی 5.0 (سال ۲۰۰۴)
* توابع بی‌نام (anonymous function) و فضای‌نام (namespace) در نسخه‌ی 5.3 (سال ۲۰۰۹)
* ویژگی‌‌های خاص (traits) در نسخه‌ی 5.4 (سال ۲۰۱۲)


### برنامه‌نویسی شی‌گرا

ویژگ‌های بسیاری از مدل برنامه‌نویسی شی‌گرا در PHP پشتیبانی می‌شوند از جمله کلاس‌ها (Classes)، کلاس‌های انتزاعی (Abstract Classes)، رابط‌ها (Interfaces)، وراثت (Inheritance)، سازنده‌ها (Constructors)، کپی‌کردن (Cloning)، استثناها (Exceptions) و بسیاری دیگر.

* [درباره‌ی شی‌گرایی در PHP بیشتر بدانید][oop]
* [درباره‌ی Traits بیشتر بدانید][traits]

### برنامه‌نویسی تابعی

PHP از توابعی پشتیبانی می‌کند که می‌توانند به متغیرها انتساب داده شوند. چه توسط کاربر تعریف شده باشند چه داخلی باشند، می‌توانند توسط یک متغیر فراخوانی شوند. توابع می‌توانند به عنوان یک آرگومان به سایر توابع فرستاده شوند (قابلیتی که به آن توابع مرتبه-بالا گفته می‌شود) و هر تابعی می‌تواند توابعی دیگری را به عنوان خروجی بازگرداند.

بازگشت (Recursion)، قابلیتی که به یک تابع اجازه می‌دهد خود را فراخوانی کند، توسط زبان پشتیبانی می‌شود اما بیشتر کد PHP روی تکرار (Iteration) تاکید دارد.

توابع بی‌نام جدید (که از Closure پشتیبانی می‌کنند) از PHP 5.3 به بعد (۲۰۰۹) وجود دارند.

نسخه‌ی 5.4 از PHP قابلیت اتصال Closure به قلمرو شی (Object's Scope) را اضافه کرده و همچنین پشتیبانی از فراخوانی‌هایی با توابع بی‌نام را بهبود بخشیده است.

* ادامه‌ی مطالعه‌ی [برنامه‌نویسی تابعی در PHP](pages/Functional-Programming.html)
* [درباره‌ی توابع بی‌نام بیشتر بدانید][anonymous-functions]
* [درباره‌ی کلاس Closure بیشتر بدانید][closure-class]
* [اطلاعات بیشتر درباره‌ی Closure RFC][closures-rfc]
* [درباره‌ی فراخوانی‌ها بیشتر بدانید][callables]
* [درباره‌ی فراخوانی پویا توسط 'call_user_func_array' بیشتر بدانید][call-user-func-array]

### برنامه‌نویسی Meta

از طریق مکانیسم‌هایی مانند Reflection API و Magic Meghods است که PHP از این سبک برنامه‌نویسی پشتیبانی می‌کند. متدهای مختلفی مانند ()get__ و ()set__ و ()clone__ و ()toString__ و ()invoke__ وجود دارند که به توسعه‌دهندگان اجازه می‌دهند رفتار داخلی یک کلاس را تغییر دهند. توسعه‌دهندگان Ruby اغلب می‌گویند PHP از نبود 'method_missing' رنج می‌برد در حالی که این عملکرد توسط ()call__ و ()callStatic__ قابل دسترسی است.

* [درباره‌ی Magic Methods بیشتر بدانید][magic-methods]
* [درباره‌ی Reflection بیشتر بدانید][reflection]
* [درباره  بیشتر Overloading بدانید][overloading]


[oop]: https://secure.php.net/language.oop5
[traits]: https://secure.php.net/language.oop5.traits
[anonymous-functions]: https://secure.php.net/functions.anonymous
[closure-class]: https://secure.php.net/class.closure
[closures-rfc]: https://wiki.php.net/rfc/closures
[callables]: https://secure.php.net/language.types.callable
[call-user-func-array]: https://secure.php.net/function.call-user-func-array
[magic-methods]: https://secure.php.net/language.oop5.magic
[reflection]: https://secure.php.net/intro.reflection
[overloading]: https://secure.php.net/language.oop5.overloading
