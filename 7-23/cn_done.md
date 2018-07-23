
## 在本地进行WordPress开发调试

### [相关代码](https://github.com/cnyy7/wordpress_learing "相关代码") 

## PHP学习 ##
#### [参考链接](http://www.runoob.com/php/php-tutorial.html "PHP 教程 | 菜鸟教程") ####

## PHP 表单和用户输入 ##
#### PHP 中的 $_GET 和 $_POST 变量用于检索表单中的信息，比如用户输入。 ####
>有一点很重要的事情值得注意，当处理 HTML 表单时，PHP 能把来自 HTML 页面中的表单元素自动变成可供 PHP 脚本使用。

下面的实例包含了一个 HTML 表单，带有两个输入框和一个提交按钮。

	<html>
	<head>
	<meta charset="utf-8">
	<title>菜鸟教程(runoob.com)</title>
	</head>
	<body>
	 
	<form action="welcome.php" method="post">
	名字: <input type="text" name="fname">
	年龄: <input type="text" name="age">
	<input type="submit" value="提交">
	</form>
	 
	</body>
	</html>

当用户填写完上面的表单并点击提交按钮时，表单的数据会被送往名为 "welcome.php" 的 PHP 文件：
	
	欢迎<?php echo $_POST["fname"]; ?>!<br>
	你的年龄是 <?php echo $_POST["age"]; ?>  岁。

这是当用户输入后就能获取输入，并显示出来。

## PHP 获取下拉菜单的数据 ##
#### PHP 下拉菜单单选 ####
以下实例设置了下拉菜单三个选项，表单使用 `GET` 方式获取数据，`action` 属性值为空表示提交到当前脚本，可以通过 `select` 的 `name` 属性获取下拉菜单的值：

`php_form_select.php` 文件代码：

	<?php
	$q = isset($_GET['q'])? htmlspecialchars($_GET['q']) : '';
	if($q) {
	        if($q =='RUNOOB') {
	                echo '菜鸟教程<br>http://www.runoob.com';
	        } else if($q =='GOOGLE') {
	                echo 'Google 搜索<br>http://www.google.com';
	        } else if($q =='TAOBAO') {
	                echo '淘宝<br>http://www.taobao.com';
	        }
	} else {
	?>
	<form action="" method="get"> 
	    <select name="q">
	    <option value="">选择一个站点:</option>
	    <option value="RUNOOB">Runoob</option>
	    <option value="GOOGLE">Google</option>
	    <option value="TAOBAO">Taobao</option>
	    </select>
	    <input type="submit" value="提交">
	    </form>
	<?php
	}
	?>

#### PHP 下拉菜单多选 ####

如果下拉菜单是多选的 `multiple="multiple"`，可以通过将设置 `select name="q[]"` 以数组的方式获取，以下使用 `POST` 方式提交，代码如下所示：

php_form_select_mul.php 文件代码：

	<?php
	$q = isset($_POST['q'])? $_POST['q'] : '';
	if(is_array($q)) {
	    $sites = array(
	            'RUNOOB' => '菜鸟教程: http://www.runoob.com',
	            'GOOGLE' => 'Google 搜索: http://www.google.com',
	            'TAOBAO' => '淘宝: http://www.taobao.com',
	    );
	    foreach($q as $val) {
	        // PHP_EOL 为常量，用于换行
	        echo $sites[$val] . PHP_EOL;
	    }
	      
	} else {
	?>
	<form action="" method="post"> 
	    <select multiple="multiple" name="q[]">
	    <option value="">选择一个站点:</option>
	    <option value="RUNOOB">Runoob</option>
	    <option value="GOOGLE">Google</option>
	    <option value="TAOBAO">Taobao</option>
	    </select>
	    <input type="submit" value="提交">
	    </form>
	<?php
	}
	?>

#### 单选按钮表单 ####

PHP 单选按钮表单中 name 属性的值是一致的，value 值是不同的，代码如下所示：

php_form_radio.php 文件代码：

	<?php
	$q = isset($_GET['q'])? htmlspecialchars($_GET['q']) : '';
	if($q) {
	        if($q =='RUNOOB') {
	                echo '菜鸟教程<br>http://www.runoob.com';
	        } else if($q =='GOOGLE') {
	                echo 'Google 搜索<br>http://www.google.com';
	        } else if($q =='TAOBAO') {
	                echo '淘宝<br>http://www.taobao.com';
	        }
	} else {
	?><form action="" method="get"> 
	    <input type="radio" name="q" value="RUNOOB" />Runoob
	    <input type="radio" name="q" value="GOOGLE" />Google
	    <input type="radio" name="q" value="TAOBAO" />Taobao
	    <input type="submit" value="提交">
	</form>
	<?php
	}
	?>

## `$_GET`、`$_POST` 和 `$_REQUEST` 的区别？ ##
1. `$_GET` 变量接受所有以 `get` 方式发送的请求，及浏览器地址栏中的 ? 之后的内容。

1. `$_POST` 变量接受所有以 `post` 方式发送的请求，例如，一个 `form` 以 `method=post` 提交，提交后 php 会处理 `post` 过来的全部变量。

1. `$_REQUEST` 支持两种方式发送过来的请求，即 `post` 和 `get` 它都可以接受，显示不显示要看传递方法，`get` 会显示在 url 中（有字符数限制），`post` 不会在 url 中显示，可以传递任意多的数据（只要服务器支持）。