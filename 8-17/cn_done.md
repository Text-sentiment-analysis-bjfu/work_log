## 匿名类

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 支持通过 **new class** 来实例化一个匿名类，这可以用来替代一些"用后即焚"的完整类定义。

### 实例

------

```php
<?php 

interface Logger { 

   public function log(string $msg); 

} 

class Application { 

   private $logger; 

   public function getLogger(): Logger { 

      return $this->logger; 

   } 

   public function setLogger(Logger $logger) { 

      $this->logger = $logger; 

   }   

} 

$app = new Application; 

// 使用 new class 创建匿名类 

$app->setLogger(new class implements Logger { 

   public function log(string $msg) { 

      print($msg); 

   } 

}); 

$app->getLogger()->log("我的第一条日志"); 

?>

```



以上程序执行输出结果为：

```php
我的第一条日志
```

### Closure::call()

------

PHP 7 的 `Closure::call()` 有着更好的性能，将一个闭包函数动态绑定到一个新的对象实例并调用执行该函数。

### 实例

------
```php
<?php 

class A { 

    private $x = 1; 

} 

// PHP 7 之前版本定义闭包函数代码 

$getXCB = function() { 

    return $this->x; 

}; 

// 闭包函数绑定到类 A 上 

$getX = $getXCB->bindTo(new A, 'A');  

echo $getX(); 

print(PHP_EOL); 

// PHP 7+ 代码 

$getX = function() { 

    return $this->x; 

}; 

echo $getX->call(new A); 

?>

```



以上程序执行输出结果为：

```php
1
1
```

 