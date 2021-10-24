[toc]



# IO
## IO部分
### 按类分
#### System.Console
- 是什么
	1. 静态类
	2. 不可被继承。why 不直接写成sealed封闭类？？
##### 输入
1. Console.ReadKey()
	- 作用：
		- 读取单个字符。可用来实现按任意键继续功能
	- 返回值类型：
		- 
2. Console.Read()
	- 作用：
		- 读取单个字符
	- 返回值类型：
		- 输入的字符作为int型返回，所以要显示字符需要进行类型转换为char。
3. Console.ReadLine()
	- 作用：
		- 读取一串字符，直到用户按下回车键
	- 返回值类型
		- 输入的一串字符存储到一个string类型对象中并返回

##### 输出
1. Console.Write()
	- 作用
		- 字符输出完后，光标不会自动移到下一行，而是在输出字符串的最后一个字符后
2. Console.WriteLine()
	- 作用
		- 将输出流输出到指定设备。默认输出到屏幕，
		- 字符输出完后，光标会自动移到下一行

3. Console.Beep()
	- 作用
		- 输出一个"哔"的音

4. Console.Clear()


#### System.IO命名空间
- 这里面





### 按使用方式分
#### 流&文件IO
- System.IO中的类

#### 设备IO
- System.Console



## 文件系统

### 文件|文件夹common的操作
#### 创建
##### 文件的创建
1. 使用File方式

##### 文件夹的创建



#### 删除
##### 文件的删除
1. 使用File静态类
2. 使用FileInfo类

##### 文件夹的删除
1. 使用Directory静态类来删除
- System.IO.Directory.Delete(@"C:\Users\Public\DeleteTest", true);

2. 使用DirectoryInfo来删除，因为是非静态类故要先实例化才能使用方法
```
    System.IO.DirectoryInfo di = new System.IO.DirectoryInfo(@"C:\Users\public");
    try
    {
    	di.Delete(true);
    }
    catch (System.IO.IOException e)
    {
    	Console.WriteLine(e.Message);
    }
```

#### 复制

#### 移动

#### 操作进度对话框
通过在C#中引用Microsoft.VisualBasic 命名空间，使用Microsoft.VisualBasic提供的 CopyFile(String, String, UIOption) ，FileSystem.CopyDirectory();这两个方法是自带进度提示的




### 文件专有的操作
#### 从文件读取
##### 按行读取
#### 写入文件
##### 按流的方式

##### 非流的方式


1. 按Line ----即一个string[]（每个元素代表一行） 的方式来写
```c#
using System.IO;
using System.Threading.Tasks;

class WriteAllLines
{
    public static async Task ExampleAsync()
    {
        string[] lines =
        {
            "First line", "Second line", "Third line" 
        };

        await File.WriteAllLinesAsync("WriteLines.txt", lines);
    }
}
```

2. 按Text -- 即一整个string的方式写
	- 

```
using System.IO;
using System.Threading.Tasks;

class WriteAllText
{
    public static async Task ExampleAsync()
    {
        string text =
            "A class is the most powerful data type in C#. Like a structure, " +
            "a class defines the data and behavior of the data type. ";

        await File.WriteAllTextAsync("WriteText.txt", text);
    }
}
```



### 目录专有的操作
#### 循环访问目录树
- 是什么
	- 可以以 string 的形式只检索文件或子目录的名称，也可以以 System.IO.FileInfo 或 System.IO.DirectoryInfo 对象的形式检索其他信息
		- ==如果必须在内存或磁盘上存储目录树的内容，那么最佳选择是仅存储每个文件or目录的 FullName 属性（类型为 string）==。 将这个FullName作为操作入口，然后可以根据需要使用此字符串创建新的 FileInfo 或 DirectoryInfo 对象，或打开需要进行其他处理的任何文件


- how
	- 自动检索: GetDirectories() + System.IO.SearchOption.AllDirectories标志位
		- 使用方式：
			- root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories)；此标志返回与指定的模式匹配的所有嵌套的子目录
		- 优点：
			- __如果你确信拥有指定根目录下的所有目录的访问权限__，此方式最简单
		- 缺点：
			- 如果指定根目录下的任何子目录引发 DirectoryNotFoundException 或 UnauthorizedAccessException 异常，则整个方法失败且__不返回任何目录__。使用 GetFiles 方法时也是如此
	- 手动检索
		- 使用递归遍历
			- 优点：
				- 
			- 缺点：
				- 如果目录树较大且嵌套深度较深，则可能引起堆栈溢出异常
		- 基于堆栈的遍历


### NTFS

https://docs.microsoft.com/zh-cn/windows-server/storage/file-server/ntfs-overview

NTFS 文件系统可以包含交接点、符号链接和硬链接等形式的重解析点。 诸如 GetFiles 和 GetDirectories 等 .NET 方法不会返回重分析点下的任何子目录。 当两个重解析点相互引用时，此行为可防止进入无限循环。 通常，处理重解析点时应格外小心，以确保不会无意中修改或删除文件。 如果需要精确控制重解析点，请使用平台调用或本机代码直接调用相应的 Win32 文件系统方法。



### 常用文件操作的类实现
- 将一些对文件的常用操作(如：遍历获取整个目录的FullName、...  、)封装为一个静态类
```

```



### 文件相关类的常用组合
- System.IO命名空间中的文件操作相关的类一般分为以下几类：
	- System.IO.Directory|System.IO.File两个静态类 
	- System.IO.FileInfo|System.IO.DirectoryInfo|System.IO.DriveInfo，常用于以下几种情况：
		1. 用来访问文件系统信息
		2. 通过将表示文件、文件夹或驱动器名称的字符串传入构造函数来创建这些类的实例
		3. 它们还包含用于打开、关闭、移动和删除文件和文件夹的方法
			- 不过由于这些方法的使用需要先new一个类的实例才能用，故不如System.IO.Directory|System.IO.File中的相应的静态方法用着方便，一般这些操作使用System.IO.Directory|System.IO.File
	- System.IO.Path
		- 以==跨平台==的方式对包含文件或目录路径信息的 String 实例执行操作。
		- 使用Path的好处：简单、不宜错
			- 不使用Path的：
				- string pathString2 = @"c:\Top-Level Folder\SubFolder2";
			- 使用Path的：
				- string pathString = System.IO.Path.Combine(@"c:\Top-Level Folder", "SubFolder");
	- System.IO.FileSystemInfo
		- 一般只用作System.IO.FileInfo|System.IO.DirectoryInfo的入口，配合 ==as运算符== + ==(fsi.Attributes & FileAttributes.Directory) == FileAttributes.Directory判断语句== 来使用。因为System.IO.FileSystemInfo类型变量指向的可能是FileInfo实体 or DirectoryInfo实体，在使用前需要判断是文件 or 目录 -> 再使用 as运算符 进行权限升级
		- 


#### System.IO.Directory
- GetDirectories(".")
- GetFiles(".")
- GetCurrentDirectory()
	- 此正在运行的应用程序.exe所在的目录
- SetCurrentDirectory(@"C:\Users\Public\TestFolder\")
- CreateDirectory(@"C:\Users\Public\TestFolder\");
	- 根据string型的FullName(绝对路径)来创建一个目录出来
- Exists(@"C:\Users\Public\TestFolder\"))
	- 根据string型的FullName来判断目录存不存在
	- 如果应用程序没有足够权限来读取指定文件，Exists 方法会返回 false（无论路径是否存在）；该方法不会引发异常。

- System.IO.Directory.Move(@"C:\Users\Public\public\test\", @"C:\Users\Public\private");

- System.IO.Directory.Delete(@"C:\Users\Public\DeleteTest");


#### System.IO.File

1. System.IO.File.Exists(pathString)
2. System.IO.FileStream fs = System.IO.File.Create(pathString)
	- 如果文件夹已存在，CreateDirectory 不执行任何操作，未引发任何异常。 但 File.Create 用新文件替换现有文件。
		- File.Create 需配合 File.Exists() -> 阻止替换现有文件
3. byte[] readBuffer = System.IO.File.ReadAllBytes(pathString);

4. System.IO.File.Copy(sourceFile, destFile, true);
	- overwrite the destination file if it already exists.
5. System.IO.File.Move(@"C:\test.txt", @"C:\Users\test.txt");
	- 如果目的文件已存在会override吗？？

6. System.IO.File.Delete(@"C:\Users\Public\DeleteTest\test.txt");

7. string text = System.IO.File.ReadAllText(@"C:\Users\Public\TestFolder\WriteText.txt");

string[] lines = System.IO.File.ReadAllLines(@"C:\Users\Public\TestFolder\WriteLines2.txt");

await File.WriteAllTextAsync("WriteText.txt", text);

await File.WriteAllLinesAsync("WriteLines.txt", lines);


#### System.IO.FileInfo


#### System.IO.DirectoryInfo


#### System.IO.DriveInfo
1. System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");



#### System.IO.Path
1. string pathString = System.IO.Path.Combine(@"c:\Top-Level Folder", "SubFolder");
2. string fileName = System.IO.Path.GetRandomFileName();





# 类型转换

### 按类来
#### System.Convert

#### System.Text命名空间


# 字符串处理
## C#中的字符串相关类
### StringBuilder
- 是什么

- why need it(有了string还不够？？？)

- how use it
	1. 命名空间
		- System.Text


### String
## 字符串常用操作
### 字符串内插
https://docs.microsoft.com/zh-cn/dotnet/csharp/tutorials/exploration/interpolated-strings
### 确定字符串是否表示数字
https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value

### 比较字符串
https://docs.microsoft.com/zh-cn/dotnet/csharp/how-to/compare-strings
### 修改字符串内容
https://docs.microsoft.com/zh-cn/dotnet/csharp/how-to/modify-string-contents
### 使用 String.Split 分隔字符串
https://docs.microsoft.com/zh-cn/dotnet/csharp/how-to/parse-strings-using-split
### 将多个字符串合并为一个字符串
https://docs.microsoft.com/zh-cn/dotnet/csharp/how-to/concatenate-multiple-strings
### 在字符串中搜索文本
https://docs.microsoft.com/zh-cn/dotnet/csharp/how-to/search-strings

