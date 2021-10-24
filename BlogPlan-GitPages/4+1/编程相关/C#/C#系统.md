[toc]

# trivals(繁琐的细节)

## 字面值
```
字面值只能用作右值，ru:初始化

限制符 类型名 xxxxx = 字面值(or 实体(变量、表达式、函数))

```
### 后缀&&前缀

### 数值类型



### 字符类型
#### char
'a '
#### string
##### 普通的
" "
##### 改进的
u8"  "



## 类型存储时的映射机制&&转换机制
### 值存储的本质
- 虽然所有类型在内存中存储时都是二进制序列(01 + 二进制的长度(bit数)，每8bit(Byte)为一个基元)，但是不同的类型对于同一串二进制序列的解析机制是不一样的。

- 不同类型的值虽然在内存中都是定长的01序列，但是实际的值意义(现实生活中的意义：ru：10，10.5，‘k’，true)与01二进制序列之间的解析机制是不同的
	- 不仅数值类型和非数值类型的不同，数值类型之间也是不同的
	- 字符类型
		- ASCII表映射转换
		- Unicode表映射
			- UTF-8
			- UTF-16
	- 数值类型
		- 整数类型
			- 按数学中的10进制与2进制的代数转换机制来转换
				如：1 -- 00000001  3 -- 00000011
			- 为了实现正数和负数的统一  --> 使用补码的机制
				- 使用补码机制，正数负数的算术运算( + - )在补码域下能实现统一
		- 浮点类型
			- 使用的是 分段 + e指数的 转换方式
		- decimal类型(C#)
			- decimal 类型的范围较小，但精度高于 double
				- 因为和浮点数的转换机制不同？？

### 值类型的转换
- 一般编程语言is__使用二进制序列为中继__来对值进行类型转换(因为一切类型的值在内存中存储的都是一定bit长的01序列)，如：强制转换，隐式转换，还有C#中的 （string，int,float,...) ->  -> byte数组， bytes数组 ->  -> 各种类型(string , int ,float...)
	- 不同数值类型之间的类型转换：
	- 数值类型&&字符类型之间的转换：



## C# is 强类型
### 1. 编译型or解释型or混合型
#### why 要弄成混合型？
1. 每种编译形式都有其存在的原因
2. why java C# 要设置成混合型？优点是什么？跨平台、比解释的快、比编译的跨平台？
#### 混合型
1. JAVA的
### 2. 动态类型语言or静态类型语言
#### 动态类型语言：
- 动态类型语言是指在运行期间才去做数据类型检查的语言，也就是说，在用动态类型的语言编程时，永远也不用给任何变量指定数据类型，该语言会在你第一次赋值给变量时，在内部将数据类型记录下来。
- Python和Ruby就是一种典型的动态类型语言，其他的各种脚本语言如VBScript也多少属于动态类型语言。
#### 静态类型语言：
- 静态类型语言与动态类型语言刚好相反，它的数据类型是在编译其间检查的，也就是说在写程序时要声明所有变量的数据类型。
- C/C++是静态类型语言的典型代表，其他的静态类型语言还有C#、JAVA等。
### 3. 强类型定义语言or弱类型定义语言
#### 强类型定义语言
- 强制数据类型定义的语言。也就是说，__一旦一个变量被指定了某个数据类型，如果不经过强制转换，那么它就永远是这个数据类型了__。
- 强类型定义语言是__类型安全__的语言。
- 举个例子：如果你定义了一个整型变量a,那么程序根本不可能将a当作字符串类型处理。强类型定义语言是类型安全的语言。
#### 弱类型定义语言
- 数据类型可以被忽略的语言。它与强类型定义语言相反, __一个变量可以赋不同数据类型的值__。
- 强类型定义语言在速度上可能略逊色于弱类型定义语言，但是强类型定义语言带来的严谨性能够有效的避免许多错误。
- 另外，“这门语言是不是__动态语言__”与“这门语言__是否类型安全__”之间是__完全没有联系__的！
- 


## 标识符命名约定
- 标识符is什么
	- 标识符是一种字符串，用来命名变量、方法、参数、etc
1. 字母, 下划线( _ )可以用于任何位置
2. 数字不能用于句首，可放于任何其他位置
3. @只能用于居首，虽然允许使用，但不推荐使用@
4. 区分大小写
	
5. 推荐：
- 不推荐名字高度相似，尽管用了大小写来区分，还是易混淆


## 关键字
- 分普通关键字、上下文关键字。
	- 一般来说，C# 语言中新增的关键字会作为上下文关键字添加，以免破坏用旧版语言编写的程序
- 关键字不能被用做变量名or任何其他形式的标识符，除非以@字符开始
- 所有C#关键字全部由小写字母组成

## 按使用场景划分
### 上下文关键字：
![c#上下文关键字表]()

- is什么
	- 仅在特定的语言结构中充当关键字的标识符，在那些位置他们有特殊的含义
- why need 上下文关键字
	- 
- 和普通关键字的区别
	- 普通关键字不能用作标识符，而上下文关键字可以在代码的其他部分被用作标识符

#### add
- 是什么
	- add 上下文关键字用于定义一个在客户端代码订阅你的事件时调用的__自定义事件访问器__
- why need add
	- 通常不需要提供自己的自定义事件访问器。 大多数情况下，使用声明事件时由编译器自动生成的访问器就足够了，那为什么mrtk-webrtc项目使用了这个？？好处在哪里？？
	- 有时，在将一个方法加入事件内部委托列表的同时want进行一些其他操作时，add-remove会很有用，他们分别在每次对事件进行+和-的时候调用？？？？
		- 如：对一个事件+-时，自动对另一个事件进行相应的一套add-remove操作
		- ![图1](C:\Users\king-kong\Desktop\要做的事情\picture\C#\add-remove自定义事件访问器3.PNG)
	
- how use add
	- add-remove必须配套使用
		- 如果提供自定义 add 访问器，还必须提供 remove 访问器
	- 类似于属性的set，get访问器的用法
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\add-remove自定义事件访问器.PNG" style="zoom:60%;" />
	- 
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\add-remove自定义事件访问器2.PNG" style="zoom:60%;" />


### 访问限制关键字

### 方法参数关键字
- 有哪些：
	- params
	- ref
	- in
	- out

- why need ref，in，out
	- 为了解决C#中方法形参默认以值传递的方式
		- 值类型的值传递
			- 创建一个新的值类型副本传给形参，后续都是对这个副本进行操作
		- 引用类型的值传递
			- 只将第一段的引用传给形参，会存在重指向的问题
	- in -> ref -> out
		- in修饰形参
			- in 关键字会导致按引用传递参数
			- 但无法通过调用的方法进行修改
		- out修饰形参
			- 与ref的唯2区别：
				- 作为 out 参数传递的变量在方法调用中传递之前不必进行初始化（ref必须进行初始化）。 但是，被调用的方法需要在返回之前赋一个值。
				- 使用 out 参数，方法定义和调用方法均必须显式使用 out 关键字
					- ![out参数用法](C:\Users\king-kong\Desktop\要做的事情\picture\C#\方法参数_out1.PNG)
		- ref修饰形参

- ref in out会对方法的重载产生影响
	- in、ref 和 out 关键字不被视为用于重载决议的方法签名的一部分。
		- 即，如果两个方法 方法名、各形参的类型相同，只有形参名、返回类型、形参类型前的in ref out不同是无法进行重载的
		- 但是，如果一个方法采用 ref、in 或 out 参数，而另一个方法采用其他参数，则可以完成重载，如：
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\方法参数对方法重载的影响.PNG" alt="对重载的影响" style="zoom:60%;" />

- 不能将 in、ref 和 out 关键字用于以下几种方法：
	- 异步方法，通过使用 async 修饰符定义。
	- 迭代器方法，包括 yield return 或 yield break 语句。
	- 扩展方法的第一个参数不能有 in 修饰符，除非该参数是结构。
	- 扩展方法的第一个参数，其中该参数是泛型类型（即使该类型被约束为结构。）

#### params
#### ref
#### in
- 是什么
	- in 关键字会导致按引用传递参数
	- 但无法通过调用的方法进行修改
- why need in
	- 将 in 参数的方法看作一项潜在的性能优化
	- 有些时候，我们并不想在方法中更改外部变量，只想避免传递这些参数（可能产生的）高昂的复制成


- in的应用场景
	- 对值类型复制代价 >> 引用类型复制的
		- 因为大多数新式计算机中的引用都比 int 大，所以将单个 int 作为只读引用传递没有任何好处。
#### out

#### default

- why need default
	- 有隐式初始化为什么还需要default？？？

- how use default
	- 指定 switch 语句中的默认标签
	- 作为 default 默认运算符或文本生成类型的默认值
		- default运算符
			- default 运算符的实参必须是类型或类型形参的名称
				- default(int)
				- default(object)
				- default(CancellationToken)
		- default文本




## 特殊字符
### @
1. @for  -> 使 C# 关键字用作标识符

2. @" "  ->  指示将原义解释字符串（将一些转义字符失效？？）
	- 简单转义字符按字面解释，而不是进行转义解释，如：
		- 代表反斜杠的 `"\\"`）
		- 十六进制转义序列（如代表大写字母 A 的 `"\x0041"`）
		- Unicode 转义序列（如代表大写字母 A 的 `"\u0041"`
	- 有几个特殊字符不按字面解释
		- 引号转义序列 ("")不会按字面解释 -> 它生成一个双引号
		- 大括号转义序列（{{ 和 }}）不按字面解释 -> 它们会生成单个大括号字符
```
string filename1 = @"c:\documents\files\u0066.txt";
string filename2 = "c:\\documents\\files\\u0066.txt";

Console.WriteLine(filename1);
Console.WriteLine(filename2);
// The example displays the following output:
//     c:\documents\files\u0066.txt
//     c:\documents\files\u0066.txt
```

```
string s1 = "He said, \"This is the last \u0063hance\x0021\"";
string s2 = @"He said, ""This is the last \u0063hance\x0021""";

Console.WriteLine(s1);
Console.WriteLine(s2);
// The example displays the following output:
//     He said, "This is the last chance!"
//     He said, "This is the last \u0063hance\x0021"
```



### $


## 程序的入口
### c/c++语言的入口：
- 因为，C/C++允许“裸的” 变量 && 函数，main(){} 作为程序的入口，
- 因为程序只能有一个入口，所以一个函数只能有一个main(){}函数

### python的入口：
- 一般写的.py文件是作为moudule被别的.py文件 import，来使用里面的“裸的”变量、“裸的”方法、class类型的类 etc.
- python作为动态语言，它的运行方式不像静态语言那样(先生成.exe文件 -> 再运行)，而是直接进入.py文件在这个文件里使用(类似于matlab的使用方式) 数据结构 、裸的 方法 、 类
- 如果想某个.py文件按脚本方式使用，可以在这个.py文件中写一个  **if __name__ =='__main__':**

### oo语言的入口（JAVA、C#）：
#### C#的入口：
- C#不允许有“裸的”变量、方法
- C#语言下的程序 == 一组文件( 文件 == 一组 类型声明 + namespace)
	- ![]()
- 至少有一个类其中声明了 Main(){}函数,作为程序入口，含有Main(){}的类可以作为 “主类”(也可以作为“助手类”)，未含有Main(){}的类 只能作为“助手类”(被别的类使用，不能作为程序的入口)

- C#9 以后有2种入口点：
	- 名为Main的静态方法
	- 顶级语句作为程序的入口点


##### 名为Main的静态方法(C#9之前)

- 是什么
	- When the application is started, the Main method is the first method that is invoked
- why need it

- Main的静态方法的要点：
	- C# application至少有一个类其中声明了 Main(){}函数,作为程序入口。但是，Libraries and services do not require a Main method as an entry point.
	- There can only be one entry point in a C# program
		- If you have more than one class that has a Main method, you must compile your program with the StartupObject compiler option to specify which Main method to use as the entry point.
	- Main is declared inside a class or struct
	- Main must be static and it need not be public. 
		- In the earlier example, it receives the default access of private
		- The preceding examples all use the public accessor modifier. That's typical, but not required.，why？？？
		- 但是，The enclosing class or struct is not required to be static.
	- 输入输出参数上：
		- 返回类型上：
			- ```void, int```, or, starting with C# 7.1, ```Task, or Task<int>``` return type.
				- If and only if Main returns a ```Task or Task<int>```, the declaration of Main may include the async modifier. 
				- 返回类型作用于C#程序运行在的environment上
					- When a program is executed in Windows, any value returned from the Main function is stored in an environment variable. This environment variable can be retrieved using ERRORLEVEL from a batch file, or $LastExitCode from PowerShell.
		- 输入参数上：
			- with or without a string[] parameter that contains command-line arguments. 

```
public static void Main() { }
public static int Main() { }
public static void Main(string[] args) { }
public static int Main(string[] args) { }
public static async Task Main() { }
public static async Task<int> Main() { }
public static async Task Main(string[] args) { }
public static async Task<int> Main(string[] args) { }
```


##### 顶级语句作为程序的入口点(C#9中添加了此功能)

- 是什么
	- Top-level statements - programs without Main method
- why need it？？
	- Top-level statements let you write simple programs for small utilities such as Azure Functions and GitHub Actions.
	-  They also make it simpler for new C# programmers to get started learning and writing code.

- 顶级语句的使用注意事项：
	- 一个C#程序(由多个文件组成)只能有一个入口点，-> 只能有一个文件有top-level statements
		- Putting top-level statements in more than one file in a project results in the following compiler error: CS8802 Only one compilation unit can have top-level statements.
		- 一个程序可以有任意多个不含top-level statements的源文件
	- using指令必须在top-level statements上方
		- If you include using directives, they must come first in the file
	- namespaces and type definitions必须在top-level statements下方
	- args：
		- 顶级语句可以引用args变量来访问输入的任何命令行参数。args变量从不为null，但如果未提供命令行参数，则其长度为零。
	- await：
		- You can call an async method by using await
	- Exit code for the process：
		- To return an int value when the application ends, use the return statement as you would in a Main method that returns an int.
		- 显式使用的return语句，必须放在Top-level statements的最后一行？？即，它的后面不能再有裸的语句了？？
	- Implicit entry point method：

![顶级语句]()

```
// A skeleton of a C# program
using System;

// Your program starts here:
Console.WriteLine("Hello world!");

Console.Write("Hello ");
//You can call an async method by using await
await Task.Delay(5000);
Console.WriteLine("World!");

//顶级语句可以引用args变量来访问输入的任何命令行参数。args变量从不为null，但如果未提供命令行参数，则其长度为零。
if (args.Length > 0)
{
    foreach (var arg in args)
    {
        Console.WriteLine($"Argument={arg}");
    }
}
else
{
    Console.WriteLine("No arguments");
}

//要在应用程序结束时返回int值，请像在返回int的Main方法中一样使用return语句。

int returnValue = int.Parse(Console.ReadLine());
return returnValue;



namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }
}
```



## 空白机制
- C#中支持，自动检测出“空白”，并在编译的时候自动忽略，这样便对程序员更友好(更不易出错)
```
	void Main(){
	 console.write("Hi");
	 console.writeLine("HiHi");
	}
	
	void Main(){consle.write("Hi");console.writeLine("HiHi");}
```
明显第一种更易读。
	
- C#中空白字符有4种：空格(Space) 制表符(Tab) 换行符(/n) 回车符(Enter)


## op->表达式->语句->块
![op->表达式->语句->块]()
### op符
#### 一元算术运算符
##### +
- 简单返回操作数的值
```
int x = +10;
```
##### -
- 返回0减操作数的数值
```
int x = +10;
int y = -x;
```

##### typeof()
- GetType()方法会调用typeof()
- GetType()方法属于object??任意类型均有?

##### nameof()
- 是什么
- why need it
- how use it
```c#
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class AwaitOperator
{
    public static async Task Main()
    {
        Task<int> downloading = DownloadDocsMainPageAsync();
        Console.WriteLine($"{nameof(Main)}: Launched downloading.");

        int bytesLoaded = await downloading;
        Console.WriteLine($"{nameof(Main)}: Downloaded {bytesLoaded} bytes.");
    }

    private static async Task<int> DownloadDocsMainPageAsync()
    {
        Console.WriteLine($"{nameof(DownloadDocsMainPageAsync)}: About to start downloading.");

        var client = new HttpClient();
        byte[] content = await client.GetByteArrayAsync("https://docs.microsoft.com/en-us/");

        Console.WriteLine($"{nameof(DownloadDocsMainPageAsync)}: Finished downloading.");
        return content.Length;
    }
}
// Output similar to:
// DownloadDocsMainPageAsync: About to start downloading.
// Main: Launched downloading.
// DownloadDocsMainPageAsync: Finished downloading.
// Main: Downloaded 27700 bytes.
```


#### =>运算符
- is什么
- why need it
- => 支持两种形式：
	- 作为 lambda 运算符
	- 表达式主体定义
##### 用于lambda表达式

##### 用于Expression-bodied 成员(表达式主体定义)
- 表达式主体定义具有下列常规语法:
	- member => expression;
		- expression 的返回类型必须可隐式转换为member的类型
		- 如果成员的返回类型为 void，或者如果member是构造函数、终结器、属性或索引器 set 访问器，则 expression 必须为语句表达式（如： set => locationName = value;）。
			- 由于表达式的结果被丢弃，该表达式的返回类型可以是任何类型。

- 自 C# 7.0 起，下列成员(member)均支持表达式主体定义：
	- 只读属性
	- 属性
	- 索引器
	- 方法
	- 构造函数
	- 终结器

- 表达式主体定义的底层实现是不是直接替换？？
	- 即，在使用上述member的地方直接替换为expression表达式？？
		- 如：每个调用 ToString()时，实际运行的是那一行表达式
		- 访问只读属性时，返回的也是表达式的结果

###### 只读属性

- 直接PropertyType PropertyName => expression;
- 每次在访问只读属性member的时候，都使用expression代替？？？

- 方式1:
```
   public abstract class MediaTrackSource : MonoBehaviour
    {
    	//只读抽象属性
        public abstract MediaKind MediaKind { get; }
		//只读抽象属性
        public abstract bool IsLive { get; }
        
    }
    
    public abstract class VideoTrackSource : MediaTrackSource
    { 
        public WebRTC.VideoTrackSource Source { get; private set; } = null;
        //对只读属性进行表达式主体定义
        public override bool IsLive => Source != null;

        public override MediaKind MediaKind => MediaKind.Video;
    }
```

- 方式2：
```
private readonly List<MediaLine> _mediaLines = new List<MediaLine>();
//不用使用set,get访问器，直接使用  普通字段声明 + => -> 进化为表达式主体定义实现只读属性 
public IReadOnlyList<MediaLine> MediaLines => _mediaLines;
```

###### 属性
```
public class Location
{
   private string locationName;

   public Location(string name) => Name = name;

   public string Name
   {
      get => locationName;
      set => locationName = value;
   }
}
```


###### 索引器

```
using System;
using System.Collections.Generic;

public class Sports
{
   private string[] types = { "Baseball", "Basketball", "Football",
                              "Hockey", "Soccer", "Tennis",
                              "Volleyball" };

   public string this[int i]
   {
      get => types[i];
      set => types[i] = value;
   }
}
```


###### 方法

- [访问修饰符]  returnType  funName()  => expression;
	- expression-bodied 方法包含单个表达式，它返回的值的类型与方法的返回类型匹配；
	- 对于返回 void 的方法，其表达式则执行某些操作，然后表达式的返回值丢弃？？。
```
using System;

public class Person
{
   public Person(string firstName, string lastName)
   {
      fname = firstName;
      lname = lastName;
   }

   private string fname;
   private string lname;

   public override string ToString() => $"{fname} {lname}".Trim();
   public void DisplayName() => Console.WriteLine(ToString());
}

```


###### 构造函数

###### 终结器



### op重载
- only struct|class类型有op重载
- 只有 struct|class含有op成员？？？
- op重载的要求
	- only struct|class类型有op重载
	- 
- 不是所有的op运算符都能被重载
	- 能重载的：
	- 不能重载的：
		- => 
		- ??
		- ??=




### 字面量
- 是什么
- why need 字面值
#### 值类型的

#### 引用类型的


## 方法
### 有名方法
- is什么
	- 有标识名的 输入-输出代码块 != pure块(没有输入和输出)
- why need it
	- 之所以给代码块起个名 -> to 回调的方式(通过方法名回调)使用


### 匿名方法
- is什么
	- 无标识名的 输入-输出代码块
- why need it
	- 虽然所有的匿名方法都可以被有名方法全包含(通过强行起个名字)，但是有时实在没必要起个名字 -> 允许不起名字来使用 输入-输出代码块 可以带来高效
	- 就像，有时我们想保存用记事本保存一段临时文字，因为不是什么重要的、值得被长期存储下来的数据，所以没必要专门为这个文件去花费心思起个名字，所以对于ms支持的 新建文本文档(2)这种方式很方便，可能只是节省了几秒钟的，但是对于人的心理上带来的顺畅感和开发的体验特别多()


### C#方法的参数
#### 输入形参
- 都有哪些成员可以作为方法的形参参数？？
	- 委托类型的委托变量
	- 

#### 输出









## 输出语句
### 格式字符串
1. console.write(" element is {index,alignment:format} {index,alignment:format} ",x0,x1,x2);
2. 替代标记串: {index,alignment:format}
	- 位置可以任意
	- index可以重复
	- console.write("the element is {1} he {0} he {1}",x0,x1);
3. {index,alignment:format}的介绍：
	- index:
	- alignment:
		- 控制字长&&对齐方式
			- 整数值 == 字长
				- 实际字符串长度 > 整数值 ， 按实际长度来输出
				- 实际字符串长度 < 整数值 ， 按整数值来输出
				- 总结：按最长的那个来输出
			- 对齐方式:
				- 正数:  右对齐
				- 负数:  左对齐
		- {2,-10:C}
	- format:
		- C c : 货币
		- D   :十进制
		- X	:十六进制
		- N	:数字
		- P	:百分比
		- E	:科学计数法
		- F
		- G
		- R
		- {2,-10:C4} 
			- format后面的跟的数字，表示小数的位数
			- note that 不同的格式后面跟的数字，表示的含义可能不同(可能不是小数点的位数)


## 注释方式
```
	/* */
	
	// 
	
	///<summary> 
	///      
	///</summary>
```


## C#的字符串
### 字符串类string
#### 符合格式字符串


### 普通字符串
" "

### 内插字符串
- 是什么
	- $" "

- why need 内插字符串
	
	- 与使用字符串复合格式设置功能创建格式化字符串相比，字符串内插提供的语法更具可读性，且更加方便。如下，明显比使用{0},{1}更具有可读性

```
string name = "Mark";
var date = DateTime.Now;

// Composite formatting:
Console.WriteLine("Hello, {0}! Today is {1}, it's {2:HH:mm} now.", name, date.DayOfWeek, date);
// String interpolation:
Console.WriteLine($"Hello, {name}! Today is {date.DayOfWeek}, it's {date:HH:mm} now.");

// Both calls produce the same output that is similar to:
// Hello, Mark! Today is Wednesday, it's 19:40 now.
```


- how 使用内插字符串
	- 内插字符串结构
		- ```{<interpolationExpression>[,<alignment>][:<formatString>]}```
	- 内插字符串中的特殊字符
		- 要在内插字符串生成的文本中包含大括号 "{" 或 "}"，请使用两个大括号，即 "{{" 或 "}}"
		- 因为冒号（“:”）在内插表达式项中具有特殊含义，为了在内插表达式中使用条件运算符，请将表达式放在括号内

```
string name = "Horace";
int age = 34;
Console.WriteLine($"He asked, \"Is your name {name}?\", but didn't wait for a reply :-{{");
Console.WriteLine($"{name} is {age} year{(age == 1 ? "" : "s")} old.");
// Expected output is:
// He asked, "Is your name Horace?", but didn't wait for a reply :-{
// Horace is 34 years old.
```


### 逐字字符串标识符
@" "  != @关键字

### 内插逐字符字符串

- @$" "  == $@" "
	- 从 C# 8.0 开始，可以按任意顺序使用 $ 和 @ 标记：$@"..." 和 @$"..." 均为有效的内插逐字字符串。
	-  在早期 C# 版本中，$ 标记必须出现在 @ 标记之前。


## C#程序的完整工作流程

![完整流程图]()

### C#没有预处理阶段
- C#不像C，是没有预编译阶段的，只有编译阶段。
	- C#模仿了C的预处理指令，但C#的预处理指令由__编译器__来处理
		- C#的预处理指令用来指示编译器如何处理源代码
	- C的预处理指令由什么来执行？预编译器？？
#### 预处理指令(实际上可看作编译器控制指令)
##### 基本规则
1. 与C#语句不同，预编译指令__不需要以分号结尾__
2. 预编译指令必须与C#代码在__不同的行__
3. 包含预处理指令的每一行必须以#字符开始
	- 在# 字符前可以有空格
	- 在#字符 与指令间可以有空格
4. C#的预处理指令必须出现在all实际代码之前 or 可以出现在实际代码内部？(像C/c++中的那样？)
	- 比C++好的方面就是有些指令不必须出现在所有实际代码之前
		- 只有#define 和 #undef必须出现在所有实际代码之前，不然会报```Cannot define/undefine preprocessor symbols after first token in file```
5. 允许在预编译指令行行尾添加注释
```
//这样添加注释是允许的
#pragma warning restore  /* 所有警告消息。。。 */  
```

##### 预编译指令种类
![预编译指令种类]()
###### #define 和 #undef
###### 条件编译指令
###### 诊断指令
###### 行号指令
###### 区域指令
- 为代码段命名，方便对代码进行划分和管理
- 区域指令会被编译器忽略 -> 这个命名不会对代码的功能产生任何影响
```
#region
//code here
#endregion
```
###### #pragma warning指令

### 程序集
#### 程序集概述
#### 程序集标识符
#### 强命名程序集||弱命名程序集
#### 程序集的私有方式部署
#### 共享程序集||GAC
#### 配置文件
#### 延迟签名


## 命名空间
- why need 命名空间
	- 一种隔离的方式，来解决命名冲突
### 命名空间基本规则
- 命名空间可以是任何有效__标识符__
- 命名空间可以包括__句点符号__，用于组织层次
	- 如：```namespace Microsoft.MixedReality.WebRTC.Unity{ }```
- 一个源文件内可以包含__任意数目__的命名空间声明
- 命名空间可以顺序也__可以嵌套__
	- 支持两种嵌套方式：
		- 原文嵌套：
		- 分离嵌套：
	- 虽然嵌套的命名空间位于父命名空间内部，但是其成员并不属于包裹的父命名空间，命名空间之间是相互独立的
- 命名空间支持分布式声明
- 命名空间内的类型称为命名空间的成员
	- 命名空间内的成员的使用方式
		- 使用完全限定名称
		- 使用using指令
			- using命名空间指令
			- using别名指令
- 命名空间内只能放置各种类型的声明？？？？
	- 命名空间内能使用using吗？

- 推荐的命名指南：
	- 不要把命名空间命名为与类or类型相同的名称
	- 

### using指令(命名空间的使用)

- why need using指令
	- 因为有时不想使用杭长的完全限定名

- using指令的两种使用方式
	- using命名空间指令
		- using System;
	- using别名指令
		- using sc = System.Console;

- using指令的使用要求
	- 它们必须放在源文件的顶端，在任何类型声明之前
	- 他们应用于当前源文件中的所有命名空间

- using指令的底层原理？
	- 命名空间列表？？


## 嵌套类型

- 1. 通常我们在namespace中声明类型
- 2. 也可以在某些自定义类型内部声明类型(class 、 struct ???)，称为嵌套类型
- 3. 嵌套类型可以是任意类型，包括可以是class 、 struct (delegate等行不行？？)
```
namespace test {
		
		class outer{    //封闭类？？

			
			
			//这是一个嵌套类型
			class inter{   //嵌套类
			
			}
			
			
		}

}

```

- 4. 嵌套类型 != 嵌套(与作用域相关，用于限定作用域(即使用范围))
	- 这个嵌套类型指的是类型模板的创建位置 != 使用这个类型模板声明一个实例的位置(才是嵌套==作用域的含义)
	- 嵌套类型的对象可以实例化在封闭类的外部，嵌套类型的使用==这个类型在封闭类外部创建时一样来使用

- 5. 嵌套类型只是对于(一个类型只是作为助手类来only对封闭类有作用时)，这种情况的一个直观表示作用罢了

### 嵌套类型的可见性

- 嵌套类型的可见性是指，(封闭类or外部类)对嵌套类的成员的访问具有限制,而嵌套类型是可以在封闭类内or封闭类外进行实例化->对象的

#### 1.嵌套类型&&封闭类的可见性
- 双方的关系严重不对等：
##### 封闭类型->嵌套类型
- 1. 封闭类型只能访问嵌套类型的public 、internal成员，但是不能访问private、protected类型的成员(就好像嵌套类型是一个他外部的独立类一样)
##### 嵌套类型->封闭类型
- 2. 不管封闭类的成员声明成什么限制级(private or protected也好)，嵌套类型都能当访问这些成员，这种访问时直接使用封闭类的成员名字(而不是 封闭类名.成员名)来使用？？？(是的)那如果嵌套类型内想使用和封闭类型中同样的成员名怎么办？？？(应该会覆盖吧，是外的覆盖内的 or 内的覆盖外的？)

```
	
	
```
- 2. 嵌套类型内使用的this引用的是嵌套类型的对象，嵌套类型外-封闭类内那个区域内的this引用的是封闭类型的对象
- 3. 为什么封闭类内的static型成员却无法在嵌套类内使用？？？()
- 4. 由于嵌套类型对封闭类型的完全访问权限，-> 如果封闭类is派生类，嵌套类型可以使用相同的名字来隐藏基类中的成员，可以使用new来显式隐藏

#### 2.嵌套类型&&封闭类外的类的可见性
- 1. class内部声明的嵌套类型的成员有5种访问限制符:public、protected、private、internal、internal protected
- 2. struct内部声明的嵌套类型的成员有3种访问限制符:public internal private
- 3. 在这儿两种封闭类型下，嵌套类型的默认访问级别都是private，(即都不能被封闭类型以外的对象所见)，同样private、internal型的成员也不可以被封闭类型可见



# 类型系统
1. C#程序 == 一组类的声明
2. 学C# == 学各种类型

- 类型系统is什么
	- 为了模拟完整的客观世界的所有存在
	- 所有不同的语言的功能都是这个(模拟出这个世界的一切，数字，字符，实体，结构，etc)，但是不同的语言又有所不同
		- C++：
		- C#：

- why need 类型(为什么非要使用类型？？不用不行吗)

## 类型的种类(4种)

![4种类型来源](c#类型.png)

### 1.语言自带的

#### 16种预定义类型

![]()

#### 6种自def方式


### 2.自def的
- C#支持6种自def的方式：
#### 值类型(2种)
##### struct
##### enum
##### 元组类型


#### 引用类型(4种)
##### class
##### delegate
##### interface
##### array

### 3.外部库来的(DLL,,etc)
### 4.BCL

## 按抽象关系分(C#all类型派生自Object)


## 按实际存储方式分(C#all类型分值类型&&引用类型)
- C#中all类型(不管你是内置的or自定义的)either值类型or引用类型
- why need 分值类型&&引用类型两种？？
- 值类型&&引用类型的本质区别
- 值类型和引用类型的区别：
	- 值类型的变量不能为null
	- 两个值类型变量不能引用同一对象
### 值类型
- ![C#中的值类型]()
- C#中的值类型 
	- 整形
	- 浮点型
		- double
		- float
	- decimal
	- bool
	- char
	- enum
	- struct
	- 元组 ( , )类型
	- 可为nul的值类型




### 引用类型

- 两段式存储
	- realdata总是位于堆中
	- 引用位于堆或栈中。怎么区分？？



### 值类型&&引用类型的互转
- 通过装箱-拆箱的方式


### 值类型&&引用类型的存储
- 不是因为是值类型 ->才 -> 1整块存，引用类型 -> 才 -> 分成2块存，先后关系搞错了
	- C# all类型is继承自object，只是一些类型比较轻量级使用 -> 存储时存成一整块比较方便 -> 后来这些类型被称为值类型，另一些类型因为使用的情形 -> 设计成2块存储更好，故设计成分开存储 -> 后被称为引用类型
		- 故，一个类型如何存储is编译器来设计的，你设置可以每一种类型专门设计一种存储方式，但是这样真的是合理的吗？
		- 实践是检验真理的唯一标准，目前根据C#，JAVA来看，分成值类型存储、引用类型存储是更高效的选择
## 静态(static)类型&&dynamic类型



## 可空类型
- 是什么
- why need it
	- 有些情况下，特别是使用数据库的时候，希望有一种方式能表示变量目前未保存有效值，这样就可以在使用他之前判断值的有效性
		- 对于引用类型很简单：把变量设置为null
		- 但是，对于值类型，


- 可空类型的使用步骤：
	- ![可空类型的使用步骤]()
	- 声明
		- T? variableName = null;
			- 可为空值类型的默认值表示 null
	- 赋值
		- 可以将以下3种类型的值赋给相应的可空类型的变量
			- 基础类型的值
			- 同一可空类型的变量
			- Null值
			![]()
	- 使用
		- 先做有效判断
			- 有效判断有三种方式：
				- 从 C# 7.0 开始，可以将 is 运算符与类型模式 结合使用，既检查 null 的可为空值类型的实例，又检索基础类型的值
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第一种.PNG" style="zoom:60%;" />
				- 使用HasValue 只读属性 
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第二种.PNG" style="zoom:60%;" />
				- 还可将可为空的值类型的变量与 null 进行比较
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第三种.PNG" style="zoom:60%;" />
		- 再使用

### 可为空的值类型
- 普通的值类型为非可空类型
- 可为空值类型的默认值表示 null

- 可空值类型的使用步骤：
	- ![可空类型的使用步骤]()
	- 声明
		- T? variableName = null;
			- 可为空值类型的默认值表示 null
	- 赋值
		- 可以将以下3种类型的值赋给相应的可空类型的变量
			- 基础类型的值
			- 同一可空类型的变量
			- Null值
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\可空类型变量的赋值.PNG" style="zoom:60%;" />
	- 使用
		- 先做有效判断
			- 有效判断有三种方式：
				- 从 C# 7.0 开始，可以将 is 运算符与类型模式 结合使用，既检查 null 的可为空值类型的实例，又检索基础类型的值
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第一种.PNG" style="zoom:60%;" />
				- 使用HasValue 只读属性 
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第二种.PNG" style="zoom:60%;" />
				- 还可将可为空的值类型的变量与 null 进行比较
					- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\null判断第三种.PNG" style="zoom:60%;" />
		- 再使用


- 可空类型的注意要点
	- 可空类型总是基于另外一种叫做基础类型的已经被声明的类型
		- 可以从任何值类型创建可空类型（包括预定义的简单类型）
			- 从 C# 2 开始，提供可为空的值类型
		- 不能从可空类型创建可空类型
			- 引用类型是可空的 -> 不能从引用类型创建可空类型
				- C#8.0 引入了“可为空引用类型”和“不可为空引用类型”
	- 不能在代码中显式声明可空类型，只能声明可空类型的变量( T? variableName = null的方式 )
		- 编译器会使用泛型隐式的创建可空类型
			- 只要这样声明 int? variableName = 35;  -> 编译器通过这个会自动地产生可空类型并关联变量类型
	- 可空类型和相应的非可空类型之间可以轻松实现转换
		- 非可空类型的值 -> 可空类型变量 is 隐式的
		- 非可空类型的变量 <- 可空类型变量 is 显示强制的
		- 2种转换的方式：
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\基础类型与可空类型的转换2.PNG" style="zoom:60%;" />
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\基础类型与可空类型的转换1.PNG" style="zoom:60%;" />
	- 基础类型&&可空类型的op符的提升
		- 预定义的一元运算符和二元运算符或值类型 T 支持的任何重载运算符也受相应的可为空值类型 T? 支持。
			- 如果一个或全部两个操作数为 null ，则这些运算符（也称为提升的运算符）将生成 null；否则，运算符使用其操作数所包含的值来计算结果。 例如：
		- 逻辑运算符：
		- 比较运算符：
			- <、>、<= 和 >=
			- 相等运算符 ==
			- 不等运算符 !=



- 非可空类型 -> 可空类型后 发生了什么变化？？
	- ![非可空类型->可空类型]()
	- 可空类型 = 原非可空类型 + 两个只读属性
		- 可空类型在一个结构中包含了基础类型对象，并且还有两个只读属性



### 可为空的引用类型

- 是什么
- why need it


- 引用类型可为空的注意事项
	- 未将 ? 附加到类型名称的任何变量都是“不可为 null 引用类型”（这包括启用此功能时现有代码中的所有引用类型变量 ）
	- 使用与 可为空值类型相同的语法记录 可为空引用类型：将 ? 附加到变量的类型。
		- ```string? name;```




### ??  
- 是什么
- why need it
	- 使用?? 实现 安全的从可为空的值类型转换为基础类型
		- 因为基础类型不能为null，但是可空类型可能为值为null，故要做对null型做特殊处理：当左操作为null时用右操作数来赋值
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\用于类型转换.PNG" style="zoom:60%;" />
	- 
- 在 C# 7.3 及更早版本中，?? 运算符左操作数的类型必须是引用类型或可以为 null 的值类型。 从 C# 8.0 版本开始，该要求替换为以下内容：?? 和 ??= 运算符的左操作数的类型必须是可以为 null 的值类型。 特别是从 C# 8.0 开始，可以使用具有无约束类型参数的 null 合并运算符：

### ??=

- 是什么
	- C# 8.0 及更高版本中可使用空合并赋值运算符 ??=
		- 该运算符仅在左侧操作数的求值结果为 null 时，才将其右侧操作数的值赋值给左操作数
		- 如果左操作数的计算结果为非 null，则 ??= 运算符不会计算其右操作数

- why need ??=
- 

- ??=如何使用

- ??=的注意要点
	- 对左操作数的要求：
		- 是上：
			- ??= 运算符的左操作数必须是变量、属性或索引器元素
		- 类型上：
			- 从 C# 8.0 版本开始，?? 和 ??= 运算符的左操作数的类型必须是可以为 null 的值类型


- 常规使用搭配
	- 从 C# 8.0 开始，可以使用 ??= 运算符将这样的代码
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\的用法.PNG" style="zoom:60%;" />


### ??和??=的区别


### ?. 和 ?[]

- 是什么
	- 本质上 这2个运算符 == 原 . 和 []的基础上 + 隐式做null判断
		- 将两个行为浓缩为一个运算符，更方便开发
	- 仅当操作数的计算结果为非 null 时，null 条件运算符才会将成员访问 ?. 或元素访问 ?[] 运算应用于其操作数；否则，将返回 null。 即：
		- 如果 a 的计算结果为 null，则 a?.x 或 a?[x] 的结果为 null。
		- 如果 a 的计算结果为非 null，则 a?.x 或 a?[x] 的结果将分别与 a.x 或 a[x] 的结果相同。
- why need it
	- 有了这两个运算符，我们就能更方便的安全使用各种类型的实例，如：<img src="C:\Users\king-kong\Desktop\要做的事情\picture\可空类型12.PNG" style="zoom:60%;" />


- 注意要点
	- NULL 条件运算符采用最小化求值策略。 即：
		- 如果条件成员或元素访问运算链中的一个运算返回 null，则链的其余部分不会执行
		- 在以下示例中，如果 A 的计算结果为 null，则不会计算 B；如果 A 或 B 的计算结果为 null，则不会计算 C：
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\可空类型11.PNG" style="zoom:50%;" />
	- 



## 类型声明位置&&作用域

## 类型&&存储
- 数据类型被分隔为值类型和引用类型。 值类型要么是堆栈分配，要么在结构中以内联方式分配。 引用类型为堆分配。 
- 引用类型和值类型均派生自最终基类 Object 。 
	- 尽管object ->  ValueType 是值类型的隐式基类，但无法创建直接从继承的类 ValueType 。只能通过相应的关键字struct enum等来进行创建
		- 除了充当 .NET Framework 中的值类型的基类， ValueType 结构通常不在代码中直接使用。 但是，它可用作方法调用中的参数，以将可能的自变量限制为值类型而不是所有对象，或者允许方法处理许多不同的值类型。
- 如果需要值类型的行为与对象类似，则会在堆上分配值类型类似于引用对象的包装，并将值类型的值复制到其中。 包装已标记，因此系统知道它包含值类型。 此过程称为装箱，相反的过程称为取消装箱。 装箱和取消装箱允许任何类型被视为对象。
### C#有几个存储区域
静态存储区？
动态存储区(heap)?
自动存储区(stack)?

### 不同类型的变量的存储位置(空间上)

### 不同类型的变量的确定时间(时间上)
- 从编写玩源代码文件 -> ... -> 结果呈现，期间变量的整个变化过程是怎样的？(如：complier何时给变量分配内存、分配的内存生存期有多长、分配的位置在哪里、)


## 类型的大小(sizeof(类型))




# 6种自def类型的use
- C#支持6种自def的方式：
	- 值类型(2种):
		- struct
		- enum
	- 引用类型(4种):
		- class
		- interface
		- delegate
		- array

- why need it ( why C#要支持这6种自def的类型？？)
	- 这6种是实际任务需要的抽象
		- class
			- class表示的数据和方法的集合的抽象
		- delegate
			- 委托是对纯方法列表的抽象
		- struct
			- 是对数据结构的抽象，它允许的一般都是数据结构需要的

- 这些关键字自def类型中都可以有哪些成员？
	- class
		- 数据相关
		- 操作相关
	- struct
		- 数据相关
		- 操作相关
	- enum
		- 常量成员
	- delegate
		- 创建委托类型时，只是声明一种输入输出类型，没有别的成员，只是满足类型的方法可以加入
	- Array
	- interface
		- 不能包含：
			- 数据成员
			- 静态成员
		- 能包含：
			- (must非静态的、must方法声明)
			- 方法
			- 属性
			- 事件
			- 索引器

- 这些类型的独特使用方式在底层是怎么实现的？


## enum
- 是什么
- why need 枚举

### enum和struct的区别

### enum可以有哪些成员

### how 使用 enum

#### 位标志

#### enum的特点
- 不能对成员使用修饰符。他们都隐式的具有和枚举相同的可访问性
- 成员是常量，即使在没有该枚举类型的变量时他们也可以被访问
	- 使用 EnumName.成员名
- enum声明的不同枚举类型是独特的类型，不能对不同枚举类型的成员进行比较
- 




## struct
- 是什么
- why need 结构
	- 对结构进行分配比创建类的实例开销小，所以使用结构代替类有时可以提高性能，但是要注意装箱-拆箱的高代价
		- 预定义简单类型(int，short，long，etc)，尽管在.NET和C#中被视为原始类型，但是实际上在.NET中都实现为结构

### struct和class的对比
- 类是引用类型，结构是值类型，故，引用类型和值类型的区别都是
	- struct类型的变量不能为null（除非声明为可为空值类型）
	- 两个结构变量不能引用同一对象
	- 内存排列上的区别
		- ![]()
	- 类变量和结构变量赋值上的区别
		- 赋值类变量时只是复制引用（浅复制）
		- 赋值结构变量时，会对每个成员的值进行复制（深复制）
- 结构是隐式密封的 -> 他们不能继承和派生 -> 多个struct间只能有复合关系，而不能有继承关系
- 成员默认访问限制级
	- class
		- private
	- struct
		- public
- 构造函数上的区别：
	- 不能声明无参数构造函数。 每个结构类型都已经提供了一个隐式无参数构造函数，该构造函数生成类型的默认值。
	- 结构类型的构造函数必须初始化该类型的所有实例字段。
		- 不能在声明实例字段或属性时对它们进行初始化。 但是，可以在其声明中初始化静态或常量字段或静态属性。
- 析构函数上的区别：
	- 不能在结构类型中声明析构函数


### 一个struct的一切
#### struct可以有哪些成员
- 和class相比struct都能有什么成员？？
- 允许有
	- 数据相关
		- 常量
		- 字段
	- 方法相关
		- 构造函数（包括：实力构造函数&&静态构造函数 -> 说明struct可以有静态成员）
- 不允许有
	- 析构函数。why??
	- 常量成员
	- 隐式密封


#### 成员区
##### 数据相关

##### 操作相关
###### 构造函数
- struct可以有构造函数（包括：实力构造函数&&静态构造函数 -> 说明struct可以有静态成员）
- 语言隐式的为每个结构提供一个无参数的默认构造函数，这个构造函数负责：
	- 把结构的每个成员设置为该成员类型的默认值
		- 值类型成员设置为他们的默认值
		- 引用类型成员设置为null
- 无参数的默认构造函数对每个结构都存在，而且不能重定义or删除
	- 即使你定义了有参数的，这个无参默认的也会存在
	- 也不能对无参默认的进行重定义，想自定义构造函数只能写成有参的构造函数
		- 不能声明无参数构造函数。 每个结构类型都已经提供了一个隐式无参数构造函数，该构造函数生成类型的默认值
- 创建struct实例的方式
	- 使用new运算符
		- 调用struct的构造函数(包括隐式无参构造函数)must要使用new运算符
			- 即使不从堆中分配内存也要使用new运算符 -> 结构体使用new创建不一定分配在堆上也可能在栈上，怎么区分结构体实例是在堆上or栈上？？有没有规律？？
			- 想要调用无参默认构造函数也要使用new才能
	- 不使用new运算符
		- 也可以不使用new运算符来创建结构的实例，然而，如果这样做，会有一些限制：
			- 在显式设置数据成员之后，才能使用它们的值
			- 在对所有数据成员赋值之后，才能调用任何函数成员
				- struct类型内初始化赋值算不算？？
					- struct不允许字段初始化语句 ![]()
				- 因为不使用new不会调用默认无参构造函数 -> 有些成员没有默认初始化(在底层上就是没有给成员变量分配存储空间？？)

###### 静态构造函数
- 结构的静态构造函数遵从类的静态构造函数一样的规则
	- 目的上：
		- 用于创建并初始化静态数据成员
	- 调用方式上：
		- 只能隐式调用，不能显式调用
		- 调用时间不能确定，在以下两种行为任意一种发生之前，将会调用静态构造函数
			- 调用显式声明的构造函数
			- 引用结构的静态成员

#### 成员级特点
- 结构总是密封的 -> struct不允许继承 -> 一些成员修饰符没有意义，故，一些成员修饰符不被允许
	- protected
	- internal
	- abstract
	- virtual
- 结构本身派生自System.ValueType，System.ValueType派生自object
	- 两个可以用于结构成员并于继承相关的关键字是new和override修饰符
		- new
		- override
	- 当创建一个和基类System.ValueType的成员有相同名称的成员时使用它们

##### const

##### static



#### struct级特点
##### 分布结构(partial)
- 和分布类一样，也有分布结构

##### readonly结构

##### ref结构
- 是什么
	- 从 C# 7.2 开始，可以在结构类型的声明中使用 ref 修饰符
	- ref 结构类型的实例在堆栈上分配，并且不能转义到托管堆。

- why need ref struct
	- 对于高性能和原生开发场景，你可能希望“仅限堆栈”类型始终停留在执行堆栈上，因此对这种类型的对象的操作只能发生在堆栈上，在作用域中公开给托管堆的任何对这种类型的外部引用都应该被禁止。
- ref struct是仅在堆栈上的值类型：
	- 表现一个顺序结构的布局；（译注：可以理解为连续内存）
	- 只能在堆栈上使用。即用作方法参数和局部变量；
	- 不能是类或正常结构的静态或实例成员；
		- 静态成员分配在静态存储区上 == 全局的 、在编译期间确定运行期间一直不变的
		- 类or正常结构的实例成员 == realdata 是分配在heap上的
	- 不能是异步方法或lambda表达式的方法参数；
	- 不能动态绑定、装箱、拆箱、包装或转换。


### 多个struct的关系(只能有复合关系)
- 一个struct中含有另一个struct
- struct 是 隐式sealed的
- 可以实现接口



### struct的用处

#### 结构作为返回值
- 和普通值类型一样，当结构作为返回值时，将创建它的副本并从函数成员返回

#### 结构作为参数
- 默认是值参数
- 使用ref和out限制符来内外关联


## 元组类型
- 是什么
	- 元组功能在 C# 7.0 及更高版本中可用
	- 提供了简洁的语法，用于将多个数据元素分组成一个轻型数据结构。
- why need 元组
	- class ->轻量化，减去一些东西-> struct ->轻量化，再减去一些东西-> 元组

- 元组的注意事项
	- 元组类型是值类型；
	- 元组元素是公共字段
	- 这使得元组为可变的值类型
		- C#中的元组不像python中的元组(一旦创建后只能读，不能改)，而是可以实时更改的？？
	- 元组元素名称
		- 可以显式指定字段名称（2种显式指定的方式）
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\3.PNG" style="zoom:50%;" />
		- 也可以初始化时的变量名称推断，据元组初始化表达式中相应变量的名称推断出此名称（即，用变量的名称作为字段的名称）
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\4.PNG" style="zoom:50%;" />
		- 始终可以使用字段的默认名称，即使字段名称是显式指定的或推断出的
			- 元组字段的默认名称为 Item1、Item2、Item3 等
	- 在编译时，编译器会将非默认字段名称替换为相应的默认名称。 因此，显式指定或推断的字段名称在运行时不可用
	- 元组赋值和元组相等比较不会考虑字段名称
	- 从 C# 7.3 开始，元组类型支持相等运算符 == 和 !=
	- 元组不能自定义方法，但可以使用它基类中的方法
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\元组2.PNG" style="zoom:50%;" />
	- 可以使用任意数量的元素定义元组
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\元组1.PNG" style="zoom:60%;" />
	- 元组功能需要 System.ValueTuple 类型和相关的泛型类型（例如 System.ValueTuple<T1,T2>）
		- 这些类型在 .NET Core 和 .NET Framework 4.7 及更高版本中可用。 若要在面向 .NET Framework 4.6.2 或更早版本的项目中使用元组，请将 NuGet 包 System.ValueTuple 添加到项目。
### 元组相对于struct又减去了哪些功能
- 方法
	- 不能在元组类型中定义方法
	- 但可以使用 .NET 提供的方法
		- 是因为元组 <- ValueType <- Object的缘故？？

### how use 元组
- 声明元组变量
- 元组赋值
	- 满足下列2个条件的元组可以赋值
		- 两个元组类型有相同数量的元素
		- 对于每个元组位置，右侧元组元素的类型与左侧相应的元组元素的类型相同或可以隐式转换为左侧相应的元组元素的类型
- 元组析构
- 元组作为out参数
- 元组作为ref参数？？

### 选择匿名类型or元组类型


### 什么情况适合使用元组||什么情况不适合使用元组？？

#### python中的元组(tuple)&&列表(list)is相关的概念
- 元组：带上枷锁的列表
	- 列表：一个大仓库，你可以随时往里边添加和删除任何东西。
	- 元组：封闭的列表，一旦定义，就不可改变（不能添加、删除或修改）。
		- 除非通过新建一个元组来间接修改，但这就带来了消耗
- 什么情况下你需要使用元组而不是列表？
	- 当我们希望内容不被轻易改写的时候，我们使用元组（把权力关进牢笼）。
	- 当我们需要频繁修改数据，我们使用列表。

#### C#中的List<>，必须是同类型的才能加入，如何实现python那样的、or像元组那样的任意类型的列表？？

##### 如何使用C#实现python中的List？？
- Python中的列表是个神奇的数据结构，也是Python中最学用的一个数据结构（个人认为），它能存放各个类型的数据，lst1=[1,2,2.3,”string”]；它的数据元素还能是列表，lst2=[1,2,2.3,”string”，
- 而C#中的List、List<> 只能是同类型的

## delegate
- 是什么
	- __实际上__是一个对象
		- 委托是一个持有一个or多个(同输入参数列表，同返回类型)的方法的对象
		- 故委托的使用(包括委托的声明、创建、使用、销毁)&&普通对象的使用__相似又存在不同__
			- 类表示的是数据和方法的集合，而委托表示的是一个or多个方法+对这些方法的预定义操作
	- __抽象上__是一个同输入参数列表，同返回类型的顺序方法组
		- 这样我们在使用方法的时候，就有两种粒度的方式：单方法、方法组。更加灵活
- why need 委托
	- 有时存在这样一种需求：不是只执行一个方法而是需要按顺序的一次执行多个（同输入、同返回类型）的一组方法
		- 如：发布者-订阅者模型是委托+事件
			- 小卖部的到货通知的那张电话单，到货时(事件触发)会依据预留的电话表(委托对象==方法组)依次打各个电话(回调各个方法)



### how use 委托

- 和class的使用步骤相似
	- 使用delegate声明委托类型A（like 使用class 声明类类型A）
	- 使用__自定义的委托类型A__实例化委托对象（like 使用自定义的类模板实例化一个此类的对象）
	- 使用委托对象（like 通过实例化的对象来使用类中的字段和方法）
	- ![delegate和class的使用流程](C:\Users\king-kong\Desktop\要做的事情\picture\委托操作步骤.png)

- delegate的特点
	- 委托对象里面__有一个调用列表__
	- 委托保存的方法__可以来自任何类或结构__，只要他们在以下两点匹配：
		- 返回类型
		- 输入参数列表（包括参数列表中的ref和out修饰符）
	- 调用列表中的方法__可以是实例方法也可以是静态方法__
	- 调用委托的时候，会按顺序依次执行调用列表中的所有方法

- delegate的注意事项
	- 声明委托类型
		- 以delegate关键字开头
		- 不能有方法主体
		- delegate和class一个等级的，可以在class外部声明
	- 创建委托对象
		- 创建委托对象is__为委托对象分配内存__，然后将内存地址返回给委托变量
			- 委托内存存放的是什么？？
				- 方法的实际代码体or方法的回调地址
		- 委托变量 != 委托对象
			- 委托变量只存储指向委托对象的饮用
			- 委托对象 is 由委托的实体(隐式or显示由new delegateName(方法名)来创建的)
	- 操作委托对象（+、-、组合）
		- 委托对象一经创建是不可变的，后续无论是 组合、+、-都是创建一个新的委托（创建新的调用列表），then将新的委托对象的引用赋值给委托变量
		- 根据 组合、+、-不同，创建新的委托的具体细节不同
			- -= 
				- -=运算符__从列表最后开始搜素__，并且移除第一个与方法匹配的实例
				- 试图删除委托中不存在的方法没有效果
				- 试图调用空委托(方法调用列表为空的委托)会抛出异常
					- 在调用委托之前，要加上 （委托变量 != null） 判断
	- 调用委托对象
		- 带返回值的委托
		- 带ref输入参数的委托

### 委托 + 有名方法 -> 委托 + 匿名函数 -> 委托 + lambda表达式
#### 委托 + 有名方法
- 最经典的委托的使用方式，上述的###how use 委托中讲的就是这个
- 一般来说 匿名方法 or lambda表达式都可以通过将为有名方法的方式来实现，只是有些情况实在没必要给代码段起一个名字(因为有的时候起名字真的很折磨人啊)


####  委托 + 匿名函数(delegate标识的)



#### 委托 + lambda表达式(=>标识的)



### 委托&&事件


### 委托用于方法形参列表






## Array -> 数组

### 数组声明、初始化时长度如何设置的本质
- 1. 数组声明时要不要指定长度？为什么？
- 2. 数组声明时用常数(编译期间确定)制定长度(define、const确定的) or 可以用运行时变量来指定长度(如，vector)？？为什么？？
- 3. 可以初始化时在指定长度吗？
- 4.

## interface

- 是什么
	- 是一组函数声明，只能被class or struct实现来使用
- why need 接口

- 接口是一个引用类型，接口对象里存的引用指向哪里？？指向内存中的实现了他的类中or结构中？？
	- 底层是怎么实现的？
	- 

- interface的注意事项
	- interface能包含的成员
		- 不能包含：
			- 数据成员
			- 静态成员
			- 构造函数
			- 类型
		- 能包含：
			- (must非静态的、must方法声明)
			- 方法
			- 属性
			- 事件
			- 索引器
	- 这些函数成员的声明不能包含任何实现代码
		- 方法
			- public returnType funName();
		- 属性
			- public returnType funName(){ set; get; };
		- 索引器
			- public returnType this[int index]{ set; get; };
		- 事件
			- 
	- 按照惯例，接口名称必须从大写的I开始（比如：ISaveable）

### 一个interface的一切
#### 成员区
- interface能包含的成员
	- 不能包含：
		- 数据成员
		- 静态成员
	- 能包含：
		- (must非静态的、must方法声明)
		- 方法
		- 属性
		- 事件
		- 索引器
##### 数据相关

- 无

##### 操作相关
###### 方法
###### 属性
###### 索引器
###### 事件




#### 成员级特点
- 不能有static，all成员必须是非静态的

##### 接口成员的访问修饰符
- 接口的成员是隐式public的，不允许有任何访问修饰符（包括显式public）



#### interface级特点
##### 分布接口(partial)
##### interface的访问修饰符
- 接口声明可以有任何的访问修饰符public、protected、internal、private 


### 多个interface的关系
#### 多继承
- 接口间可以__多继承__
	- 类or结构可以实现任意数量的接口
	- 所有实现的接口必须列在基类列表中并以逗号分隔

#### 复合关系？？？




### interface的使用
- 接口只能被struct和class通过先实现，再使用
- 要实现接口，类or结构必须：
	- 在基类列表中包括接口名字
		- 基类列表中同时有基类和接口时 -> 基类必须放在所有接口之前，接口之间顺序随意
	- must为接口的每一个成员都提供实现

#### 接口的实现

##### 一般情况的实现
```


```

##### 基类成员作为实现
- 派生类实现接口，但是基类中实现了接口中的同名方法，此时，基类中的代码还是能满足实现接口方法的需求(即，不用在派生类中重新实现也能用)
- ![基类成员作为实现]()

##### 实现具有重复成员的多个接口
###### one for all型
- 由于类可以实现任意数量的接口，有可能两个or多个接口成员都有相同的签名和返回类型，编译器如何处理此种情况？？
	- 如果一个类实现了多个接口，并且其中一些接口有相同的签名和返回类型的成员，那么类可以实现单个成员来满足所有包含重复成员的接口(即，class中实现一个，多个接口都可以使用)
	- ![同一个类成员实现多个接口]()

###### 显示接口成员实现(每个接口分离实现)
![显示接口成员实现]()
###### 访问显示接口成员实现
- 显示接口成员实现只可以通过指向接口的引用来访问
	- 即，只能通过 类对象 -> 强制类型转换 -> 接口 来访问，不能通过 类对象名.方法名() 来访问 
	- 类的其他成员方法也不可以直接访问他们![]()


##### 不同类实现同一个接口
![]()

- 基类作为子类的入口，不是会进行截断的吗？（即，只能从基类看到子类中继承的基类的那一部分，子类新增区的基类不可见吧）为什么基类可以将子类实现的接口传给接口类型引用？？


#### 接口的2种使用方式
![]()
##### 通过类对象来使用（便捷版，有使用条件）
- 类内实现了接口中的各方法后，便可以通过 objName.成员方法名() 来使用接口中声明的方法，但是满足下列要求的才可以使用这种便捷方式，否则只能使用强制类型转换+接口类型的方式
	- 接口方法的实现不能是__显式接口成员实现__

##### 通过类对象->强制类型转->接口类型引用来使用（万金油版）
- 


###### 多个接口的引用
- 如果类实现了多个接口，我们可以获取每一个接口的独立引用



## class
### 一个类的一切
### 类间关系
#### is-a
##### 继承
#### has-a
##### 复合
##### private继承

### 类的使用




# 类型转换
- 是什么
	- 接受一个类型的值并使用它作为另一个类型的等价值的过程
	- 转换后的值应和原值一样(这个是哪个域意义下的值一样？)，但其类型变为目标类型
- why need类型转换

## 值的类型转换任务的抽象

![类型转换任务抽象图]()

### 隐式类型转换(不会丢失精度的转换)
#### 扩充机制
##### 零扩展(无符号类型的)
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\无符号扩展.png" style="zoom:40%;" />

- 在前面补0
##### 符号扩展(有符号类型的)
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\符号扩展.png" style="zoom:40%;" />

- 对于有符号类型的转换，额外的高位用源表达式的符号位进行填充
- 正数在前面补0
- 负数在前面补1
### 显式类型(强制类型)转换(可能会出问题的转换) 

#### 溢出机制
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\溢出.png" style="zoom:40%;" />


## C#类型转换总览

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#类型转换.PNG" style="zoom:33%;" />

### 值类型间的转换
#### 数字类型的转换
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#数字类型的转换.png" style="zoom:33%;" />

##### 隐式数字类型转换
##### 显示数字转换
- 知道发生数据丢失时转换会如何处理很重要
##### 溢出检测上下文(显示数字类型转换的)
- 代码片段是否溢出检查称作溢出检测上下文
- C#给我们提供的自主选择运行时是否在进行类型转换时检测结果溢出的能力
	- C#通过提供checked运算符和unchecked运算符来实现此能力

- 默认的溢出检测上下文是__不检查__

###### unchecked和checked运算符的使用
1. checked和unchecked运算符
- checked(表达式)
- unchecked(表达式)
```
ushort sh = 2000;
byte by1 = unchecked( (byte) sh )   //能运行但是会丢失重要的位
byte by2 = checked( (byte) sh )		//直接抛出溢出错误
```

2. checked和unchecked语句
- 和1.中执行相同的功能，但是控制的是一块代码中的所有转换，而不仅是单个表达式
- unchecked语句和checked语句可以被嵌套在任何层次


### 引用类型间的转换
- 和值类型不同的是，继承链深的到浅的不会丢失信息(会隐式进行)

#### 隐式引用类型转换
- 所有引用类型可以隐式转换为object类型(因为，object是继承链上的根)
- __任何类型__可以隐士转换到他继承的接口
- 类可以隐式转换到：
	- 他继承链中的任何类
	- 它实现的任何接口
- 委托可以隐式转换成.NET BCL的类和接口
	- System.Delegate, System.MulticastDelegate

- Array数组可以隐式转换为：
	- .NET BCL类和接口
	- 另一个Array数组，只要同时满足下列条件：
		- 两个数组有一样的维度
		- 他们的元素类型都是引用类型不是值类型
		- 在他们的元素类型间存在隐式转换
#### 显示引用类型的转换
- 从object到任何引用类型的转换
- 从基类到他派生的类的转换
- 引用类型的显示转换不导致溢出问题而是引用内存中不存在类成员这种问题(因为是小的强行变成大的)
##### 运行时能成功运行的显示转换有3种
1. 显示转换是没有必要的(也就是说语言以自动为我们进行了强制转换)
	- 从派生类到基类的转换总是隐式转换的
2. 源引用是null(因为引用类型不管大小都使用null表示空指向)
```

```
3. 由源引用指向的实际数据可以被安全的进行隐式转换
```


```
### 值类型 <==> 引用类型间的

#### 装箱转换(值类型->引用类型)
- 装箱转换is一种隐式转换
- 装箱is创建对象副本	
	- 在装箱完成之后，该只有两个副本：原始值类型、引用类型副本，每一个都可以独立操作
```
int i = 10;

object oi = i;//

i = 12;
oi = 15;//i变量值仍是12
```

- 任何值类型都可以隐式转换为object类型、System.ValueType类型
![]()
#### 拆箱转换(引用类型->值类型)
- 拆箱转换is显示转换
- 拆箱时进行的过程
	- 1. 检测要拆箱的对象是不是
	- 2. ‘
- 尝试将一个值拆箱为非原始类型会抛出InvalidCastException异常

### 自def类型转换 
- 为自def类型而设计的，不可能源目标类型都是内置类型，那样的是不允许自def类型转换的也是没有意义的
- 自def类型转换的本意就是为自def类型设计转换机制？？内置的标准类型转换就够用了
#### 自def类型转换的要求
- 只可以为class和struct定义用户自def类型转换
- 不能对前面的标准隐式or显示转换进行重自def
- 对于源类型S到目标类型T
	- S和T必须是不同类型
		- 对于相同的源or目标类型，我们不能声明隐式转换和显示转换
	- S和T不能通过类型关联
		- 即，S不能继承自T，T也不能继承自S
	- S和T都不能是接口类型or object类型
	- 转换运算符必须作为S or T的成员
#### 自def类型转换的声明有特定格式
- 使用implicit explicit来标识是隐式转换or显示转换
- 必须将声明式放于原类型or目标类型
	- 哪个类型可自定放于哪个类型之中
		- 如：自def  Person类 -> int类的隐式类型转换 or flaot -> Person类型的显示转换，因为int float类型is不可更改的，故我们将其放于可自def的Person类中
	- 不可能源目标类型都是内置类型，那样的是不允许自def类型转换的

![声明格式]()


#### 自def类型转换的使用也有特定格式

![使用格式]()

#### 多步转换->合为->单步转换

![]()

## 类型转换相关运算符
### is运算符
- is什么
	- 用于"是"关系检测的，只检测不判断
- why need is运算符
	- 有些转换会报错，我们最好再转换前先检查一下，从而避免盲目转换


- is运算符只可以用于__引用间转换__、__装箱-拆箱__、不能用于__用户自定义转换__
- is运算符的使用语法
	- 通过表达式来使用
		- 源(待转换的变量or实例) is TargetType(想转成的类型)
		- 表达式返回true -> 存在是的关系 -> __引用间转换__、__装箱-拆箱__是可以成功的
```
class Employe : Person{

}

class Program{

	static void main(){
	
		Employe bill = new Employe();
		Person p;
		
		//先检查，再转换
		if(bill is Person){
			p = bill;
			// code here
		}
		
	}
}
```

### as运算符

- is什么
	- as真的会进行显示转换而且不会报错，和is只进行检测能不能隐式转换不同
- why need it

- as运算符只能用于__引用间转换__、__装箱转换__，不能用与__用户自定义__or__值类型的转换__
- as运算符和强制转换运算符类似，只是他不抛出异常
	- 如果转换失败，返回null而不是抛出异常
- as运算符的使用语法
	- 1. typeObj = srtObj as typeof(typeObj)
	- 2. 因为不会返回错误最多返回null->使用时要加上null判断
```
class Employe : Person{

}

class Program{

	static void main(){
	
		Employe bill = new Employe();
		Person p;
		
		//先显示转换，再检查判断
		p = bill as Person;
		if(p != null){
			// code here
		}
		
	}
}
```





# 泛型

- 是什么
	- 泛型类型is类型的模板![泛型类型is类型的模板]()
- why need 泛型
	- to代码复用
		- 如：模板方法、模板类型

## 泛型和非泛型的区别

![泛型和非泛型的区别]()

### 使用上的区别

### 底层实现上的区别
- 泛型是什么实现的
- 



## c#允许的泛型种类
- C#提供了5种泛型：
	- 类
	- 结构
	- 接口
	- 委托
	- 方法

### 泛型类

### 泛型结构

### 泛型接口

### 泛型委托

### 泛型方法

## 类型参数的约束






# 枚举器|迭代器|协程


## 迭代器

- 迭代器方法有一个重要限制：在同一方法中不能同时使用 return 语句和 yield return 语句
	- 解决办法：
		1. 可以选择在整个方法中使用 yield return
		2. 选择将原始方法分成多个方法，一些只使用 return，另一些只使用 yield return







# 异常


# 属性||反射

属性是派生自 Attribute 的类




# 流程结构
## 顺序
## 分支
## 循环
## 同步-异步
- is什么
- why need 异步
	- 新型应用广泛使用文件和网络 I/O，默认情况下 I/O API 一般会阻塞，导致糟糕的用户体验和硬件利用率

- C#下 how use 异步
	- .NET 提供了执行异步操作的3种模式：
		- 基于任务的异步模式 (TAP)
			- TAP 是在 .NET Framework 4 中引入的
			- 这是在 .NET 中进行异步编程的推荐方法
		- 基于事件的异步模式 (EAP)
		- 异步编程模型 (APM) 模式（也称为 IAsyncResult 模式）
			- 不建议新的开发使用此模式，why??

### 基于任务的异步模式 (TAP)





## 并发-并行
### 多进程
### 多线程
### 协程
### SIMD
## 事件机制(发布者-订阅者)






# 疑问

## 方法的输入形参可以有哪些种类的成员？？



