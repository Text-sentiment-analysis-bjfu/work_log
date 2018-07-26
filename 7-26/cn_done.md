## PHP - AJAX 与 MySQL ##
AJAX 可用来与数据库进行交互式通信。

### AJAX 数据库实例 ###
下面的实例将演示网页如何通过 AJAX 从数据库读取信息：
![](http://i4.bvimg.com/602998/93219520f65683d4.png)
### 实例解释 - MySQL 数据库 ###
在上面的实例中，使用的数据库表如下所示：

	mysql> select * from websites;
	+----+--------------+---------------------------+-------+---------+
	| id | name         | url                       | alexa | country |
	+----+--------------+---------------------------+-------+---------+
	| 1  | Google       | https://www.google.cm/    | 1     | USA     |
	| 2  | 淘宝       | https://www.taobao.com/   | 13    | CN      |
	| 3  | 菜鸟教程 | http://www.runoob.com/    | 4689  | CN      |
	| 4  | 微博       | http://weibo.com/         | 20    | CN      |
	| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
	+----+--------------+---------------------------+-------+---------+
	5 rows in set (0.01 sec)
### 实例解释 - HTML 页面 ###
当用户在上面的下拉列表中选择某位用户时，会执行名为 `showSite()` 的函数。该函数由 `onchange` 事件触发：

	<!DOCTYPE html> 
	<html> 
	<head> 
	<meta charset="utf-8"> 
	<title>菜鸟教程(runoob.com)</title> 
	<script>
	function showSite(str)
	{
	    if (str=="")
	    {
	        document.getElementById("txtHint").innerHTML="";
	        return;
	    } 
	    if (window.XMLHttpRequest)
	    {
	        // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
	        xmlhttp=new XMLHttpRequest();
	    }
	    else
	    {
	        // IE6, IE5 浏览器执行代码
	        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	    }
	    xmlhttp.onreadystatechange=function()
	    {
	        if (xmlhttp.readyState==4 && xmlhttp.status==200)
	        {
	            document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
	        }
	    }
	    xmlhttp.open("GET","getsite_mysql.php?q="+str,true);
	    xmlhttp.send();
	}
	</script>
	</head>
	<body>
	 
	<form>
	<select name="users" onchange="showSite(this.value)">
	<option value="">选择一个网站:</option>
	<option value="1">Google</option>
	<option value="2">淘宝</option>
	<option value="3">菜鸟教程</option>
	<option value="4">微博</option>
	<option value="5">Facebook</option>
	</select>
	</form>
	<br>
	<div id="txtHint"><b>网站信息显示在这里……</b></div>
	 
	</body>
	</html>

`showSite()` 函数会执行以下步骤：

检查是否有网站被选择

- 创建 XMLHttpRequest 对象

- 创建在服务器响应就绪时执行的函数

- 向服务器上的文件发送请求

- 请注意添加到 URL 末端的参数（q）（包含下拉列表的内容）

### PHP 文件 ###
上面这段通过 JavaScript 调用的服务器页面是名为 `getsite_mysql.php` 的 PHP 文件。

`getsite_mysql.php` 中的源代码会运行一次针对 MySQL 数据库的查询，然后在 HTML 表格中返回结果：

	<?php
	$q = isset($_GET["q"]) ? intval($_GET["q"]) : '';
	 
	if(empty($q)) {
	    echo '请选择一个网站';
	    exit;
	}
	 
	$con = mysqli_connect('localhost','root','123456');
	if (!$con)
	{
	    die('Could not connect: ' . mysqli_error($con));
	}
	// 选择数据库
	mysqli_select_db($con,"test");
	// 设置编码，防止中文乱码
	mysqli_set_charset($con, "utf8");
	 
	$sql="SELECT * FROM Websites WHERE id = '".$q."'";
	 
	$result = mysqli_query($con,$sql);
	 
	echo "<table border='1'>
	<tr>
	<th>ID</th>
	<th>网站名</th>
	<th>网站 URL</th>
	<th>Alexa 排名</th>
	<th>国家</th>
	</tr>";
	 
	while($row = mysqli_fetch_array($result))
	{
	    echo "<tr>";
	    echo "<td>" . $row['id'] . "</td>";
	    echo "<td>" . $row['name'] . "</td>";
	    echo "<td>" . $row['url'] . "</td>";
	    echo "<td>" . $row['alexa'] . "</td>";
	    echo "<td>" . $row['country'] . "</td>";
	    echo "</tr>";
	}
	echo "</table>";
	 
	mysqli_close($con);
	?>

**解释：**当查询从 JavaScript 发送到 PHP 文件时，将发生：

1. PHP 打开一个到 MySQL 数据库的连接

1. 找到选中的用户

1. 创建 HTML 表格，填充数据，并发送回 "txtHint" 占位符