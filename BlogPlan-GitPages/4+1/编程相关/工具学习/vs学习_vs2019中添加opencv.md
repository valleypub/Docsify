[toc]

# vs2019中添加opencv
## 下载opencv库
	根据自己的需求，选择相应版本的opencv进行下载
[opencv release版本的官方下载link](https://opencv.org/releases/)
## 配置opencv环境变量（windows中添加opencv）

	要添加的部分
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\66.PNG" style="zoom:60%;" />
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\77.PNG" style="zoom:60%;" />

	将在这两个路径添加进环境变量


## vs2019中添加opencv
	先随便新建一个测试工程（C++空项目），然后选择 视图->其他窗口->属性管理器—>Debug|x64->右键属性
### vc与vs对应图
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\33.PNG" alt="img1" style="zoom:50%;" />

### VC++目录中配置include , lib
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\11.PNG" alt="include配置" style="zoom:60%;" />


### 附加依赖项配置
	链接器->输入->附加依赖项
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\22.PNG" alt="附加依赖项配置" style="zoom:60%;" />
### 

## 将库文件放入windows的查找目录中
	要添加哪些？为什么要添加？
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\55PNG.PNG" alt="img5" style="zoom:60%;" />

### system32(x64版的)

### systemWOW(32版的)



## 只对当前项目有效的配置方式&&对所有项目均有效的配置方式

	(从父集或项目默认继承 ？？？是什么意思？)


	我们一般配置项目依赖时是通过下面的位置来配置的，但是这种配置一般只对此项目有用。

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\88.PNG" style="zoom:60%;" />

	如何让一些配置对所有的后续的项目均有效？？


	通过的是“从父项继承值”的方式，只要两个步骤：
	1.后续的项目的（include目录）（lib目录）（依赖项）均自动继承一些配置，
	2.我们只需要在这些会被自动继承的地方进行配置，则等价于完成了对所有项目的配置

### 继承值是怎么加入进去的？

	只要是在下图中的地方配置，都是会被自动继承的

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\99.PNG" style="zoom:60%;" />

### 继承值怎么删除？

	修改上图中的地方，来修改继承值



:happy:

# **以此类推**

:smile:



# 往vs中添加任意别的库 

## **1.将bin文件夹配置入 windows环境变量**

## **2.将include对应的dll文件添加进system32 or systemWOW**
	why 非带是dll？？不是同样有lib版本的吗？？

## **3.配置vs的属性**

### **3.1 配置include目录**

### **3.2 配置库目录**

### **3.3 配置附加依赖项**

**3** 中的配置 又分为 **一次性配置** 和 **永久性配置**

## **一次性配置**

## **永久性配置**

	通过继承来设置的


​	
​	

# vs中添加libjpeg-turbo库

## 1. 下载vs上可用的版本的库
```
不知道why同样是.exe生成的库，为什么vc64版的(lib下时Lib)可用，gcc64的(lib下时.dll .dll.a)不可用

```

## 2. 配置的三步法:

### 1. bin--环境变量

### 2. 添加include、lib目录

### 3. 附加依赖项设置&&将.lib文件copy to system32 &&systemWOW

## 3. 将设置设为永久的



# vs属性配置器
## 附加依赖项是什么???
```
为什么只能链接lib文件???
dll文件在什么地方配置？？？
```

要想在vs中使用库文件 ， 使用Lib版本的，通过附加依赖项可以

dll版本的目前还没找到办法:

