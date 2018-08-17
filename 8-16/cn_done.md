### NULL 合并运算符

------

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 新增加的 NULL 合并运算符`??`是用于执行`isset()`检测的三元运算的快捷方式。

`NULL` 合并运算符会判断变量是否存在且值不为`NULL`，如果是，它就会返回自身的值，否则返回它的第二个操作数。

以前这样写三元运算符：

```php
$site = isset($_GET['site']) ? $_GET['site'] : '菜鸟教程';
```

现在可以直接这样写：

```php
$site = $_GET['site'] ?? '菜鸟教程';
```

#### 实例

```php
<?php
// 获取 $_GET['site'] 的值，如果不存在返回 '菜鸟教程'
$site = $_GET['site'] ?? '菜鸟教程';

print($site);
print(PHP_EOL); // PHP_EOL 为换行符


// 以上代码等价于
$site = isset($_GET['site']) ? $_GET['site'] : '菜鸟教程';

print($site);
print(PHP_EOL);
// ?? 链
$site = $_GET['site'] ?? $_POST['site'] ?? '菜鸟教程';

print($site);
?>
```

以上程序执行输出结果为：

```php
菜鸟教程
菜鸟教程
菜鸟教程
```

### 太空船运算符（组合比较符）

------

PHP 7 新增加的太空船运算符（组合比较符）用于比较两个表达式 **$a** 和 **$b**，如果 **$a** 小于、等于或大于 **$b**时，它分别返回-1、0或1。

#### 实例

```php
<?php
// 整型比较
print( 1 <=> 1);print(PHP_EOL);
print( 1 <=> 2);print(PHP_EOL);
print( 2 <=> 1);print(PHP_EOL);
print(PHP_EOL); // PHP_EOL 为换行符

// 浮点型比较
print( 1.5 <=> 1.5);print(PHP_EOL);
print( 1.5 <=> 2.5);print(PHP_EOL);
print( 2.5 <=> 1.5);print(PHP_EOL);
print(PHP_EOL);

// 字符串比较
print( "a" <=> "a");print(PHP_EOL);
print( "a" <=> "b");print(PHP_EOL);
print( "b" <=> "a");print(PHP_EOL);
?>
```

以上程序执行输出结果为：

```php
0
-1
1

0
-1
1

0
-1
1
```

### 常量数组

------

在 PHP 5.6 中仅能通过 const 定义常量数组，PHP 7 可以通过 `define()` 来定义。

#### 实例

```php
<?php
// 使用 define 函数来定义数组
define('sites', [
   'Google',
   'Runoob',
   'Taobao'
]);

print(sites[1]);
?>
```

以上程序执行输出结果为：

```php
Runoob
```