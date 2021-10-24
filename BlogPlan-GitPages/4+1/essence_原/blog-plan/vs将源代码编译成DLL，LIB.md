[toc]

# 使用vs将源代码编译成DLL，LIB

## 将C++ -> DLL , LIB

### C++ -> DLL

#### **桌面应用向导方式**

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\111.PNG" style="zoom:30%;" />

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\222.PNG" style="zoom:30%;" />

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\333.PNG" style="zoom:30%;" />

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\444.PNG" style="zoom:45%;" />


	最后一步，在vs工具栏中，生成->生成XXXXX
	注意：
	1.因为生成的是DLL，是不可以直接调试运行的，如果直接调节会报错。
	2.这种方式生成DLL的时候，同时还会生成LIB（静态链接库）
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\555.PNG" style="zoom:50%;" />


#### **直接使用vs2019的DLL生成方式**

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\666.PNG" style="zoom:45%;" />

#### **直接使用vs2019的LIB生成方式**

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\777.PNG" style="zoom:45%;" />



# 
## 1. 什么可以编译成库(DLL、LIB)?-----what
### 将一组函数编译成库
方法使用_declspec(dllexport)修饰符

1. 但是为什么 全局变量不需要特殊的修饰，就可以在别的地方随意使用？？
2. 而且_declspec(dllexport)修饰的方法，也可以所以调用别的_declspec(dllexport)修饰的方法，


```
	_declspec(dllexport) void closeAllKinect()
		{
			//closeAzureKinect();
			//closeAzureKinect2();
			//closeAzureKinect3();
```


### 将一组class(封装在一个namespace中)编译成库

- 1. 由于namespace的分布式合并特性，等价于
```
//using here

using System;
using System.Collections.Generic;
using System.Net.Sockets;
using System.Net;
using System.Text;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;


namespace {

public class NetPacket{
		//code here
}

public class NetworkManager{

		//code here
}

public class Tcppeer{
		//code here
}

}

```

- 2. 上面的编译成库是，双方全使用C#语法，如果：双端用不同的语法(ru：用C++编译成库，C#来使用？)还能使用吗？
- 3. .dll是语言无关 only 抽象功能一一对应的吗？？

```
#include <iostream>
#include <vector>

using namespace std;

namespace cv{

public class1{
}

public class2{
}

public class3{
}

}

```

## 2. 通过什么方式编译成库--------how





## 3. 怎么使用库文件？---------how to use



## 4. 各种错误

### 1. unity中添加xxx.dll后，在脚本中using yyyyy; 后使用yyyyy中的class，报The type or namespace name 'TCPPeer' could not be found (are you missing a using directive or an assembly reference?)

- 1. 考虑unity的.net版本&&vs编译dll时采用的.NET版本是否相同
```
在edit-> project setting-> player -> other seting 
```
- 2. 




# 疑问

## 1. vs既然可以将xx.cs xx.cpp编译成dll库，为什么不能将opencv(一组cpp文件）编译成库？？

