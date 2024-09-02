+++
title = 'PHP编译实验'
date = 2024-09-02T12:20:26+08:00
draft = false
categories = ['PHP']
tags = ['编程', 'PHP']
+++

# 前言

PHP解释器（或称为虚拟机）是C语言编写的，使用GCC可编译成在各种计算机架构系统中的可执行程序。随着国产化的趋势加速进行，PHP作为一个开源的编程语言也在考虑的范围之内。

SAPI的选择：
 1. PHP-FPM - 是LNMP经典组合的选择。
 2. PHP-CLI - 使用Swoole、Workerman等框架开发应用的性能更好。

> 理想的情况下在生产环境二选一即可

# 简化编译

在对8.3.11版本进行配置时，使用参数`--disable-all`会禁用所有的扩展，不同场景使用SAPI也去掉，只保留cli。

```bash
./configure --disable-cgi --disable-phpdbg --disable-all
```

编译后的模块列表包括：

```bash
$ # 查看PHP的扩展
$ php -m
[PHP Modules]
Core
date
hash
json
pcre
random
Reflection
SPL
standard

[Zend Modules]
```

编译后的PHP解释器大小约为`28M`（28736024 byte），编译后整体（包括include、man、lib、bin）的大小为`31M`。
通过这种方式安装的PHP远不能在开发和生产环境使用，通常的框架或应用多少会涉及基础扩展，所以我们按需求场景进行编译安装。

# 基于workerman的编译

worerman所需要的模块官方文档中已经明确指出：`posix`、`pcntl`。最好将event扩展也安装上。
使用composer作为项目管理工具`Phar`、`mbstring`、`iconv`扩展是必不可少的。

```bash
./configure --prefix=/usr/local/php/8.3.11 \
 --with-zlib --with-openssl --enable-pcntl --enable-mbstring \
 --disable-cgi --disable-phpdbg --disable-pdo --disable-simplexml --disable-xml --disable-xmlreader --disable-xmlwriter --disable-dom --without-libxml --without-sqlite3 
```

`zlib`是压缩使用的扩展，例如常用于http的.gz压缩。
有些扩展不指定不安装，例如`pcntl`、`mbstring`。
另一些不指定禁用就会默认安装，例如`iconv`、`Phar`、`posix`。
如果安装`event`扩展，那么要先安装`sockets`扩展。不过这两个扩展可以使用`phpize`单独安装。
*xml*、*sqlite*功能我自己没有用到，所以我也会将相关的扩展去掉。
编译后的PHP解释器大小约为`41M`，编译后整体（包括include、man、lib、bin）的大小约为`55M`。

# docker环境的编译

在docker环境或k8s中一般会启用FPM，使用`--enable-php-fpm`参数启用FPM。同时用`--disable-cli`参数关闭cli模式。这样做有两个好处，一个是可以减少编译时间节省存储空间，另一个没有cli这样的SAPI在某些情况下安全性也会提高。
在相同扩展情况下，编译出的php-fpm和php大小基本一致，只是不同的入口而已。

# 总结

这次实验目的是实践一些想法及得到一些数据。
编译后的PHP在生产环境没有进行验证，仅作参考请自行斟酌使用。  