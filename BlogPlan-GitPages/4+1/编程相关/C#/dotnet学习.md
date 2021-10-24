[toc]

# .NET相对JAVA的优势
[.NET SDK 官方下载网页](https://dotnet.microsoft.com/download)

- .NET is free. There are no fees or licensing costs, including for commercial use.
- .NET is open-source and cross-platform, with free development tools for Windows, Linux, and macOS.
- .NET is supported by Microsoft. Microsoft ships official releases that are built and tested on Microsoft-maintained servers in Azure and supported just like any Microsoft product.


# .NET .NET Core .NET Framework的区别
- 1. .net framework is 只有windows下才有的-不跨平台的，linux,mac版本只有 .NET 和.NET Core
	- .NET Framework is a Windows-only version of .NET for building any type of app that runs on Windows.
- 2. .NET .NET Core 的区别？？？



# .NET 体系结构

# 特点
- 可以为 null 的类型可防范不引用已分配对象的变量。
- Lambda 表达式支持函数编程技术。
- 语言集成查询 (LINQ) 语法创建一个公共模式，用于处理来自任何源的数据
- 异步操作语言支持提供用于构建分布式系统的语法
- C# 有统一类型系统*。 所有 C# 类型（包括 int 和 double 等基元类型）均继承自一个根 object 类型。 所有类型共用一组通用运算。
- 任何类型的值都可以一致地进行存储、传输和处理。
- C# 还支持用户定义的引用类型和值类型。
	- C++，JAVA不都有吗，js没有吧
- C# 允许动态分配轻型结构的对象和内嵌存储。
- C# 支持泛型方法和类型，因此增强了类型安全性和性能。
- C# 可提供迭代器，使集合类的实现者可以定义客户端代码的自定义行为。
- C# 强调版本控制，以确保程序和库以兼容方式随时间推移而变化。
	- C# 设计中受版本控制加强直接影响的方面包括：单独的 virtual 和 override 修饰符，关于方法重载决策的规则，以及对显式接口成员声明的支持。

# 入门
[](https://docs.microsoft.com/zh-cn/dotnet/csharp/tour-of-csharp/#types-and-variables)
## 简介
### .NET 体系结构
### Hello world
### 类型和变量
### 程序结构

## 

# 设置C#开发环境
## .NET Core CLI(.NET SDK中自带的)
- Command-line interface (CLI) for developing cross platform websites and services on Linux, macOS, and Windows.
- 使用步骤：
	- 1. web app相关：
		- dotnet new webApp -o myWebApp --no-https
		- cd webApp
		- dotnet watch run
	- 2. 本机consle app相关：
		- dotnet new console -o myApp
		- cd myApp
		- dotnet run

- 缺点：
	- 不方便对代码进行调试
	- 对于有多个cs文件的复杂工程放不方便进行管理和构建？？
	- 对于一些简单的可以这样，对于复杂的还是使用ide好

- cmake能不能构建C#项目？？

## dotnet + vs code
- 推荐use这种方式
	- vs code 的 跨平台做的好，linux macos windows均可以
	- vscode 对于 go java html js等都有很好的支持
	- 真正有可能 one ide for all program language and os

- 配置流程：
	- 1. 下载-安装 dotnet sdk
		- dotnet sdk是直接安装在windows上的，只要下载-安装某一版本的dotnet sdk -> 整个windows上的软件都可以使用dotnet sdk
		- 通过control -> 程序：可以查看windows上有没有安装dotnet sdk
	- 2. 下载-安装 vs code
	- 3. vs code中安装C#插件

- 使用步骤：
	- 1. 在外部在指定位置创建一个工程文件夹
	- 2. 在vscode中进入这个文件夹
	- 3. ctrl+` 打开终端 
		- 在vscode中以terminal的方式创建-调试C#工程