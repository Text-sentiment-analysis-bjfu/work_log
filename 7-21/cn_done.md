
## 在本地进行WordPress开发调试

### [相关代码](https://github.com/cnyy7/wordpress_learing "相关代码") 

## PHP学习 ##
#### [参考链接](http://www.runoob.com/php/php-tutorial.html "PHP 教程") ####

## PHP MySQL Where 子句 ##
`WHERE` 子句用于提取满足指定标准的的记录。

- 语法
		 
		SELECT column_name(s)
		FROM table_name
		WHERE column_name operator value

为了让 PHP 执行上面的语句，必须使用 `mysqli_query()` 函数。该函数用于向 MySQL 连接发送查询或命令。

下面的实例将从 `Persons` 表中选取所有 `FirstName='Peter'` 的行：

	<?php
	$con=mysqli_connect("localhost","username","password","database");
	// 检测连接
	if (mysqli_connect_errno())
	{
	    echo "连接失败: " . mysqli_connect_error();
	}
	
	$result = mysqli_query($con,"SELECT * FROM Persons
	WHERE FirstName='Peter'");
	
	while($row = mysqli_fetch_array($result))
	{
	    echo $row['FirstName'] . " " . $row['LastName'];
	    echo "<br>";
	}
	?>

以上代码将输出：

	Peter Griffin

## PHP MySQL Order By 关键词 ##

`ORDER BY `关键词用于对记录集中的数据进行排序。

`ORDER BY` 关键词默认对记录进行升序排序。

如果要进行降序排序，要使用 `DESC` 关键字。

- 语法
		
		SELECT column_name(s)
		FROM table_name
		ORDER BY column_name(s) ASC|DESC

下面的实例选取 `Persons` 表中存储的所有数据，并根据 `Age` 列对结果进行排序：

	<?php
	$con=mysqli_connect("localhost","username","password","database");
	// 检测连接
	if (mysqli_connect_errno())
	{
	    echo "连接失败: " . mysqli_connect_error();
	}
	
	$result = mysqli_query($con,"SELECT * FROM Persons ORDER BY age");
	
	while($row = mysqli_fetch_array($result))
	{
	    echo $row['FirstName'];
	    echo " " . $row['LastName'];
	    echo " " . $row['Age'];
	    echo "<br>";
	}
	
	mysqli_close($con);
	?>
以上结果将输出：
	
	Glenn Quagmire 33
	Peter Griffin 35

#### 根据两列进行排序 ####
可以根据多个列进行排序。当按照多个列进行排序时，只有第一列的值相同时才使用第二列：
	
	SELECT column_name(s)
	FROM table_name
	ORDER BY column1, column2
## PHP MySQL Update ##
更新数据库中的数据

`UPDATE` 语句用于更新数据库表中已存在的记录。

- 语法
 
 		UPDATE table_name
		SET column1=value, column2=value2,...
		WHERE some_column=some_value

**注意： `UPDATE` 语法中的 `WHERE` 子句。`WHERE` 子句规定了哪些记录需要更新。如果省去 WHERE 子句，所有的记录都会被更新！**

假如一个名为 `Persons` 的表，如下所示：

|FirstName|	LastName|	Age  |
|:------  |:------  |:------:|
|Peter    |Griffin  |	35   |
|Glenn    |Quagmire |33      |

下面的例子更新 `Persons` 表的一些数据：

		<?php
		$con=mysqli_connect("localhost","username","password","database");
		// 检测连接
		if (mysqli_connect_errno())
		{
		    echo "连接失败: " . mysqli_connect_error();
		}
		
		mysqli_query($con,"UPDATE Persons SET Age=36
		WHERE FirstName='Peter' AND LastName='Griffin'");
		
		mysqli_close($con);
		?>

在这次更新后，`Persons` 表如下所示：

|FirstName|	LastName|	Age  |
|:------  |:------  |:------:|
|Peter    |Griffin  |	36   |
|Glenn    |Quagmire |   33   |

## PHP MySQL Delete ##
删除数据库中的数据

`DELETE FROM `语句用于从数据库表中删除记录。

- 语法
	
		DELETE FROM table_name
		WHERE some_column = some_value

**注意: `DELETE` 语法中的 `WHERE` 子句规定了哪些记录需要删除。如果省去 `WHERE` 子句，所有的记录都会被删除！**

假如一个名为 "Persons" 的表，如下所示：

|FirstName|	LastName|	Age  |
|:------  |:------  |:------:|
|Peter    |Griffin  |	35   |
|Glenn    |Quagmire |33      |
下面的实例删除 `Persons` 表中所有 `LastName='Griffin'` 的记录：

	<?php
	$con=mysqli_connect("localhost","username","password","database");
	// 检测连接
	if (mysqli_connect_errno())
	{
	    echo "连接失败: " . mysqli_connect_error();
	}
	
	mysqli_query($con,"DELETE FROM Persons WHERE LastName='Griffin'");
	
	mysqli_close($con);
	?>

删除后，`Persons` 表如下所示：

|FirstName|	LastName|	Age  |
|:------  |:------  |:------:|
|Glenn    |Quagmire |33      |