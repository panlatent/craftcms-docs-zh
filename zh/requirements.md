# 服务器要求

这些是成功安装和正确运行 Craft 的要求。

## 检查您的服务器

在安装 Craft 之前，请务必检查您的服务器是否符合要求。查看下面的要求或使用 [Craft Server Check](https://github.com/craftcms/server-check) 脚本快速检查您是否符合要求。

_如果你不负责服务器，请将链接发送到您的服务器管理员。_

## 服务器要求

Craft 要求如下：

* PHP 7.0+
* MySQL 5.5+ (含 InnoDB) or PostgreSQL 9.5+
* 一个 Web 服务器 (Apache, Nginx, IIS)
* 分配给 PHP 的最小内存为 256MB
* 至少 200MB 的可用磁盘空间

## 必需的PHP扩展

Craft 需要以下PHP扩展：

* [PCRE](http://php.net/manual/en/book.pcre.php)
* [PDO](http://php.net/manual/en/book.pdo.php)
* [PDO MySQL 驱动程序](http://php.net/manual/en/ref.pdo-mysql.php) or [PDO PostgreSQL 驱动程序](http://php.net/manual/en/ref.pdo-pgsql.php)
* [GD](http://php.net/manual/en/book.image.php) or [ImageMagick](http://php.net/manual/en/book.imagick.php). ImageMagick是首选。
* [OpenSSL](http://php.net/manual/en/book.openssl.php)
* [Multibyte String](http://php.net/manual/en/book.mbstring.php)
* [JSON](https://php.net/manual/en/book.json.php)
* [cURL](http://us1.php.net/manual/en/book.curl.php)
* [Reflection](http://php.net/manual/en/class.reflectionextension.php)
* [SPL](http://php.net/manual/en/book.spl.php)
* [Zip](https://secure.php.net/manual/en/book.zip.php)

## 可选的PHP扩展

* [iconv](http://us1.php.net/manual/en/book.iconv.php) – 与PHP内置的 [mb_convert_encoding()](http://php.net/manual/en/function.mb-convert-encoding.php) 函数相比，它支持更多的字符编码，Craft 在将字符串转换为 UTF-8 时将使用该函数。
* [Intl](http://php.net/manual/en/book.intl.php) – 增加丰富的国际化支持。
* [DOM](http://php.net/manual/en/book.dom.php) - 解析 XML feed 以及 `yii\web\XmlResponseFormatter`.


## 所需的数据库用户权限

Craft 进行连接的数据库用户必须具有以下权限：

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

## CP（控制面板） 浏览器要求

Craft 的控制面板需要一个现代浏览器：

### Windows and macOS

* Chrome 29 或更高版本
* Firefox 28 或更高版本
* Safari 9.0 或更高版本
* Internet Explorer 11 或更高版本
* Microsoft Edge

### 移动端

* iOS: Safari 9.1 或更高版本
* Android: Chrome 4.4 或更高版本

注意：Craft 的控制面板的浏览器要求与您的实际网站无关。如果你是一个酷爱极端的人，并希望你的网站在 IE 6 上看起来完美无瑕，那是你自己的选择。
