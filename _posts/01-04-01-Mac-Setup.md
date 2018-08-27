---
title: نصب در مکینتاش
isChild: true
anchor: mac_setup
---

## نصب در مکینتاش  {#mac_setup_title}

سیستم عامل OSX به صورت پیش فرض PHP را نصب دارد اما از نسخه‌های قدیمی‌تر آن استفاده می‌کند. راه‌های مختلفی برای نصب آخرین نسخه PHP  در macOS وجود دارد.

### نصب PHP با Homebrew

 مدیر بسته [Homebrew]  در macOS کمک میکند تا به راحتی PHP و اکستنشن‌های مختلف PHP  را نصب کنیم. ریپازیتوری اصلی Homebrew برای نصب نسخه های PHP 5.6, 7.0, 7.1, and 7.2 از قاعده نام آنها برای نصب استفاده میکند. برای نصب آخرین نسخه از دستور زیر استفاده میکنیم : 
```
brew install php@7.2
```

می توانید بین نسخه های مختلف PHP سویج کنید با ویرایش کردن متغییر `PATH` . همچنین، می توایند از  [brew-php-switcher][brew-php-switcher] برای سویچ کردن بین نسخه های مختلف PHP  به صورت خودکار استفاده کنید.

### نصب PHP با Macports

پروژه [MacPorts]، پروژه ای اوپن سورس برای نصب آسان سیستم ها برای کامپایل، نصب و آپگرید کردن هم به صورت کامند لاین، X11 و یا نرم افزار هایی اپن سورس Aqua based  در سیستم عامل OS X استفاده می شود.

ابزار MacPorts از باینری های از قبل کامپایل شده (pre-compiled binaries) پشتیبانی میکند، بنابر این لازم نیست دوباره هر  وابستگی را برای منابع با فایل های tarball (نوعی فرمت فایل فشرده) کامپایل کنید، این زندگی شما نجات میدهد اگر هیچ بسته ای پیش از این روی سیستم شما نصب نشده باشد.
 
برای نصب نسخه های مختلف  `php54`, `php55`, `php56`, `php70` یا `php71` از دستور  `port install` استفاده کیند برای مثال : 

    sudo port install php56
    sudo port install php71

و می توانید با اجرا کردن دستور  `select` بین نسخه‌های مختلف PHP سویچ کنید :‌

 sudo port select --set php php71

### نصب PHP با  Liip's binary installer

گزینه محبوب دیگر [php-osx.liip.ch] است که با یک خط دستور نصب می توان نسخه های 5.3 تا 7.1 را نصب کرد.
این ابزار روی باینری‌های PHP نصب شده توسط اپل باز نویسی نمی‌کند، اما همه چیز را در مکان جدایی نصب میکند (/usr/local/php5).

### کامپایل کردن از منبع

شما همچنین می‌توانید خودتان آن را [کامپایل][mac-compile] کنید; در این صورت، اطمینان حاصل کنید که قبل از آن Xcode یا [جایگزین Apple][apple-developer] برای آن را نصب کرده باشید، که از وبسایت رسمی Apple قابل دریافت است.

### نصب کننده‌های All-in-One

روش های نصب ذکر شده در بالا همگی در مورد نصب PHP به تنهایی بود، و چیز‌های دیگر مانند وب سرور آپاچی Apache ، انجین‌ایکس Nginx و پایگاه داده SQL server را نصب نمی کنند.
بسته‌های آماده‌ای مانند [MAMP][mamp-downloads] یا [XAMPP][xampp] هستند که نرم افزارهای دیگر  مورد نیاز را با هم نصب میکنند، اما اگر چه این روش نصب آسان است اما انعطاف پذیری را از شما میگیرد.( روش نصب آسان در مقابل انتعطاف پذیری).

[Homebrew]: https://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://php-osx.liip.ch/
[mac-compile]: https://secure.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/index.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
