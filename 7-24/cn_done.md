
## 在本地进行WordPress开发调试

### [相关代码](https://github.com/cnyy7/wordpress_learing "相关代码") 

## PHP学习 ##
#### [参考链接](http://www.runoob.com/php/php-tutorial.html "PHP 教程 | 菜鸟教程") ####

> ## `$_GET`、`$_POST` 和 `$_REQUEST` 的区别？ ##
> 1. `$_GET` 变量接受所有以 `get`  方式发送的请求，及浏览器地> 址栏中的 ? 之后的内容。

> 1. `$_POST` 变量接受所有以 `post` 方式发送的请求，例如，一> 个 `form` 以 `method=post` 提交，提交后 php 会处理 > `post` 过来的全部变量。

> 1. `$_REQUEST` 支持两种方式发送过来的请求，即 `post` 和 `get` 它都可以接受，显示不显示要看传递方法，`get` 会显示在 url 中（有字符数限制），`post` 不会在 url 中显示，可以传递任意多的数据（只要服务器支持）。

## PHP $_GET 变量 ##
预定义的 `$_GET` 变量用于收集来自 `method="get"` 的表单中的值。

从带有 GET 方法的表单发送的信息，对任何人都是可见的（会显示在浏览器的地址栏），并且对发送信息的量也有限制。
#### 实例 ####
form.html 文件代码如下：
	<html>
	<head>
	<meta charset="utf-8">
	<title>菜鸟教程(runoob.com)</title>
	</head>
	<body>
	
	<form action="welcome.php" method="get">
	名字: <input type="text" name="fname">
	年龄: <input type="text" name="age">
	<input type="submit" value="提交">
	</form>
	
	</body>
	</html>

当用户点击 `Submit ` 按钮时，发送到服务器的 URL 如下所示：

	http://www.runoob.com/welcome.php?fname=Runoob&amp;age=3

`welcome.php` 文件现在可以通过 `$_GET` 变量来收集表单数据了（注意，表单域的名称会自动成为 `$_GET` 数组中的键）：

	欢迎 <?php echo $_GET["fname"]; ?>!<br>
	你的年龄是 <?php echo $_GET["age"]; ?>  岁。

动态演示：

![](http://i1.bvimg.com/602998/d527c658f0a6268c.gif)



### 何时使用 `method="get"` ？ ###
---

- 在 HTML 表单中使用 `method="get"` 时，所有的变量名和值都会显示在 URL 中。

- **注释**：所以在发送密码或其他敏感信息时，不应该使用这个方法！

- 然而，正因为变量显示在 `URL` 中，因此可以在收藏夹中收藏该页面。在某些情况下，这是很有用的。

- **注释**：`HTTP GET` 方法不适合大型的变量值。它的值是不能超过 2000 个字符的。

## PHP $_POST 变量 ##
预定义的 $_POST 变量用于收集来自 method="post" 的表单中的值。

从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制。

注释：然而，默认情况下，POST 方法的发送信息的量最大值为 8 MB（可通过设置 php.ini 文件中的 post_max_size 进行更改）。
#### 实例 ####

form.html 文件代码如下：

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

当用户点击 "提交" 按钮时，URL 类似如下所示：

	http://www.runoob.com/welcome.php
"welcome.php" 文件现在可以通过 $_POST 变量来收集表单数据了（请注意，表单域的名称会自动成为 $_POST 数组中的键）：
	
	欢迎 <?php echo $_POST["fname"]; ?>!<br>
	你的年龄是 <?php echo $_POST["age"]; ?>  岁。
动态演示：

![](http://i4.bvimg.com/602998/cdaba2a44061e411.gif)
### 何时使用 `method="post"`？ ###
从带有 `POST` 方法的表单发送的信息，对任何人都是不可见的，并且对发送信息的量也没有限制。

然而，由于变量不显示在 URL 中，所以无法把页面加入书签。
## PHP `$_REQUEST` 变量 ##

预定义的 `$_REQUEST` 变量包含了 `$_GET`、`$_POST` 和 `$_COOKIE` 的内容。

`$_REQUEST` 变量可用来收集通过 `GET` 和 `POST` 方法发送的表单数据。

#### 实例 ####
可以将 "welcome.php" 文件修改为如下代码，它可以接受 `$_GET`、`$_POST`等数据。

	欢迎 <?php echo $_REQUEST["fname"]; ?>!<br>
	你的年龄是 <?php echo $_REQUEST["age"]; ?>  岁。
