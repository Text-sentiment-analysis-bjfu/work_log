### intdiv() 函数

------

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 新增加了 `intdiv()` 函数，接收两个参数，返回值为第一个参数除于第二个参数的值并取整。

#### 实例

------
```php
<?php 

echo intdiv(9,3),PHP_EOL; 

echo intdiv(10,3),PHP_EOL; 

echo intdiv(5,10),PHP_EOL; 

?>

```



以上程序执行输出结果为：

```
3
3
0
```

### Session 选项

------

PHP 7 `session_start()`函数可以接收一个数组作为参数，可以覆盖php.ini中session的配置项。

这个特性也引入了一个新的php.ini设置（`session.lazy_write`）,默认情况下设置为 true，意味着session数据只在发生变化时才写入。

除了常规的会话配置指示项， 还可以在此数组中包含 `read_and_close` 选项。如果将此选项的值设置为 TRUE， 那么会话文件会在读取完毕之后马上关闭， 因此，可以在会话数据没有变动的时候，避免不必要的文件锁。

#### 实例

把`cache_limiter`设置为私有的，同时在阅读完session后立即关闭。

------

```php
<?php 

session_start( 

   'cache_limiter' => 'private', 

   'read_and_close' => true, 

]); 

?>

```

