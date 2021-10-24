[toc]


# 一、概论
## 生命周期&&编程范式

### C++生命周期

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\生命周期.jpg" style="zoom:30%;" />

#### 预编译期间能看到的

- 

#### 编译期间能看到的

- 编译阶段的特殊性在于，它看到的都是 C++ 语法实体，比如 typedef、using、template、struct/class 这些关键字定义的类型，而不是运行阶段的变量。


### C++5种编程范式


<img src="C:\Users\king-kong\Desktop\要做的事情\picture\5种范式.jpg" alt="关系图" style="zoom:33%;" />


#### 面向过程

- 核心思想是“命令”，通常就是(顺序、分支、循环)执行的语句、子程序（函数），把任务分解成若干个步骤去执行，最终达成目标

#### OO

- 核心思想是“抽象”和“封装”
- 倡导的是把任务分解成一些**高内聚低耦合**的对象，这些对象互相通信协作来完成任务。它强调对象之间的关系和接口，而不是完成任务的具体步骤。

#### GP

- 核心思想是“一切皆为类型”，或者说是“参数化类型” “类型擦除”
- 使用模板而不是继承的方式来复用代码，所以运行效率更高，代码也更简洁。
- 在 C++ 里，泛型的**基础就是 template 关键字**，然后是庞大而复杂的标准库，里面有各种泛型容器和算法，比如 vector、map、sort，等等。
- 只能以源码的方式提供？不能以库的分离-链接方式？？
	- Egein

#### 模板元

- 核心思想是“类型运算”
- 操作的数据是编译时可见的“类型”，所以也比较特殊，代码只能由编译器执行，而不能被运行时的 CPU 执行。
- 模板元编程是一种高级、复杂的技术，C++ 语言对它的支持也比较少，更多的是以库的方式来使用，比如 type_traits、enable_if 等


#### 函数式

- 核心思想是“一切皆可调用”，通过一系列连续或者嵌套的函数调用实现对数据的处理。
- 所谓的“函数式”并不是 C++ 里写成函数的子程序，而是数学意义上、无副作用的函数
- 函数式早在 C++98 时就有少量的尝试（bind1st/bind2nd 等函数对象），但直到 C++11 引入了 Lambda 表达式，它才真正获得了可与其他范式并驾齐驱的地位。



## 宏定义&&条件编译(预编译阶段)



## 静态&&动态检查(编译-运行阶段)

- 编译阶段的特殊性在于，它看到的都是 C++ 语法实体，比如 typedef、using、template、struct/class 这些关键字定义的类型，而不是运行阶段的变量。
	- 只能看到编译时的常数和类型，看不到运行时的变量、指针、内存数据等

- 和预处理阶段（use预编译指令来控制预编译器）一样，在编译器阶段(use 编译器指令 -> 控制编译器)

### 属性（attribute）

- 1. 在 C++11 之前，标准里没有规定这样的东西，但 GCC、VC 等编译器发现这样做确实很有用，于是就实现出了自己“编译指令”。
	- 在 GCC 里是“__ attribute __”，
	- 在 VC 里是“__declspec”。
	- 不过因为它们不是标准，所以名字显得有点“怪异”。

- 2. 到了 C++11，标准委员会终于认识到了“编译指令”的好处，于是就把“民间”用法升级为“官方版本”，起了个正式的名字叫**“属性”**。
	- 你可以把它理解为给变量、函数、类等“贴”上一个编译阶段的“标签”，方便编译器识别处理。

- 3. “属性”没有新增关键字，而是用两对方括号的形式“[[…]]”，方括号的中间就是属性标签（看着是不是很像一张方方正正的便签条）。
	- 在 C++11 里只定义了两个属性：“noreturn”和“carries_dependency”，它们基本上没什么大用处。
	- C++14 的情况略微好了点，增加了一个比较实用的属性“deprecated”，用来标记不推荐使用的变量、函数或者类，也就是被“废弃”。
	- 目前的 C++17 和 C++20 又增加了五六个新属性，比如 fallthrough、likely，但我觉得，标准委员会的态度还是太“保守”了，在实际的开发中，这些真的是不够用

```
[[noreturn]]              // 属性标签
int func(bool flag)       // 函数绝不会返回任何值
{
    throw std::runtime_error("XXX");
}
```

```
[[deprecated("deadline:2020-12-31")]]      // C++14 or later
int old_func();

于是，任何用到这个函数的程序都会在编译时看到这个标签，报出一条警告：
warning: ‘int old_func()’ is deprecated: deadline:2020-12-31 [-Wdeprecated-declarations]

```

- 5. 好在“属性”也支持非标准扩展，允许以类似名字空间的方式使用编译器自己的一些“非官方”属性，
	- GCC 的属性都在“gnu::”里。
		- deprecated：与 C++14 相同，但可以用在 C++11 里。
		- unused：用于变量、类型、函数等，表示虽然暂时不用，但最好保留着，因为将来可能会用。
		- constructor：函数会在 main() 函数之前执行，效果有点像是全局对象的构造函数。
		- destructor：函数会在 main() 函数结束之后执行，有点像是全局对象的析构函数。
		- always_inline：要求编译器强制内联函数，作用比 inline 关键字更强。
		- hot：标记“热点”函数，要求编译器更积极地优化。
	- VC里的属性：
		- 1. 

### 断言
- “属性”像是给编译器的一个“提示”“告知”，无法进行计算，还算不上是编程，而接下来要讲的“静态断言”，就有点编译阶段写程序的味道了。
#### 动态断言（assert ）
- 1. assert 虽然**是一个宏**，但是在**预处理阶段不生效**，而是在**运行阶段才起作用**，所以又叫“动态断言”。
	- 用来控制运行阶段的报错
- 2. 当程序（也就是 CPU）运行到 assert 语句时，就会计算表达式的值，如果是 false，就会输出错误消息，然后调用 abort() 终止程序的执行。
- 3. 使用assert必须```#include <cassert>```


#### 静态断言（static_assert）

- 1.  static_assert，不过它**是一个专门的关键字**，而不是宏。因为它**只在编译时生效**，**运行阶段看不见**，所以是“静态”的。
	- 用来控制编译阶段的报错
- 2. 编译器看到 static_assert 也会计算表达式的值，如果值是 false，就会报错，导致编译失败。


##### 静态断言的用途：

- 1. 这节课刚开始时的斐波拉契数列计算函数，可以用静态断言来保证模板参数必须大于等于零：

```
template<int N>
struct fib
{
    static_assert(N >= 0, "N >= 0");

    static const int value =
        fib<N - 1>::value + fib<N - 2>::value;
};
```

- 2. 要想保证我们的程序只在 64 位系统上运行，可以用静态断言在编译阶段检查 long 的大小，必须是 8 个字节（当然，你也可以换个思路用预处理编程来实现）：
```
static_assert(
  sizeof(long) >= 8, "must run on x64");
  
static_assert(
  sizeof(int)  == 4, "int must be 32bit");
```

- 3. static_assert 运行在编译阶段，只能看到编译时的常数和类型，看不到运行时的变量、指针、内存数据等，是“静态”的，所以不要简单地把 assert 的习惯搬过来用。
```
char* p = nullptr;
static_assert(p == nullptr, "some error.");  // 错误用法
```

- 4. 在泛型编程的时候，怎么检查模板类型呢？比如说，断言是整数而不是浮点数、断言是指针而不是引用、断言类型可拷贝可移动……
	- 配合标准库里的**type_traits**，它提供了对应这些概念的各种编译期“函数”
```
// 假设T是一个模板参数，即template<typename T>

static_assert(
  is_integral<T>::value, "int");

static_assert(
  is_pointer<T>::value, "ptr");

static_assert(
  is_default_constructible<T>::value, "constructible");

```



# 二、语言特性

## auto/decltype：为什么要有自动类型推导？
## const/volatile/mutable：常量/变量究竟是怎么回事？
## smart_ptr：智能指针到底“智能”在哪里？
## exception：怎样才能用好异常？
## lambda：函数式编程带来了什么？



# 三、标准库

## 字符串

## 容器

## 算法

- C++ 里的算法，指的是工作在**容器**上的一些**泛型函数**，会对容器内的元素实施的各种操作。

- 算法只能**通过迭代器**去**“间接”访问容器以及元素**，算法的能力是由迭代器决定的。
	- 1. 间接的好处:
		- 这就是**泛型编程**的理念，与OO正好相反，**分离了数据和操作**。算法可以不关心容器的内部结构，以一致的方式去操作元素，适用范围更广，用起来也更灵活。
	- 2. 间接的弊端：
		- 因为算法是通用的，免不了对有的数据结构虽然可行但效率比较低。
		- 所以，对于 merge、sort、unique 等一些特别的算法，容器就提供了专门的替代成员函数（相当于特化），


- 迭代器：
	- 1. C++ 里的迭代器也有很多种，比如输入迭代器、输出迭代器、双向迭代器、随机访问迭代器，等等
	- 2. 可以把它简单地理解为另一种形式的“智能指针”，只是它强调的是**对数据的访问**，而不是生命周期管理。
	- 3. 容器一般都会提供 begin()、end() 成员函数，调用它们就可以得到表示两个端点的迭代器，具体类型最好用 auto 自动推导，不要过分关心：
		- 建议使用更加通用的全局函数 begin()、end()，虽然效果是一样的，但写起来比较方便，看起来也更清楚（另外还有 cbegin()、cend() 函数，返回的是常量迭代器）：
	- 4. 迭代器和指针类似，**也可以前进和后退**，但你不能假设它一定支持“++”“--”操作符，**最好也要用函数来操作**，常用的有这么几个：
		- distance()，计算两个迭代器之间的距离；
		- advance()，前进或者后退 N 步；
		- next()/prev()，计算迭代器前后的某个位置

```
vector<int> v = {1,2,3,4,5};    // vector容器
auto iter1 = v.begin();        // 成员函数获取迭代器，自动类型推导
auto iter2 = v.end();
```

```
auto iter3 = std::begin(v);   // 全局函数获取迭代器，自动类型推导
auto iter4 = std::end(v);
```


```
array<int, 5> arr = {0,1,2,3,4};  // array静态数组容器

auto b = begin(arr);          // 全局函数获取迭代器，首端
auto e = end(arr);            // 全局函数获取迭代器，末端

assert(distance(b, e) == 5);  // 迭代器的距离

auto p = next(b);              // 获取“下一个”位置
assert(distance(b, p) == 1);    // 迭代器的距离
assert(distance(p, b) == -1);  // 反向计算迭代器的距离

advance(p, 2);                // 迭代器前进两个位置，指向元素'3'
assert(*p == 3);
assert(p == prev(e, 2));     // 是末端迭代器的前两个位置
```

### 常用经典算法
####  1. for_each和(lambda表达式 or 有名函数对象)
- for_each，它是手写 for 循环的真正替代品。
- 逻辑和形式上与 for 循环几乎完全相同
- 必须指定：容器范围、lambda表达式(每个元素进行的操作)
- for_each 算法的价值就体现在这里，它把要做的事情分成了两部分，也就是两个函数：一个遍历容器元素，另一个操纵容器元素，而且名字的含义更明确，代码也有更好的封装。

```
vector<int> v = {3,5,1,7,10};   // vector容器

for(const auto& x : v) {        // range for循环
    cout << x << ",";
}

auto print = [](const auto& x)  // 定义一个lambda表达式
{
    cout << x << ",";
};
for_each(cbegin(v), cend(v), print);// for_each算法

for_each(                      // for_each算法，内部定义lambda表达式
    cbegin(v), cend(v),        // 获取常量迭代器
    [](const auto& x)          // 匿名lambda表达式
    {
        cout << x << ",";
    }
);
```

#### 2. 排序算法：

- 默认的sort()：采用的是组合方式，插入、快排、，因为采用快排所以不稳定。
- 要求排序后仍然保持元素的相对顺序，应该用 stable_sort，它是稳定的；
- 选出前几名（TopN），应该用 partial_sort；
- 选出前几名，但不要求再排出名次（BestN），应该用 nth_element；
- 中位数（Median）、百分位数（Percentile），还是用 nth_element；
- 按照某种规则把元素划分成两组，用 partition；
- 第一名和最后一名，用 minmax_element。
-------
- **在使用这些排序算法时，还要注意一点，它们对迭代器要求比较高，通常都是随机访问迭代器（minmax_element 除外），所以最好在顺序容器 array/vector 上调用**。
- 如果是 list 容器，应该调用成员函数 sort()，它对链表结构做了特别的优化。
- 有序容器 set/map 本身就已经排好序了，直接对迭代器做运算就可以得到结果。
- 而对无序容器，则不要调用排序算法，原因你应该不难想到（散列表结构的特殊性质，导致迭代器不满足要求、元素无法交换位置）。
- 
-------

```
// top3
std::partial_sort(
    begin(v), next(begin(v), 3), end(v));  // 取前3名

// best3
std::nth_element(
    begin(v), next(begin(v), 3), end(v));  // 最好的3个

// Median
auto mid_iter =                            // 中位数的位置
    next(begin(v), v.size()/2);
std::nth_element( begin(v), mid_iter, end(v));// 排序得到中位数
cout << "median is " << *mid_iter << endl;
    
// partition
auto pos = std::partition(                // 找出所有大于9的数
    begin(v), end(v),
    [](const auto& x)                    // 定义一个lambda表达式
    {
        return x > 9;
    }
); 
for_each(begin(v), pos, print);         // 输出分组后的数据  

// min/max
auto value = std::minmax_element(        //找出第一名和倒数第一
    cbegin(v), cend(v)
);
```

#### 3. 查找

- 有序容器上查找：
	- binary_search
		- 二分查找。但糟糕的是，它只返回一个 bool 值，告知元素是否存在，
	- lower_bound
		- 已序容器、二分查找
		- 它返回第一个“大于或等于”值的位置
	- upper_bound


- 未排序的容器上：
	- 这些算法以 find 和 search 命名

```
vector<int> v = {1,9,11,3,5,7};  // vector容器

decltype(v.end()) pos;          // 声明一个迭代器，使用decltype

pos = std::find(                 // 查找算法，找到第一个出现的位置
    begin(v), end(v), 3
);  
assert(pos != end(v));         // 与end()比较才能知道是否找到

pos = std::find_if(            // 查找算法，用lambda判断条件
    begin(v), end(v),
    [](auto x) {              // 定义一个lambda表达式
        return x % 2 == 0;    // 判断是否偶数
    }
);  
assert(pos == end(v));        // 与end()比较才能知道是否找到

array<int, 2> arr = {3,5};    // array容器
pos = std::find_first_of(      // 查找一个子区间
    begin(v), end(v),
    begin(arr), end(arr)
);  
assert(pos != end(v));       // 与end()比较才能知道是否找到
```




# 四、进阶
## 网络通信：我不想写原生Socket

- C++ 里的几个好用的网络通信库：libcurl、cpr 和 ZMQ

### libcurl：高可移植、功能丰富的通信库

[](https://curl.se/)

- libcurl 使用纯 C 语言开发，兼容性、可移植性非常好，基于 C 接口可以很容易写出各种语言的封装，所以 Python、PHP 等语言都有 libcurl 相关的库。
- 因为 C++ 兼容 C，所以我们也可以在 C++ 程序里直接调用 libcurl 来收发数据。

### cpr：更现代、更易用的通信库

[源码](https://github.com/whoshuu/cpr)
### ZMQ：高效、快速、多功能的通信库
### Beast

## 序列化：简单通用的数据交换格式有哪些？

## 脚本语言：搭建高性能的混合系统

## 性能分析：找出程序的瓶颈


# 实战技巧
## code style

## how to write a good  类

## 多用auto声明局部变量
- for()中多用auto& 来降低开销



