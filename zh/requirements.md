# 服务器要求

这些是成功安装和正确运行 Craft 的要求。

## 检查您的服务器

在安装 Craft 之前，请务必检查您的服务器是否符合要求。查看下面的要求或使用 [Craft Server Check](https://github.com/craftcms/server-check) 脚本快速检查您是否符合要求。

_如果你不负责服务器，请将链接发送到您的服务器管理员。_

## 服务器要求

Craft 要求如下：

* PHP 7.0+
* MySQL 5.5+ (含 InnoDB) or PostgreSQL 9.5+
* A web server (Apache, Nginx, IIS)
* A minimum of 256MB of memory allocated to PHP
* A minimum of 200MB of free disk space

## Required PHP Extensions

Craft requires the following PHP extensions:

* [PCRE](http://php.net/manual/en/book.pcre.php)
* [PDO](http://php.net/manual/en/book.pdo.php)
* [PDO MySQL Driver](http://php.net/manual/en/ref.pdo-mysql.php) or [PDO PostgreSQL Driver](http://php.net/manual/en/ref.pdo-pgsql.php)
* [GD](http://php.net/manual/en/book.image.php) or [ImageMagick](http://php.net/manual/en/book.imagick.php). ImageMagick is preferred.
* [OpenSSL](http://php.net/manual/en/book.openssl.php)
* [Multibyte String](http://php.net/manual/en/book.mbstring.php)
* [JSON](https://php.net/manual/en/book.json.php)
* [cURL](http://us1.php.net/manual/en/book.curl.php)
* [Reflection](http://php.net/manual/en/class.reflectionextension.php)
* [SPL](http://php.net/manual/en/book.spl.php)
* [Zip](https://secure.php.net/manual/en/book.zip.php)

## Optional PHP Extensions

* [iconv](http://us1.php.net/manual/en/book.iconv.php) – Adds support for more character encodings than PHP’s built-in [mb_convert_encoding()](http://php.net/manual/en/function.mb-convert-encoding.php) function, which Craft will take advantage of when converting strings to UTF-8.
* [Intl](http://php.net/manual/en/book.intl.php) – Adds rich internationalization support.
* [DOM](http://php.net/manual/en/book.dom.php) - Required for parsing XML feeds as well as `yii\web\XmlResponseFormatter`.


## Required Database User Privileges

The database user you tell Craft to connect with must have the following privileges:

#### MySQL

* `SELECT`
* `INSERT`
* `DELETE`
* `UPDATE`
* `CREATE`
* `ALTER`
* `INDEX`
* `DROP`
* `REFERENCES`

#### PostgreSQL

* `SELECT`
* `INSERT`
* `DELETE`
* `UPDATE`
* `CREATE`
* `DELETE`
* `REFERENCES`
* `CONNECT`

## CP Browser Requirements

Craft’s Control Panel requires a modern browser:

### Windows and macOS

* Chrome 29 or later
* Firefox 28 or later
* Safari 9.0 or later
* Internet Explorer 11 or later
* Microsoft Edge

### Mobile

* iOS: Safari 9.1 or later
* Android: Chrome 4.4 or later

Note: Craft’s Control Panel browser requirements have nothing to do with your actual website. If you’re a glutton for punishment and want your website to look flawless on IE 6, that’s your choice.
