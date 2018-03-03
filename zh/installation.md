# 安装说明

- [0. 引言](#0-introduction)
- [1. 安装 Composer](#1-install-composer)
- [2. 创建一个新的 Craft 项目](#2-create-a-new-craft-project)
- [3. 设置数据库](#3-set-up-the-database)
- [4. 设置 Web 服务器](#4-set-up-the-web-server)

## 0. 引言

Craft 3 是一个 [Composer] 包. 如果您不熟悉 Composer, 那么它是一个包管理器（如 npm），它试图通过终端命令轻松的安装和更新 PHP 库。

> {note} 另一种放弃 Composer 的安装方法正在开发中，在 Craft 3.0 GA 发布时应该准备好了。尽管这样，开始熟悉 Composer 仍然是一个好主意！

Craft 的 Composer 支持有两个部分：

1. **[`craftcms/cms`]** – 这是包含 Craft 所有源代码的 Composer 软件包。
2. **[`craftcms/craft`]** –  这是一个 Composer “项目”，可以作为新的 Craft 项目的起点。

## 1. 安装 Composer

您应该运行 Composer 1.3.0 或更高版本。您可以通过运行以下命令打开您的终端来找到您安装的 Composer 版本（如果有的话）：

    composer -V

如果输出错误，说 composer 没有找到或未被识别，则 Composer 未安装。按照 Composer 的说明进行安装：

  - [macOS/Linux/Unix 说明] *（全局安装）*
  - [Windows 说明]

如果输出的版本号小于 `1.3.0`，则运行以下命令进行更新：

    composer self-update

## 2. 创建一个新的 Craft 项目

要创建一个新的 Craft 项目，请运行以下命令（`PATH` 用 Composer 创建项目的路径代替）：

    composer create-project -s RC craftcms/craft PATH

注意：如果 Composer 报告说你的系统没有安装 PHP 7，但你知道这不是问题，比如 Craft 使用不同的 PHP（例如通过 MAMP 或 Vagrant）运行，请使用该 `--ignore-platform-reqs` 选项。

Composer 将花几分钟安装一切。

一旦完成，你的项目目录应该有这样的文件结构：

```
config/...
storage/
templates/
vendor/...
web/...
.env
.env.example
composer.json
craft
craft.bat
LICENSE.md
README.md
```

有关这些目录和文件的信息，请参阅 [目录结构](directory-structure.md)。

## 3. 建立数据库

接下来，您需要为您的Craft项目创建一个数据库。Craft 3 支持 MySQL 5.5+ 和 PostgreSQL 9.5+ 。

如果您已经选择，我们建议在大多数情况下使用以下数据库设置：

- **MySQL**
  - 默认字符集: `utf8`
  - 默认排序规则: `utf8_unicode_ci`

- **PostgreSQL**
  - 字符集: `UTF8`

创建数据库后，您需要配置文你的 `.env` 文件作为数据库连接设置。您可以手动编辑文件，也可以在终端的根目录下运行 `./craft setup` 命令。

注： 在 `craftcms/craft` 项目带有预安装的 [PHP dotenv](https://github.com/vlucas/phpdotenv) 来处理 `.env` 文件。使用 PHP dotenv 的优势在于它提供了一个可以将敏感信息（如数据库连接设置）存储在 Git 仓库之外的方式。

## 4. 设置 Web 服务器

创建一个新的 Web 服务器来托管您的 Craft 项目。它的文档根目录应指向您的公共 HTML 文件夹。如果您使用的是 Craft 的 Composer【开始项目](https://github.com/craftcms/craft)，那么默认情况下它的目录是 `web/` ，但只要您的 Web 服务器配置为指向该目录，就可以将其重命名为任何您想要的内容。

如果您的虚拟主机已经为您设置了一个公共 HTML 文件夹，在您无法重命名时，那么您可以将 Craft 的 `web` 文件夹的内容复制到该文件夹并使用您的主机的默认公共 HTML 文件夹。

如果您不使用 [MAMP](https://mamp.info) 或其他本地主机工具，则可能需要更新 hosts 文件，以便您的计算机知道将请求路由到本地计算机的所选主机名。

- **macOS/Linux/Unix:** `/etc/hosts`
- **Windows:** `\Windows\System32\drivers\etc\hosts`

您可以通过将您的Web浏览器指向 `http://HOSTNAME/index.php?p=admin`（`HOSTNAME` 用您的新Web服务器的主机名替换）。

如果成功，您将会访问到 Craft 安装向导。该向导将带您通过数个安装配置页面，然后执行 Craft 的安装。

[Composer]: https://getcomposer.org/
[`craftcms/cms`]: https://github.com/craftcms/cms
[`craftcms/craft`]: https://github.com/craftcms/craft
[Composer installer]: https://getcomposer.org/doc/articles/custom-installers.md
[project]: https://github.com/craftcms/craft
[macOS/Linux/Unix instructions]: https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx
[Windows instructions]: https://getcomposer.org/doc/00-intro.md#installation-windows
[PHP dotenv]: https://github.com/vlucas/phpdotenv
