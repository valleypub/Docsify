[toc]



# C++的特点(trivals)



# 类型系统

- C++的各种类型的存储机制到底是怎么样的？？分不分引用类型(2段式存储)、值类型(1段式存储)？

## 引用
```
	int t = 5;//如果不初始化的话，编译期间会分配存储空间吗or运行期间分配？
	int& t1 = t;
	int& t2 = t;
	int& t3 = t2;
	
	int t4 = t1;//可以这样使用吗？？
```

http://c.biancheng.net/view/195.html

- 正着用-反着用
- 作为方法的输入参数-作为方法的输出参数
- 常引用
	- 被cons限制的那个引用const T&不能更改，但是主体T or 未加const限制的别的引用 可以进行更改值
	- 同一类型T的const T& 和 T& 是不同的类型
		- T& 类型的引用或 T 类型的变量可以用来初始化 const T & 类型的引用
		- const T 类型的常变量和 const T & 类型的引用则不能用来初始化 T & 类型的引用，除非进行强制类型转换，why???还是没搞懂引用究竟是什么

```
int n = 100;
const int & r = n;
int & y = n;
r = 200;  //编译出错，不能通过常引用修改其引用的内容
n = 300;  //没问题，n的值变为300
y = 500;  //
```

```
void Func(char & r) { }
void Func2(const char & r) { }
int main()
{
    const char cc = 'a';
    char c;
    const char & rcl = cc;
    const char & rc2 = c;  //char变量可以用来初始化 const char & 的引用
    char & r = cc;  //编译出错，const char 类型的常变量不能用来初始化 char & 类型的引用
    char & r2 = (char &)cc;  //没问题，强制类型转换
    Func(rcl);  //编译出错，参数类型不匹配
    Func2(rcl);  //没问题，参数类型匹配
    return 0;
}
```





## 指针



# 存储系统
- 是怎么配合compile工作的？？
## C++有几个存储区()
### 静态存储区
- 默认的全局变量，默认全局(main()一级块内 or main()外？)各种类型都是？？如结构类型变量、类类型变量、对象数组
- static修饰的变量(全局or局部)
- 
### 动态存储区
- 
### 自动存储区
- 局部的变量，各种类型都是？？如结构类型变量、类类型变量、对象数组
- 什么情况算局部？？至少在一层块内？




# 类型转换


# 泛型


# 流程结构