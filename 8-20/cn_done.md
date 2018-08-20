## PHP 7 异常

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 异常用于向下兼容及增强旧的`assert()`函数。它能在生产环境中实现零成本的断言，并且提供抛出自定义异常及错误的能力。

老版本的API出于兼容目的将继续被维护，`assert()`现在是一个语言结构，它允许第一个参数是一个表达式，而不仅仅是一个待计算的 string或一个待测试的boolean。

------

### assert() 配置

------



| 配置项           | 默认值 | 可选值                                                       |
| ---------------- | ------ | ------------------------------------------------------------ |
| zend.assertions  | 1      | **1** - 生成和执行代码 (开发模式)**0** - 生成代码，但在执行时跳过它**-1** - 不生成代码 (生产环境) |
| assert.exception | 0      | **1** - 断言失败时抛出，可以抛出异常对象，如果没有提供异常，则抛出 `AssertionError` 对象实例。**0** - 使用或生成 `Throwable`, 仅仅是基于对象生成的警告而不是抛出对象(与 PHP 5 兼容) |

### 参数

- **assertion**

  断言。在 PHP 5 中，是一个用于执行的字符串或者用于测试的布尔值。在 PHP 7 中，可以是一个返回任何值的表达式， 它将被执行结果用于指明断言是否成功。

- **description**

  如果 `assertion` 失败了，选项 `description` 将会包括在失败信息里。

- **exception**

  在 PHP 7 中，第二个参数可以是一个 **Throwable** 对象，而不是一个字符串，如果断言失败且启用了 `assert.exception` 该对象将被抛出。

### 实例

将 `zend.assertions` 设置为 0：

```php
<?php 

ini_set('zend.assertions', 0); 

assert(true == false); 

echo 'Hi!'; 

?>

```



以上程序执行输出结果为：

```
Hi!
```

将 `zend.assertions` 设置为 1，`assert.exception` 设置为 1：

### 实例

------



```php
<?php 

ini_set('zend.assertions', 1); 

ini_set('assert.exception', 1); 

assert(true == false); 

echo 'Hi!'; 

?>

```



以上程序执行输出结果为：

```php
Fatal error: Uncaught AssertionError: assert(true == false) in -:2
Stack trace:
#0 -(2): assert(false, 'assert(true == ...')
#1 {main}
  thrown in - on line 2
```