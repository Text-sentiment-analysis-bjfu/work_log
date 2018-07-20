
## 在本地进行WordPress开发调试

### [相关代码](https://github.com/cnyy7/wordpress_learing "相关代码") 

## PHP学习 ##
#### [参考链接](http://www.runoob.com/php/php-tutorial.html "PHP 教程") ####

## PHP 创建 MySQL 表 ##
`CREATE TABLE` 语句用于创建 MySQL 表。

创建表前，需要使用 `use myDB` 来选择要操作的数据库：

	use myDB;
创建一个名为 `"MyGuests"` 的表，有 5 个列：` "id"`, `"firstname"`, `"lastname"`, `"email"` 和 `"reg_date"`:

    CREATE TABLE MyGuests (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    firstname VARCHAR(30) NOT NULL,
    lastname VARCHAR(30) NOT NULL,
    email VARCHAR(50),
    reg_date TIMESTAMP
    )


> 数据类型指定列可以存储什么类型的数据。完整的数据类型请参考[数据类型参考手册](http://www.runoob.com/sql/sql-datatypes.html)。

在设置了数据类型后，可以为每个列指定其他选项的属性：

- NOT NULL - 每一行都必须含有值（不能为空），null 值是不允许的。

- DEFAULT value - 设置默认值

- UNSIGNED - 使用无符号数值类型，0 及正数

- AUTO INCREMENT - 设置 MySQL 字段的值在新增记录时每次自动增长 1

- PRIMARY KEY - 设置数据表中每条记录的唯一标识。 通常列的 PRIMARY KEY 设置为 ID 数值，与 AUTO_INCREMENT 一起使用。

> 每个表都应该有一个主键(本列为 "id" 列)，主键必须包含唯一的值。

	<?php
	$servername = "localhost";
	$username = "username";
	$password = "password";
	$dbname = "myDB";
	
	// 创建连接
	$conn = new mysqli($servername, $username, $password, $dbname);
	// 检测连接
	if ($conn->connect_error) {
	    die("连接失败: " . $conn->connect_error);
	} 
	
	// 使用 sql 创建数据表
	$sql = "CREATE TABLE MyGuests (
	id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
	firstname VARCHAR(30) NOT NULL,
	lastname VARCHAR(30) NOT NULL,
	email VARCHAR(50),
	reg_date TIMESTAMP
	)";
	
	if ($conn->query($sql) === TRUE) {
	    echo "Table MyGuests created successfully";
	} else {
	    echo "创建数据表错误: " . $conn->error;
	}
	
	$conn->close();
	?>
## PHP MySQL 插入数据 ##
以下为一些语法规则：



- PHP 中 SQL 查询语句必须使用引号


- 在 SQL 查询语句中的字符串值必须加引号


- 数值的值不需要引号


- NULL 值不需要引号

INSERT INTO 语句通常用于向 MySQL 表添加新的记录：
    
	INSERT INTO table_name (column1, column2, column3,...)
	VALUES (value1, value2, value3,...)
假如有表 `"MyGuests"`，表字段有: `"id"`, `"firstname"`, `"lastname"`, `"email"` 和 `"reg_date"`。 现在，开始向表填充数据。

	<?php
	$servername = "localhost";
	$username = "username";
	$password = "password";
	$dbname = "myDB";
	
	// 创建连接
	$conn = new mysqli($servername, $username, $password, $dbname);
	// 检测连接
	if ($conn->connect_error) {
	    die("连接失败: " . $conn->connect_error);
	} 
	
	$sql = "INSERT INTO MyGuests (firstname, lastname, email)
	VALUES ('John', 'Doe', 'john@example.com')";
	
	if ($conn->query($sql) === TRUE) {
	    echo "新记录插入成功";
	} else {
	    echo "Error: " . $sql . "<br>" . $conn->error;
	}
	
	$conn->close();
	?>
## PHP MySQL 预处理语句 ##
预处理语句及绑定参数
预处理语句用于执行多个相同的 SQL 语句，并且执行效率更高。

预处理语句的工作原理如下：

1. 预处理：创建 SQL 语句模板并发送到数据库。预留的值使用参数 "?" 标记 。例如：

		INSERT INTO MyGuests (firstname, lastname, email) VALUES(?, ?, ?)
1. 数据库解析，编译，对SQL语句模板执行查询优化，并存储结果不输出。

2. 执行：最后，将应用绑定的值传递给参数（"?" 标记），数据库执行语句。应用可以多次执行语句，如果参数的值不一样。

相比于直接执行SQL语句，预处理语句有两个主要优点：

- 预处理语句大大减少了分析时间，只做了一次查询（虽然语句多次执行）。

- 绑定参数减少了服务器带宽，你只需要发送查询的参数，而不是整个语句。
 
以下是一个实例

	<?php
	$servername = "localhost";
	$username = "username";
	$password = "password";
	$dbname = "myDB";
	 
	// 创建连接
	$conn = new mysqli($servername, $username, $password, $dbname);
	 
	// 检测连接
	if ($conn->connect_error) {
	    die("连接失败: " . $conn->connect_error);
	}
	 
	// 预处理及绑定
	$stmt = $conn->prepare("INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)");
	$stmt->bind_param("sss", $firstname, $lastname, $email);
	 
	// 设置参数并执行
	$firstname = "John";
	$lastname = "Doe";
	$email = "john@example.com";
	$stmt->execute();
	 
	$firstname = "Mary";
	$lastname = "Moe";
	$email = "mary@example.com";
	$stmt->execute();
	 
	$firstname = "Julie";
	$lastname = "Dooley";
	$email = "julie@example.com";
	$stmt->execute();
	 
	echo "新记录插入成功";
	 
	$stmt->close();
	$conn->close();
	?>
来看下 bind_param() 函数：

	$stmt->bind_param("sss", $firstname, $lastname, $email);
该函数绑定了 SQL 的参数，且告诉数据库参数的值。 "sss" 参数列处理其余参数的数据类型。s 字符告诉数据库该参数为字符串。

参数有以下四种类型:

1. i - integer（整型）

1. d - double（双精度浮点型）

1. s - string（字符串）

1. b - BLOB（binary large object:二进制大对象）

每个参数都需要指定类型。
## PHP MySQL 读取数据 ##
SELECT 语句用于从数据表中读取数据:

	SELECT column_name(s) FROM table_name
使用 * 号来读取所有数据表中的字段：

	SELECT * FROM table_name
以下实例中从 `myDB` 数据库的 `MyGuests` 表读取了 `id`, `firstname` 和 `lastname` 列的数据并显示在页面上：

	<?php
	$servername = "localhost";
	$username = "username";
	$password = "password";
	$dbname = "myDB";
	 
	// 创建连接
	$conn = new mysqli($servername, $username, $password, $dbname);
	// Check connection
	if ($conn->connect_error) {
	    die("连接失败: " . $conn->connect_error);
	} 
	 
	$sql = "SELECT id, firstname, lastname FROM MyGuests";
	$result = $conn->query($sql);
	 
	if ($result->num_rows > 0) {
	    // 输出数据
	    while($row = $result->fetch_assoc()) {
	        echo "id: " . $row["id"]. " - Name: " . $row["firstname"]. " " . $row["lastname"]. "<br>";
	    }
	} else {
	    echo "0 结果";
	}
	$conn->close();
	?>
以上代码解析如下:

>首先，设置了 SQL 语句从` MyGuests`数据表中读取 `id`, `firstname` 和 `lastname` 三个字段。之后使用该 SQL 语句从数据库中取出结果集并赋给复制给变量 `$result`。

>函数 `num_rows() `判断返回的数据。

>如果返回的是多条数据，函数 `fetch_assoc()` 将结合集放入到关联数组并循环输出。 `while()` 循环出结果集，并输出 `id`, `firstname` 和 `lastname` 三个字段值。