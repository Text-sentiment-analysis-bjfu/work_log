## include 和 require 语句

在 PHP 中，你可以在服务器执行 PHP 文件之前在该文件中插入一个文件的内容。

include 和 require 语句用于在执行流中插入写在其他文件中的有用的代码。

**include 和 require 除了处理错误的方式不同之外，在其他方面都是相同的：**

- require 生成一个致命错误（`E_COMPILE_ERROR`），在错误发生后脚本会停止执行。
- include 生成一个警告（`E_WARNING`），在错误发生后脚本会继续执行。

因此，如果你希望继续执行，并向用户输出结果，即使包含文件已丢失，那么请使用 include。否则，在框架、CMS 或者复杂的 PHP 应用程序编程中，请始终使用 require 向执行流引用关键文件。这有助于提高应用程序的安全性和完整性，在某个关键文件意外丢失的情况下。

包含文件省去了大量的工作。这意味着你可以为所有网页创建标准页头、页脚或者菜单文件。然后，在页头需要更新时，你只需更新这个页头包含文件即可。

## 语法

```php
include 'filename';

或者

require 'filename';
```

------

## include 和 require 语句

### 基础实例

假设你有一个标准的页头文件，名为 "header.php"。如需在页面中引用这个页头文件，请使用 include/require：

```php+HTML
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<?php include 'header.php'; ?>
<h1>欢迎来到我的主页!</h1>
<p>一些文本。</p>

</body>
</html>
```

### 实例 2

假设我们有一个在所有页面中使用的标准菜单文件。

"menu.php":

```php+HTML
echo '<a href="/">主页</a>
<a href="/html">HTML 教程</a>
<a href="/php">PHP 教程</a>';
```

网站中的所有页面均应引用该菜单文件。以下是具体的做法：

```php+HTML
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<div class="leftmenu">
<?php include 'menu.php'; ?>
</div>
<h1>欢迎来到我的主页!</h1>
<p>一些文本。</p>

</body>
</html>
```

### 实例 3

假设我们有一个定义变量的包含文件（"vars.php"）：

```php
<?php
$color='red';
$car='BMW';
?>
```

这些变量可用在调用文件中：

```php+HTML
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<h1>欢迎来到我的主页!</h1>
<?php 
include 'vars.php';
echo "I have a $color $car"; // I have a red BMW
?>

</body>
</html>
```

## PHP 中 include 和 require 的区别详解

## 1、概要

`require()` 语句的性能与 `include()` 相类似，都是包括并运行指定文件。不同之处在于：对 include() 语句来说，在执行文件时每次都要进行读取和评估；而对于 require() 来说，文件只处理一次（实际上，文件内容替换 require() 语句）。这就意味着如果可能执行多次的代码，则使用 require() 效率比较高。另外一方面，如果每次执行代码时是读取不同的文件，或者有通过一组文件迭代的循环，就使用 include() 语句。

require() 的使用方法如：

```php
require("myfile.php")
```

这个语句通常放在 PHP 脚本程序的最前面。PHP 程序在执行前，就会先读入 require() 语句所引入的文件，使它变成 PHP 脚本文件的一部分。

include() 使用方法和 require 一样如：

```php
include("myfile.php")
```

这个语句一般是放在流程控制的处理区段中。

PHP 脚本文件在读到 include() 语句时，才将它包含的文件读取进来。这种方式，可以把程式执行时的流程简单化。

- **incluce** 在用到时加载
- **require** 在一开始就加载
- **_once** 后缀表示已加载的不加载

PHP 系统在加载PHP程序时有一个伪编译过程，可使程序运行速度加快。但 incluce 的文档仍为解释执行。include 的文件中出错了，主程序继续往下执行，require 的文件出错了，主程序也停了，所以包含的文件出错对系统影响不大的话（如界面文件）就用 include，否则用 require。

`require()` 和 `include()` 语句是语言结构，不是真正的函数，可以像 php 中其他的语言结构一样，例如 `echo()` 可以使用 `echo("ab")` 形式，也可以使用 echo "abc" 形式输出字符串 abc。`require()` 和`include()` 语句也可以不加圆括号而直接加参数。

`include_once()` 和 `require_once()` 语句也是在脚本执行期间包括运行指定文件。此行为和 `include()` 语句及 `require()` 类似，使用方法也一样。唯一区别是如果该文件中的代码已经被包括了，则不会再次包括。这两个语句应该用于在脚本执行期间，同一个文件有可能被包括超过一次的情况下，确保它只被包括一次，以避免函数重定义以及变量重新赋值等问题。

------

## 2、详解

### 2.1 报错

**include** 引入文件的时候，如果碰到错误，会给出提示，并继续运行下边的代码。

**require** 引入文件的时候，如果碰到错误，会给出提示，并停止运行下边的代码。

用例子来说话，写两个 php 文件，名字为 test-include.php 和 test-require.php，注意相同的目录中，不要存在一个名字是 test-nothing.php 的文件。

###### test-include.php

```php
<?php include 'test-nothing.php'; echo 'abc'; ?>
```

###### test-require.php

```php
<?php require 'test-nothing.php'; echo 'abc'; ?>
```

浏览 **http://localhost/test-include.php**，因为没有找到 test-nothing.php 文件，我们看到了报错信息，同时，报错信息的下边显示了 abc，你看到的可能是类似下边的情况：

```php
Warning: include(test-nothing.php) [function.include]: failed to open stream: No such file or directory in D:\www\test-include.php on line 2

Warning: include() [function.include]: Failed opening 'test-nothing.php' for inclusion (include_path='.;C:\php5\pear') in D:\www\test-include.php on line 2

abc
```

浏览 http://localhost/test-require.php，因为没有找到 test-nothing.php 文件，我们看到了报错信息，但是，报错信息的下边没 有显示abc，你看到的可能是类似下边的情况：

```php
Warning: require(test-nothing.php) [function.require]: failed to open stream: No such file or directory in D:\www\test-require.php on line 2

Fatal error: require() [function.require]: Failed opening required 'test-nothing' (include_path='.;C:\php5\pear') in D:\www\test-require.php on line 2 
```

### 2.2 文件引用方式

`include()` 执行时需要引用的文件每次都要进行读取和评估，`require()` 执行时需要引用的文件只处理一次（实际上执行时需要引用的文件内容替换了 `require()` 语句）可以看出若有包含这些指令之一的代码和可能执行多次的代码，则使用 `require()` 效率比较高，若每次执行代码时相读取不同的文件或者有通过一组文件叠代的循环，就使用 `include()`，可以给想要包括的文件名设置变量，当参数为 `include()` 时使用这个变量。