
## AJAX ##
- AJAX = Asynchronous JavaScript and XML.

- AJAX 是一种用于创建快速动态网页的技术。

- AJAX 通过在后台与服务器进行少量数据交换，使网页实现异步更新。这意味着可以在不重载整个页面的情况下，对网页的某些部分进行更新。

- 传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个页面。

- 有很多使用 AJAX 的应用程序案例：Google Maps、Gmail、Youtube 和 Facebook。
## AJAX 如何工作 ##

![](http://i2.bvimg.com/602998/91f58efadac33f92.gif)

### AJAX 基于因特网标准 ###
AJAX 基于因特网标准，并使用以下技术组合：

- XMLHttpRequest 对象（与服务器异步交互数据）

- JavaScript/DOM（显示/取回信息）

- CSS（设置数据的样式）

- XML（常用作数据传输的格式）

**AJAX 应用程序与浏览器和平台无关的！**

## AJAX PHP 实例 ##

下面的实例将演示当用户在输入框中键入字符时，网页如何与 Web 服务器进行通信：
![](http://i2.bvimg.com/602998/17eee7a6eb159d64.png)

HTML 页面如下

当用户在上面的输入框中键入字符时，会执行 "showHint()" 函数。该函数由 "onkeyup" 事件触发：

	<html>
	<head>
	<script>
	function showHint(str)
	{
	    if (str.length==0)
	    { 
	        document.getElementById("txtHint").innerHTML="";
	        return;
	    }
	    if (window.XMLHttpRequest)
	    {
	        // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行的代码
	        xmlhttp=new XMLHttpRequest();
	    }
	    else
	    {    
	        //IE6, IE5 浏览器执行的代码
	        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	    }
	    xmlhttp.onreadystatechange=function()
	    {
	        if (xmlhttp.readyState==4 && xmlhttp.status==200)
	        {
	            document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
	        }
	    }
	    xmlhttp.open("GET","gethint.php?q="+str,true);
	    xmlhttp.send();
	}
	</script>
	</head>
	<body>
	
	<p><b>在输入框中输入一个姓名:</b></p>
	<form> 
	姓名: <input type="text" onkeyup="showHint(this.value)">
	</form>
	<p>返回值: <span id="txtHint"></span></p>
	
	</body>
	</html>

源代码解释：

如果输入框是空的（`str.length==0`），该函数会清空 txtHint 占位符的内容，并退出该函数。

如果输入框不是空的，那么 `showHint()` 会执行以下步骤：

- 创建 `XMLHttpRequest` 对象

- 创建在服务器响应就绪时执行的函数

- 向服务器上的文件发送请求

- 请注意添加到 URL 末端的参数（q）（包含输入框的内容）


### PHP 文件 ###
----
上面这段通过 JavaScript 调用的服务器页面是名为 "gethint.php" 的 PHP 文件。

"gethint.php" 中的源代码会检查姓名数组，然后向浏览器返回对应的姓名：

	<?php
	// 将姓名填充到数组中
	$a[]="Anna";
	$a[]="Brittany";
	$a[]="Cinderella";
	$a[]="Diana";
	$a[]="Eva";
	$a[]="Fiona";
	$a[]="Gunda";
	$a[]="Hege";
	$a[]="Inga";
	$a[]="Johanna";
	$a[]="Kitty";
	$a[]="Linda";
	$a[]="Nina";
	$a[]="Ophelia";
	$a[]="Petunia";
	$a[]="Amanda";
	$a[]="Raquel";
	$a[]="Cindy";
	$a[]="Doris";
	$a[]="Eve";
	$a[]="Evita";
	$a[]="Sunniva";
	$a[]="Tove";
	$a[]="Unni";
	$a[]="Violet";
	$a[]="Liza";
	$a[]="Elizabeth";
	$a[]="Ellen";
	$a[]="Wenche";
	$a[]="Vicky";
	
	//从请求URL地址中获取 q 参数
	$q=$_GET["q"];
	
	//查找是否由匹配值， 如果 q>0
	if (strlen($q) > 0)
	{
	    $hint="";
	    for($i=0; $i<count($a); $i++)
	    {
	        if (strtolower($q)==strtolower(substr($a[$i],0,strlen($q))))
	        {
	            if ($hint=="")
	            {
	                $hint=$a[$i];
	            }
	            else
	            {
	                $hint=$hint." , ".$a[$i];
	            }
	        }
	    }
	}
	
	// 如果没有匹配值设置输出为 "no suggestion" 
	if ($hint == "")
	{
	    $response="no suggestion";
	}
	else
	{
	    $response=$hint;
	}
	
	//输出返回值
	echo $response;
	?>
**解释：**如果 JavaScript 发送了任何文本（即 strlen($q) > 0），则会发生：

1. 查找匹配 JavaScript 发送的字符的姓名

1. 如果未找到匹配，则将响应字符串设置为 "no suggestion"

1. 如果找到一个或多个匹配姓名，则用所有姓名设置响应字符串

1. 把响应发送到 "txtHint" 占位符