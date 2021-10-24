[toc]



# 目录


### 预编译指令

#### #pragma 

- #pragma once
	- 防止同一文件被多次#include,   == #ifndef #define #endif那一套
	- 

#### #define用法:

- 1. 代码段短小 2.需重复大量使用的  函数 ，写成宏表达式，表达式只有一个返回值  

```
	#define RGB2Y(r,g,b) \
	((unsigned char)((66 * r + 129 * g + 25 * b + 128) >> 8) + 16)
	#define RGB2U(r,g,b) \
	((unsigned char)((-38 * r - 74 * g + 112 * b + 128) >> 8) + 128)
	#define RGB2V(r,g,b) \
	((unsigned char)((112 * r - 94 * g - 18 * b + 128) >> 8) + 128)

```

### 泛化的形式:

```
    #define K4A_DECLARE_HANDLE(_handle_name_)                                                                              \
        typedef struct _##_handle_name_                                                                                    \
        {                                                                                                                  \
            size_t _rsvd; /**< Reserved, do not use. */                                                                    \
        } * _handle_name_;


配合:
	K4A_DECLARE_HANDLE(k4a_image_t);	
```

### 指针

#### 内存泄露问题

- 局部内使用普通变量不容易造成内存问题。
	- 因为局部的是压入栈，每次用完会自动出栈(== 自动释放，gc)
- 局部内使用**指针**却会造成内存泄漏（永不被释放）
	- 给未初始化只声明的指针指向的地址赋值时，系统会自动给其分配存储空间，且不会被自动释放？？
```
void swap2(int *p,int *q)
{
    int *temp;
    *temp=*p;
    *p=*q;
    *q=*temp;
}
```

#### 指针&&数组的区别

- 数组名 == 常指针
```
Type arrName[100];

arrName <==> is const Type* 类型的指针


char** argv   == char* argv[] // 每个argv[i] is char*类型的

```

- 字符数组和字符串常量的区别
	- 作为局部变量时，字符数组和字符串常量的主要区别就是其生命周期不同。字符数组保存在栈中，所以在函数调用结束时就被销毁了，字符串常量是保存静态存储区域中，

```
char *strA()
{
    char *str = "hello world";
    return str;
}
char *strB()
{
    char str[] = "hello world";
    return str;
}
```


#### 指针与引用的区别

- 非空区别。在任何情况下都不能使用指向空值的引用。因此如果你使用一个变量并让它指向一个对象，但是该变量在某些时候也可能不指向任何对象，这时你应该把变量声明为指针，因为这样你可以赋空值给该变量。相反，如果变量肯定指向一个对象，例如你的设计不允许变量为空，这时你就可以把变量声明为引用。不存在指向空值的引用这个事实意味着使用引用的代码效率比使用指针要高。

- 合法性区别。在使用引用之前不需要测试它的合法性。相反，指针则应该总是被测试，防止其为空。

- 可修改区别。指针与引用的另一个重要的区别是指针可以被重新赋值以指向另一个不同对象。但是引用则总是指向在初始化时被指定的对象，以后不能改变，但是指定的对象其内容可以改变。
	- 也可以使用const修改指针的可修改性
```
const int* p;
int* const p;
```




### 其他

- 同数据类型的才能进行比较(< ，>，<= 等)，如果是float型和double型变量进行比较可能会出现奇怪的问题
- this只能用于非静态成员内部，不能用于成员函数参数列表
- struct有没有静态的？？
- 在局部内（class内、函数体内、块内、）如何声明全局的变量？使用static
- 变量动态命名问题：如给多线程动态的指定变量名字，个数不能提前确定
- 无名对象机制：用于传值，Size(600,400)
- const && 指针变量的位置；
- static和extern的区别
- 三目表达式也有无能为力的时候：
```
(find(a.begin(), a.end(), t) == a.end()) ? a.push_back(t) :  ;
最后一个要放语句，如果是满足情况执行A，不满足情况不执行时，不适合用三木
三目适合 同返回值、flag的满足与否，会分开的执行两种不同的分支，不能一种不执行
```
-  xxx( const int& ransacThreshold = 3, )可以这种const型默认形参吗？？const型不是说在初始化时必须主动初始化？因为后面不能改了，只能在一开始的时候改变？
-  平时vector都是只声明不初始化配合push_back使用，要么是声明时初始化，如何声明后再进行初始化大小？？
```
vector<int> obj(size);
或
vector<int> obj;
obj.resize(size);
```

- 线程的同步与听等待：join（阻塞控制）、detach(孤儿线程)
	- 循环自动开启多线程的：命名&&听等待（同步）问题很麻烦
- vector只声明不指定长度时，只能使用引用功能&&push_back()等，而不能使用下标随机访问，因为还没有分配内存呢
- 常量做引用类型的默认初始值，必须为const型的
```
virtual void generateHList_RANSAC(const double & confidence = 0.99, const int& n = 5) {

}

//这样是错误的
virtual void generateHList_RANSAC(double & confidence = 0.99, int& n = 5) {

}

```


- 需要冒号结尾的体：struct、class、     表达式、语句
- 不需要冒号结尾的体：方法体、pure块、语句块



### ADT
#### vector
- 深拷贝
```
一、初始化构造时拷贝
vector<int> tem(list);
这种拷贝，相当于复制了一份数据，list中的数据不变。
二、assign
vector<int> temlist;
temlist.assign(list.begin(), list.end());
一样的复制了一份数据，list中的数据不变。
三、swap
vector<int> temlist;
temlist.swap(list);
将list中数据全部移到temlist中，此时list中为空了
四、insert
vector<int> temlist;
vector<int> temlist2;
temlist2.push_back(2);
temlist2.push_back(2);
temlist.insert(temlist.end(), temlist2.begin(), temlist2.end());
将temlist2中的数据，全部插入到temlist的末尾。相当于复制了一份数据

```




### class相关的

- 构造函数前不能使用 public等修饰符
- class 、struct前布恩使用public等
- C++ VS中一旦重载了别的构造函数，就不能使用默认构造函数，除非显示重载一个默认构造函数
- namespace具有分布性，同一namespace分布于不同hpp中，如果不包括对应的hpp也无法通过namespace使用


### 关键字相关的

- static与extern的区别
- const



### 从opencv源码中的学习

#### 宏de使用

- 
```
#define CV_Assert( expr ) do { if(!!(expr)) ; else cv::error( cv::Error::StsAssert, #expr, CV_Func, __FILE__, __LINE__ ); } while(0)

CV_Assert(!ssize.empty());
```
- 

