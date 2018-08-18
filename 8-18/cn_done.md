### 过滤 unserialize()

------

[![PHP 7 新特性](http://www.runoob.com/images/up.gif) PHP 7 新特性](http://www.runoob.com/php/php7-new-features.html)

PHP 7 增加了可以为 `unserialize()` 提供过滤的特性，可以防止非法数据进行代码注入，提供了更安全的反序列化数据。

### 实例

------



```php
<?php 

class MyClass1 {  

   public $obj1prop;    

} 

class MyClass2 { 

   public $obj2prop; 

} 

$obj1 = new MyClass1(); 

$obj1->obj1prop = 1; 

$obj2 = new MyClass2(); 

$obj2->obj2prop = 2; 

$serializedObj1 = serialize($obj1); 

$serializedObj2 = serialize($obj2); 

// 默认行为是接收所有类 

// 第二个参数可以忽略 

// 如果 allowed_classes 设置为 false, unserialize 会将所有对象转换为 __PHP_Incomplete_Class 对象 

$data = unserialize($serializedObj1 , ["allowed_classes" => true]); 

// 转换所有对象到 __PHP_Incomplete_Class 对象，除了 MyClass1 和 MyClass2 

$data2 = unserialize($serializedObj2 , ["allowed_classes" => ["MyClass1", "MyClass2"]]); 

print($data->obj1prop); 

print(PHP_EOL); 

print($data2->obj2prop); 

?>

```



以上程序执行输出结果为：

```
1
2
```

### IntlChar() 

------

PHP 7 通过 intl 扩展来支持国际化 (i18n) 和本地化 (l10n) 。此扩展仅仅是对 ICU 库的基础包装，并提供了和 ICU 库类似的方法和特性。

PHP 7 通过新的 IntlChar 类暴露出 ICU 中的 Unicode 字符特性。这个类自身定义了许多静态方法用于操作多字符集的 unicode 字符。

### 实例

------



```php
<?php 

printf('%x', IntlChar::CODEPOINT_MAX); 

echo IntlChar::charName('@'); 

var_dump(IntlChar::ispunct('!')); 

?>
```

以上程序执行输出结果为：

```php
10ffff
COMMERCIAL AT
bool(true)
```

 