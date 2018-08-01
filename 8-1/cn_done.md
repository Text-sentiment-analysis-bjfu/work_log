## Cookie 是什么？

cookie 常用于识别用户。cookie 是一种服务器留在用户计算机上的小文件。每当同一台计算机通过浏览器请求页面时，这台计算机将会发送 cookie。通过 PHP，能够创建并取回 cookie 的值。

------

## 如何创建 Cookie？

`setcookie()` 函数用于设置 cookie。

**注释：**`setcookie()` 函数必须位于 <html> 标签之前。

### 语法

```php
setcookie(name, value, expire, path, domain);
```

### 实例 1

在下面的例子中，将创建名为 "user" 的 cookie，并为它赋值 "runoob"。也规定了此 cookie 在一小时后过期：

```php
<?php
setcookie("user", "runoob", time()+3600);
?>

<html>
.....
```

**注释：**在发送 cookie 时，cookie 的值会自动进行 URL 编码，在取回时进行自动解码。（为防止 URL 编码，请使用 `setrawcookie()` 取而代之。）

### 实例 2

还可以通过另一种方式设置 cookie 的过期时间。这也许比使用秒表示的方式简单。

```php
<?php
$expire=time()+60*60*24*30;
setcookie("user", "runoob", $expire);
?>

<html>
.....
```

在上面的实例中，过期时间被设置为一个月（*60 秒 \* 60 分 * 24 小时 * 30 天*）。

------

## 如何取回 Cookie 的值？

PHP 的 `$_COOKIE` 变量用于取回 cookie 的值。

在下面的实例中，取回了名为 "user" 的 cookie 的值，并把它显示在了页面上：

```php
<?php
// 输出 cookie 值
echo $_COOKIE["user"];

// 查看所有 cookie
print_r($_COOKIE);
?>
```

在下面的实例中，使用 `isset()` 函数来确认是否已设置了 cookie：

```php+HTML
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<?php
if (isset($_COOKIE["user"]))
    echo "欢迎 " . $_COOKIE["user"] . "!<br>";
else
    echo "普通访客!<br>";
?>

</body>
</html>
```

 

------

## 如何删除 Cookie？

当删除 cookie 时，应当使过期日期变更为过去的时间点。

删除的实例：

```php
<?php
// 设置 cookie 过期时间为过去 1 小时
setcookie("user", "", time()-3600);
?>
```

 

------

## 如果浏览器不支持 Cookie 该怎么办？

如果应用程序需要与不支持 cookie 的浏览器打交道，那么不得不使用其他的办法在应用程序中的页面之间传递信息。一种方式是通过表单传递数据。

下面的表单在用户单点击 "Submit" 按钮时，向 "welcome.php" 提交了用户输入：

```html
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<form action="welcome.php" method="post">
名字: <input type="text" name="name">
年龄: <input type="text" name="age">
<input type="submit">
</form>

</body>
</html>
```

取回 "welcome.php" 文件中的值，如下所示：

```php+HTML
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

欢迎 <?php echo $_POST["name"]; ?>.<br>
你 <?php echo $_POST["age"]; ?> 岁了。

</body>
</html>
```