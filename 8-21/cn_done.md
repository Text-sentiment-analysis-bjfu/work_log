## use 语句

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 可以使用一个 use 从同一个 namespace 中导入类、函数和常量：

### 实例

------



```php
// PHP 7 之前版本需要使用多次 use 

use some\namespace\ClassA; 

use some\namespace\ClassB; 

use some\namespace\ClassC as C; 

use function some\namespace\fn_a; 

use function some\namespace\fn_b; 

use function some\namespace\fn_c; 

use const some\namespace\ConstA; 

use const some\namespace\ConstB; 
 
use const some\namespace\ConstC; 

// PHP 7+ 之后版本可以使用一个 use 导入同一个 namespace 的类 

use some\namespace{ClassA, ClassB, ClassC as C}; 

use function some\namespace{fn_a, fn_b, fn_c}; 

use const some\namespace{ConstA, ConstB, ConstC}; 

?>

```

## 错误处理

------

PHP 7 改变了大多数错误的报告方式。不同于 PHP 5 的传统错误报告机制，现在大多数错误被作为 **Error** 异常抛出。

这种 Error 异常可以像普通异常一样被 try / catch 块所捕获。如果没有匹配的 try / catch 块， 则调用异常处理函数（由 `set_exception_handler()` 注册）进行处理。 如果尚未注册异常处理函数，则按照传统方式处理：被报告为一个致命错误（Fatal Error）。

Error 类并不是从 Exception 类 扩展出来的，所以用 `catch (Exception $e) { ... }` 这样的代码是捕获不 到 Error 的。你可以用 `catch (Error $e) { ... }` 这样的代码，或者通过注册异常处理函数（ `set_exception_handler()`）来捕获 Error。

### Error 异常层次结构

- **Error**
  - **ArithmeticError**
  - **AssertionError**
  - **DivisionByZeroError**
  - **ParseError**
  - **TypeError**
- Exception
  - ...

![img](http://www.runoob.com/wp-content/uploads/2016/03/1458887252-2773-exception-hiearchy.jpg)

### 实例

```php
<?php 

class MathOperations  

{ 

   protected $n = 10; 

   // 求余数运算，除数为 0，抛出异常 

   public function doOperation(): string 

   { 

      try { 

         $value = $this->n % 0; 

         return $value; 

      } catch (DivisionByZeroError $e) { 

         return $e->getMessage(); 

      } 

   } 

} 

$mathOperationsObj = new MathOperations(); 

print($mathOperationsObj->doOperation()); 

?>

```



以上程序执行输出结果为：

```php
Modulo by zero
```