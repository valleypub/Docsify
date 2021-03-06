[toc]

```
1. 下面这些是我在学习-使用，c/c++、c#、python时接触到的一些common 、abstract的concept
2. 不同语言在实现这些concept的时候具体实现细节不相同
3. 甚至同一语言在不同os上实现细节也不相同,ru: socket数据传输，c/c++方式，在unix和windows下的具体细节不同，但是流程框架是一样的
4. 但是这些实现都是围绕这些concept的实现，都实现了这些concept
```

# 类型相关的

## 泛型机制

- 编译器是怎么实现的这个concept的？
- 

## 类型推断机制

- 编译器怎么实现这个concept的？



## 整数溢出机制

### C中的整数溢出机制

#### 无符号整形
- 对原始类型最大值取模
	- 对于unsigned整型溢出，C的规范是有定义的——“溢出后的数会以2^(8*sizeof(type))作模运算”，也就是说，如果一个unsigned char（1字符，8bits）溢出了，会把溢出的值与256求模。
```
#include <stdio.h>
int main(int argc, const char * argv[]) {
  // insert code here...
  unsigned char x;
  x = 128 + 130;
  printf("%d\n",x);  
}

上面代码会输出：2，258以256为模的结果值是2。

```

#### 有符号整型

- 有符号整型溢出又可分为向上溢出和向下溢出。
- 

## 扩充机制
### 零扩充
### 符号扩充

# 其他

## 保存程序运行时的临时数据

![]()

### 1. 想保存的是什么
- 1. 普通变量？字符串？

```
都是直接以字符串的形式保存的？
```

- 2. 普通对象(包含很多成员（属性、方法）的那种)？

+ 序列化机制
+ + 二进制序列化 配合 字符串读写
+ + jason序列化
+ + xml序列化

+ 


### 2. how to 读写(保存)
- 1. stream的方式

- 2. 文件的方式

### 3. 保存的形式
- 1. jason格式，专为保存对象而引入的字符串文本格式？？
```
1. JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。
2. 该文档说，从结构上看，所有的数据(data)最终可以分解成三种类型：
第一种类型是标量scalar，也就是一个单独的字符串string或数字numbers，比如“成都”这个单独的词。
第二种类型是序列sequence，也就是若干个相关的数据按照一定顺序并列在一起，又叫做数组array，或者列表list，比如“成都，重庆”。
第三种类型是映射mapping，也就是一个名/值name/value，即数据有一个名称，还有一个与之相对应的值，这又称作散列hash或字典dictionary，比如“蓉城：成都”。
是啊，原来数据构成的最小单元经如此简单。难怪在编程语言中，只要有了数组array和对象object就能够存储一切数据了。

```

#### 


## 解决高速cpu与龟速IO外设的速度不匹配问题
```

```
![]()


## 进程间的通信问题

- 1. **同一进程的不同线程is共享all data的**，所以不存在线程间的通信问题(不同进程间的线程通信问题，本质上升为了不同进程间的通信问题)
- 2. **不同进程是不共享数据的**，相互隔绝。even,同一进程fork()后，这两个进程除了由于fork()复制了一份数据使fork()前的数据一样、但是也是独立的两份外，fork()后就相当于是两个进程了，不再共享数据

![]()


## 事件--注册机制
```

```

### 单个方法注册

### 方法组(委托对象)注册
- 委托 == 一组标签、返回类型形同、有序的方法



## 异步机制

- 1. 所有的异步机制都是基于线程池的线程操作？？？

![C#中的异步机制]()

- 2. 使用异步制作一个小程序

- 3. 异步编程是一项关键技术，可以直接处理多个核心上的阻塞 I/O 和并发操作

### C#中



## 并发机制(多线程、多进程concept)
```

```
### 1. 为什么多线程、多进程

### 2. 带来的好处

### 3. how to use

### 4. 引入的问题

#### 读写保护机制

##### lock锁机制

##### 




## 线程池？



## 面向硬件-面向过程-GP-OO-组合

```
不同的应用领域，催生不同的编程方式 --->每一个领域都有其适合的编程方式
```


## 作用域机制 - > 生命周期

- 1. 大大降低标识符的命名冲突问题，防止全局污染 -->依靠局部变量对全局的名字覆盖机制

```
golang中，
函数内定义的的变量，包括形参都是局部变量
函数外定义的是全局
C++中
c#中：
只要属于块内(pure块、语句块、函数块)定义的，是局部的
不属于任意块内(class、struct等后面跟的{}不是块)的是实例变量or静态变量，是C#中的最外层了，因为OO不允许裸的

```

- 2. 


## 重载机制
- 实现	!=	重载	!=	重写(virtual-override)

### op重载

### 方法重载



## 静态联编--动态联编



## 编译器优化机制

1. go中的编译器有 内存分配的优化机制 : 
2. C++的编译器有const的符号表加速，编译重叠




## OO中 都有哪些 可以is静态的

### C#中
#### 1. 静态类
- 1. 和接口、抽象类一样，静态类不能被实例化
- 2. 静态类的所有成员都是静态的
```
因为，静态类不能被实例化 -> 不能实例化的实例成员有什么意义呢(实例成员只有类实例化后才能被使用)
```

- 3. 再类前 + static， 在all内部成员 前 也都+ static
- 4. 一些不想被别人实例化成多个副本的类，如只能有一个公共副本的作为common的工具类来使用，
- 
#### 2. 静态字段
#### 3. 静态方法
#### 4. 静态构造函数
- 1. 静态类&&非静态类都能创建静态构造函数
- 2. 静态构造函数is for 静态成员服务的
- 3. 声明静态构造函数不需要添加形如public的访问限制付：
构造函数 声明称private形的不就没意义了吗，因为构造函数只能在类外使用啊
```
	static	类名( ) {
}
```



## 内存池(一种缓存技术)

- 1. Go再启动程序时，会向操作系统申请一大块内存，作为内存池
- 2. Go的分层级内存管理由，mcahe、mcentral、mheap三大组成
- 3. TCMalloc



## 缓存概念(池的思想)
### 线程池
### 内存池

## 隔离(解决冲突的一种思想)
- 冲突了 -> 外加一层 -> 将冲突的变为各个不同的小区间

### 命名空间
1. C中没有命名空间的思想
2. C++的命名空间
3. C#的命名空间

### 容器is基于命名空间来实现的

### 公网ip -> 私有ip 
- 通过划分一些私有的、可复用的段 -> 解决冲突问题



## 类多继承(C++) vs {类单继承+接口多继承}(C# JAVA)
- 为什么接口可以多继承，类不可以多继承，这样做保护了什么or避免了什么？？ 和java一样都是通过接口多继承来代替类的多继承 ???






## GUID（全局统一标识符）
- 是什么
	- GUID（全局统一标识符）是指在一台机器上生成的数字，它保证对在同一时空中的所有机器都是唯一的。
	- 生成算法很有意思，用到了以太网卡地址、纳秒级时间、芯片ID码和许多可能的数字
	- GUID的唯一缺陷在于生成的结果串会比较大。” 
	- 通常平台会提供生成GUID的API。
		- 在 Windows 平台上，GUID 应用非常广泛：注册表、类及接口标识、数据库、甚至自动生成的机器名、目录名等。
		- 一个GUID为一个128位的整数(16字节)，在使用唯一标识符的情况下，你可以在所有计算机和网络之间使用这一整数。
		- GUID 的格式为“xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx”，其中每个 x 是 0-9 或 a-f 范围内的一个十六进制的数字。例如：337c7f2b-7a34-4f50-9141-bab9e6478cc8 即为有效的 GUID 值。
		- 世界上（Koffer注：应该是地球上）的任何两台计算机都不会生成重复的 GUID 值。GUID 主要用于在拥有多个节点、多台计算机的网络或系统中，分配必须具有唯一性的标识符。
- why need it
	- 我们有些时候需要全局唯一的标识符来(作为各种name(文件名、线程名、)、)等，guid就是解决这个需求的。
		- GUID（全局统一标识符）是在一台机器上生成的数字，它保证对在同一时空中的所有机器都是唯一的。
		- 世界上（Koffer注：应该是地球上）的任何两台计算机都不会生成重复的 GUID 值。GUID 主要用于在拥有多个节点、多台计算机的网络或系统中，分配必须具有唯一性的标识符。

- how use it
	- .NET中使用GUID
	- C++中使用 GUID
	- JAVA中使用GUID
