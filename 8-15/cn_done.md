 ## 标量类型声明

   默认情况下，所有的PHP文件都处于弱类型校验模式。

   PHP 7 增加了标量类型声明的特性，标量类型声明有两种模式:

   - 强制模式 (默认)
   - 严格模式

   标量类型声明语法格式：

   ```php
   declare(strict_types=1); 
   ```

   代码中通过指定 strict_types的值（1或者0），1表示严格类型校验模式，作用于函数调用和返回语句；0表示弱类型校验模式。

   可以使用的类型参数有：

   - int
   - float
   - bool
   - string
   - interfaces
   - array
   - callable

   ### 强制模式实例

   #### 实例

```php
   <?php 

   // 强制模式 

   function sum(int ...$ints) 

   { 

      return array_sum($ints); 

   } 

   print(sum(2, '3', 4.1)); 

   ?>

```



   以上程序执行输出结果为：

   ```php
   9
   ```

   实例汇总将参数 4.1 转换为整数 4 后再相加。

   ### 严格模式实例

   #### 实例

```php
   <?php 

   // 严格模式 

   declare(strict_types=1); 

   function sum(int ...$ints) 

   { 

      return array_sum($ints); 

   } 

   print(sum(2, '3', 4.1)); 

   ?>

```



   以上程序由于采用了严格模式，所以如果参数中出现不适整数的类型会报错，执行输出结果为：

   ```php
   PHP Fatal error:  Uncaught TypeError: Argument 2 passed to sum() must be of the type integer, string given, called in……
   ```

------

   ### 返回类型声明

   PHP 7 增加了对返回类型声明的支持，返回类型声明指明了函数返回值的类型。

   可以声明的返回类型有：

   - int
   - float
   - bool
   - string
   - interfaces
   - array
   - callable

   ### 返回类型声明实例

   实例中，要求返回结果为整数：

   #### 实例

   ```php
   <?php 
   
   declare(strict_types=1); 
   
   function returnIntValue(int $value): int 
   
   { 
   
      return $value; 
   
   } 
   
   print(returnIntValue(5)); 
   
   ?>
   
   ```

   

   以上程序执行输出结果为：

   ```php
   5
   ```

   ### 返回类型声明错误实例

   #### 实例

   ```php
   <?php 
   
   declare(strict_types=1); 
   
   function returnIntValue(int $value): int 
   
   { 
   
      return $value + 1.0; 
   
   } 
   
   print(returnIntValue(5)); 
   
   ?>
   
   ```

   

   以上程序由于采用了严格模式，返回值必须是 int，但是计算结果是float，所以会报错，执行输出结果为：

   ```php
   Fatal error: Uncaught TypeError: Return value of returnIntValue() must be of the type integer, float returned...
   ```