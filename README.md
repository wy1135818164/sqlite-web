![](http://media.charlesleifer.com/blog/photos/sqlite-web.png)

`sqlite-web` 是用Python编写的基于Web的SQLite数据库浏览器。
 从coleifer/sqlite-web分叉，进行了页面汉化处理

项目依赖项:

* [flask](http://flask.pocoo.org)
* [peewee](http://docs.peewee-orm.com)
* [pygments](http://pygments.org)

### 安装

```sh
$ pip install sqlite-web
```

### 使用

```sh
$ sqlite_web /path/to/database.db
```

### 特点

![](http://media.charlesleifer.com/blog/photos/p1494359468.71.gif)

* 可以与现有的SQLite数据库一起使用，也可以用于创建新的数据库。
* 添加或删除:
  * 表
  * 列（是的，您可以删除并重命名列！）
  * 索引
* 导出数据为JSON或CSV（导出时，注意表名不能为中文）。
* 导入JSON或CSV。
* 浏览表数据。

### 屏幕截图

首页显示有关数据库的一些基本信息，包括表和索引的数量以及其在磁盘上的大小：

![](https://github.com/wy1135818164/sqlite-web/blob/master/首页.png)

“表结构”选项卡显示关于表结构的信息，包括列、索引和外键(如果存在的话)。您还可以在此页面中创建、重命名或删除列和索引。

![](https://github.com/wy1135818164/sqlite-web/blob/master/表结构.png)

“内容”选项卡显示所有表格数据。表标头中的链接可用于对数据进行排序

![](https://github.com/wy1135818164/sqlite-web/blob/master/内容.png)

“查询”选项卡允许您对表执行任意SQL查询。查询结果显示在一个表中，可以导出为JSON或CSV

![](https://github.com/wy1135818164/sqlite-web/blob/master/查询.png)

“导入”选项卡支持导入CSV和JSON文件到表中。有一个选项可以为导入文件中任何无法识别的键自动创建列

![](https://github.com/wy1135818164/sqlite-web/blob/master/导入.png)

### 命令行选项

调用sqlite-web的语法是：

```console

$ sqlite_web [options] /path/to/database-file.db
```

可以使用下列选项：

* ``-p``, ``--port``: 初始值为 8080
* ``-H``, ``--host``: 初始值为 127.0.0.1
* ``-d``, ``--debug``: 初始值为 false
* ``-x``, ``--no-browser``: 当sqlite-web启动时不打开web浏览器
* ``-P``, ``--password``: 提示输入密码以访问sqlite-web。或者，可以将密码存储在“ SQLITE_WEB_PASSWORD”环境变量中，在这种情况下，应用程序不会提示输入密码，而是使用来自环境的值。
* ``-r``, ``--read-only``: 以只读模式打开数据库。
* ``-u``, ``--url-prefix``: 应用程序的url前缀，例如 “ / sqlite-web”。

### 使用 docker

sqlite-web提供了一个Dockerfile。 使用方法：

```console

$ cd docker/  # Change dirs to the dir containing Dockerfile
$ docker build -t coleifer/sqlite-web .
$ docker run -it --rm \
    -p 8080:8080 \
    -v /path/to/your-data:/data \
    -e SQLITE_DATABASE=db_filename.db \
    coleifer/sqlite-web
```
