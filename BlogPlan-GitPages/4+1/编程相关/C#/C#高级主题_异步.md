[toc]


## awit运算符

[ awai表达式官方参考](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/language-specification/expressions#await-expressions)
[await运算符官方参考](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/await)

Await 运算符的用途是在等待的任务完成之前挂起封闭异步函数的执行，然后获取其结果。

### Await表达式

- await t表达式合法 需要 t表达式可等待，t表达式如果以下包含其中一项，则表达式为可等待：
	- t 属于编译时类型 dynamic
	- t 具有调用的可访问实例或扩展方法 GetAwaiter ，其中不包含任何参数和类型参数，以及 A 以下所有保留的返回类型：
		- A 实现接口 System.Runtime.CompilerServices.INotifyCompletion (以后称为的简称 INotifyCompletion)
		- A具有类型的可访问的可读实例属性 IsCompleted``bool
		A 具有一个 GetResult 无参数且无类型参数的可访问实例方法





## Task类是什么
System.Threading.Tasks.Task 和相关类型是可以用于推断正在进行中的任务的类

- ==why Task async await总是一起按一个固定的模式来使用？？？==





# 参考文档
1. [await和同步阻塞的区别](https://www.unfish.net/archives/1009-20200512.html)




# 明天的任务
https://docs.microsoft.com/zh-cn/dotnet/standard/async-in-depth

https://docs.microsoft.com/zh-cn/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap

https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/async/#dont-block-await-instead