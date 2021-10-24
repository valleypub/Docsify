[toc]


# ADO.NET
- 是什么



- 根据将要访问的数据库类型，.NET Framework包含了两个数据提供程序，如下所示：
	1. __OLE DB.NET数据库提供程序__ 
		- 用于访问任何与OLE DB兼容的数据库。
		- OLE DB .NET数据提供程序类位于System.Data.OleDb命名空间中
	2. __SQL Server.NET数据库提供程序 __
		- 用于访问SQL Server 7或者更高版本的数据库。
		- SQL Server .NET数据提供程序类位于System.Data.SqlClient命名空间中
	3. 每个数据库提供程序都实现了以下的类，它们构成了提供程序的核心：
		- Connection 用于建立到数据库的连接。
		- Command 用于执行对数据库的命令。
		- DataReader 用于访问一个只向前的、只读窗体中的数据。
		- DataAdapter 用于访问一个读/写窗体中的数据，并管理数据的更新。
		- ![](C:\Users\king-kong\Desktop\BlogPlan\picture\C#\C#操作数据库\两种数据库的核心接入类.PNG)


- ADO.NET模型的步骤：
	1. 创建一个连接
	2. 准备并执行一个命令
	3. 处理检索到的数据

### ADO.NET模型的详细步骤
#### SQL Server .NET版的
##### 连接到数据源
- 表示与SQL Server的物理连接的类是SqlConnection，它位于System.Data.SqlClient命名空间

- SqlConnection类的属性||方法
	- 属性区
		- ![]()
		- 注意：除了ConnectionString外，其他都是只读属性。
	- 方法区
		- ![]()

- SqlConnection类的常见工作模式
```c#
string connString = "SERVER=…;DATABASE=…;UID=…;PWD=…";￼   SqlConnection conn = new SqlConnection(connString);￼    
conn.Open();￼    
…￼
conn.Close();
```


#### OLE DB .NET版的