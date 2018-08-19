## CSPRNG

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

CSPRNG（Cryptographically Secure Pseudo-Random Number Generator，伪随机数产生器）。

PHP 7 通过引入几个 CSPRNG 函数提供一种简单的机制来生成密码学上强壮的随机数。

- **random_bytes()** - 加密生存被保护的伪随机字符串。
- **random_int()** - 加密生存被保护的伪随机整数。

------

### random_bytes()

------

### 语法格式

```php
string random_bytes ( int $length )
```

### 参数

- **length** - 随机字符串返回的字节数。

### 返回值

- 返回一个字符串，接受一个int型入参代表返回结果的字节数。

### 实例

------



```php
<?php 

$bytes = random_bytes(5); 

print(bin2hex($bytes)); 

?>

```



以上程序执行输出结果为：

```php
6f36d48a29
```

------

### random_int()

------

### 语法格式

```php
int random_int ( int $min , int $max )
```

### 参数

- **min** - 返回的最小值，必须是大于或等于 PHP_INT_MIN 。
- **max** - 返回的最大值，必须是小于或等于 PHP_INT_MAX 。

### 返回值

- 返回一个指定范围内的int型数字。

### 实例

------



```php
<?php 

print(random_int(100, 999)); 

print(PHP_EOL); 

print(random_int(-1000, 0)); 

?>

```



以上程序执行输出结果为：

```php
723
-64
```