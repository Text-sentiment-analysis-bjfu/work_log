## AJAX 与 XML ##
AJAX 可用来与 XML 文件进行交互式通信。

下面的实例将演示网页如何通过 AJAX 从 XML 文件读取信息：
<html>
<head>

</head>
<body>

<form>
Select a CD:
<select name="cds" onchange="showCD(this.value)">
<option value="">Select a CD:</option>
<option value="Bob Dylan">Bob Dylan</option>
<option value="Bonnie Tyler">Bonnie Tyler</option>
<option value="Dolly Parton">Dolly Parton</option>
</select>
</form>
<div id="txtHint"><b>CD info will be listed here...</b></div>

</body>
</html>
![](http://i4.bvimg.com/602998/be5f2f089efdbf51.png)
#### 实例解释 - HTML 页面 ####
当用户在上面的下拉列表中选择某张 CD 时，会执行名为 "showCD()" 的函数。该函数由 "onchange" 事件触发：

	<html>
	<head>
	<script>
	function showCD(str)
	{
	    if (str=="")
	    {
	        document.getElementById("txtHint").innerHTML="";
	        return;
	    } 
	    if (window.XMLHttpRequest)
	    {
	        // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行
	        xmlhttp=new XMLHttpRequest();
	    }
	    else
	    {
	        // IE6, IE5 浏览器执行
	        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	    }
	    xmlhttp.onreadystatechange=function()
	    {
	        if (xmlhttp.readyState==4 && xmlhttp.status==200)
	        {
	            document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
	        }
	    }
	    xmlhttp.open("GET","getcd.php?q="+str,true);
	    xmlhttp.send();
	}
	</script>
	</head>
	<body>
	
	<form>
	Select a CD:
	<select name="cds" onchange="showCD(this.value)">
	<option value="">Select a CD:</option>
	<option value="Bob Dylan">Bob Dylan</option>
	<option value="Bonnie Tyler">Bonnie Tyler</option>
	<option value="Dolly Parton">Dolly Parton</option>
	</select>
	</form>
	<div id="txtHint"><b>CD info will be listed here...</b></div>
	
	</body>
	</html>

showCD() 函数会执行以下步骤：

- 检查是否有 CD 被选择

- 创建 XMLHttpRequest 对象

- 创建在服务器响应就绪时执行的函数

- 向服务器上的文件发送请求

- 请注意添加到 URL 末端的参数（q）（包含下拉列表的内容）

### PHP文件 ###
上面这段通过 JavaScript 调用的服务器页面是名为 "getcd.php" 的 PHP 文件。

PHP 脚本加载 XML 文档，"[cd_catalog.xml](http://www.runoob.com/try/demo_source/cd_catalog.xml)"，运行针对 XML 文件的查询，并以 HTML 返回结果：

	<?php
	$q=$_GET["q"];
	
	$xmlDoc = new DOMDocument();
	$xmlDoc->load("cd_catalog.xml");
	
	$x=$xmlDoc->getElementsByTagName('ARTIST');
	
	for ($i=0; $i<=$x->length-1; $i++)
	{
	    // 处理元素节点
	    if ($x->item($i)->nodeType==1)
	    {
	        if ($x->item($i)->childNodes->item(0)->nodeValue == $q)
	        {
	            $y=($x->item($i)->parentNode);
	        }
	    }
	}
	
	$cd=($y->childNodes);
	
	for ($i=0;$i<$cd->length;$i++)
	{ 
	    // 处理元素节点
	    if ($cd->item($i)->nodeType==1)
	    {
	        echo("<b>" . $cd->item($i)->nodeName . ":</b> ");
	        echo($cd->item($i)->childNodes->item(0)->nodeValue);
	        echo("<br>");
	    }
	}
	?>

当 CD 查询从 JavaScript 发送到 PHP 页面时，将发生：

1. PHP 创建 XML DOM 对象
1. 查找所有 <artist> 元素中与 JavaScript 所传数据相匹配的名字
1. 输出 album 的信息，并发送回 "txtHint" 占位符