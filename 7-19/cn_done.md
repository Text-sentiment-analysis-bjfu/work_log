
## 在本地进行WordPress开发调试

### [相关代码](https://github.com/cnyy7/wordpress_learing "相关代码") 

## PHP学习 ##
#### [参考链接](http://www.runoob.com/php/php-tutorial.html "PHP 教程 | 菜鸟教程") ####

- PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。
- PHP 脚本可以放在文档中的任何位置。PHP 脚本以 `<?php` 开始，以 `?>` 结束： 

        <?php
    	// PHP 代码
    	?>
- 以下是一个PHP 文件实例，它可以向浏览器输出文本 "Hello World!"

        <!DOCTYPE html> 
	    <html> 
	    <body> 
	    
	    <h1>My first PHP page</h1> 
	    
	    <?php 
	    echo "Hello World!"; 
	    ?> 
	    
	    </body> 
	    </html>
- 注意，PHP 中的每个代码行都必须以分号结束。分号是一种分隔符，用于把指令集区分开来。
## PHP变量 ##
- 与代数类似，可以给 PHP 变量赋予某个值（x=5）或者表达式（z=x+y）

- 变量可以是很短的名称（如 x 和 y）或者更具描述性的名称（如 age、carname、totalvolume）

 
### PHP 变量规则： ###

1. 变量以 $ 符号开始，后面跟着变量的名称
1. 变量名必须以字母或者下划线字符开始
1. 变量名只能包含字母数字字符以及下划线（`A-z`、`0-9` 和` _` ）
1. 变量名不能包含空格
1. 变量名是区分大小写的（`$y `和` $Y` 是两个不同的变量）

----------

- PHP 没有声明变量的命令。
- 变量在您第一次赋值给它的时候被创建：
- 以下是一个实例
 
	    <?php
    	$txt="Hello world!";
    	$x=5;
    	$y=10.5;
    	?>
#### PHP 是一门弱类型语言，不必向 PHP 声明该变量的数据类型。PHP 会根据变量的值，自动把变量转换为正确的数据类型。 ####
## PHP输出语句 ##
**在 PHP 中有两个基本的输出方式： echo 和 print。**

- echo 是一个语言结构，使用的时候可以不用加括号，也可以加上括号： echo 或 echo()。
- 下面演示了如何使用 echo 命令输出字符串（字符串可以包含 HTML 标签）：

    	<?php
	    $txt1=" 学习 PHP";
	    $txt2="RUNOOB.COM";
	    $cars=array("Volvo","BMW","Toyota");
	     
	    echo $txt1;
	    echo "<br>";
	    echo " 在 $txt2 学习 PHP ";
	    echo "<br>";
	    echo " 我车的品牌是 {$cars[0]}";
	    ?>	
- print 同样是一个语言结构，可以使用括号，也可以不使用括号： print 或 print()。

	    <?php
	    $txt1=" 学习 PHP";
	    $txt2="RUNOOB.COM";
	    $cars=array("Volvo","BMW","Toyota");
	     
	    print $txt1;
	    print "<br>";
	    print " 在 $txt2 学习 PHP ";
	    print "<br>";
	    print " 我车的品牌是 {$cars[0]}";
	    ?>
### echo 和 print 语句的区别 ###
1. echo 可以输出一个或多个字符串；
1. print 只允许输出一个字符串，返回值总为 1；
1. echo 输出的速度比 print 快；
1. echo 没有返回值，print 有返回值 1；
## PHP 数组排序 ##
**数组中的元素可以按字母或数字顺序进行降序或升序排列。**

- sort() - 对数组进行升序排列
- rsort() - 对数组进行降序排列
- asort() - 根据关联数组的值，对数组进行升序排列
- ksort() - 根据关联数组的键，对数组进行升序排列
- arsort() - 根据关联数组的值，对数组进行降序排列
- krsort() - 根据关联数组的键	，对数组进行降序排列
#### 举例，下面对数组按字母降序排序 ####
    <?php
	$cars=array("Volvo","BMW","Toyota");
	rsort($cars);
	?>
## PHP 超级全局变量 ##
- PHP 中预定义了几个超级全局变量（superglobals） ，这意味着它们在一个脚本的全部作用域中都可用。 不需要特别说明，就可以在函数及类中使用。

**PHP 超级全局变量列表:**

- $GLOBALS
- $_SERVER
- $_REQUEST
- $_POST
- $_GET
- $_FILES
- $_ENV
- $_COOKIE
- $_SESSION
## PHP 魔术常量 ##
 PHP 向它运行的任何脚本提供了大量的预定义常量。

 不过很多常量都是由不同的扩展库定义的，只有在加载了这些扩展库时才会出现，或者动态加载后，或者在编译时已经包括进去了。

 有八个魔术常量它们的值随着它们在代码中的位置改变而改变。



1.   `__LINE__` &#160;&#160;&#160;&#160;&#160;&#160;	&#160;文件中的当前行号。
1.  `__FILE__`		&#160;&#160;&#160;&#160;&#160;&#160;	&#160;文件的完整路径和文件名。如果用在被包含文件中，则返回被包含的文件名。
1.  `__DIR__`   &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; &#160;文件所在的目录。如果用在被包括文件中，则返回被包括的文件所在的目录。
1.  `__FUNCTION__`&#160;&#160;函数名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该函数被定义时的名字（区分大小写）。在 PHP 4 中该值总是小写字母的。
1.  `__CLASS__`&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;类的名称（PHP 4.3.0 新加）。自 PHP 5 起本常量返回该类被定义时的名字（区分大小写）。
1. `__TRAIT__`&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Trait 的名字（PHP 5.4.0 新加）。自 PHP 5.4.0 起，PHP 实现了代码复用的一个方法，称为 traits。
1. `__METHOD__`&#160;&#160;&#160;&#160;&#160;&#160;类的方法名（PHP 5.0.0 新加）。返回该方法被定义时的名字（区分大小写）。
1. `__NAMESPACE__`&#160;当前命名空间的名称（区分大小写）。此常量是在编译时定义的（PHP 5.3.0 新增）。