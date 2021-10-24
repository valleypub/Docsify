[toc]

# 学习目标
- js编程语言
- 面向对象编程(!=基于对象编程)
- WebAPI
	- DOM
	- BOM
- js开源框架
	- jQuery
	- ECharts
	- ES6



## DOM
### DOM概述
- 是什么
	- 文档对象模型
	- 是一个w3c规定的标准编程接口
		- 通过这些接口可以改变网页的内容、结构、样式etc
- why need it
#### DOM树
- 文档
- 元素
- 节点
- 上述一切皆看作对象，故称为文档对象模型


### 获取元素
#### 1

document.getElementById();
document.getElementsByTagName();

- 返回的这些元素组成的对象集合，以伪数组的形式存储
	- 伪数组？？

element.getElementsByTagName();
只会获取元素内的tag匹配的，而不是document级别的

- 注意
	- 按id搜的，id是要自己添加的一个标记
	- tagname则是标签原本的名字

#### html5新增加的
document.getElementsByClassName()

一个统一的基于选择器的
document.querySelector()
	- 返回指定选择器的第一个元素对象
	- 里面的选择器要加符号
		- .box  class用.
		- #nav  id用#
		- 
document.querySelectorAll()

#### 获取特殊的元素
- 给body,html标签加id标识，然后使用前面的方法可以获取
- 用document.querySelector('body')行吗？like 获取li标签元素那样
- 因为这两个标签实在是太特殊了，直接提供了两种专门的获取方式
	- 获取html元素对象
		- var htmlEle = document.documentElement;
	- 获取body元素
		- var bodyEle = document.body;

### 操作元素
#### 改变元素内容
element.innnerText
这个element实际中要换成获取的元素对象

element.innerHTML

- innnerText 和 innerHTML的区别	
	- 识不识别html标签：如：<strong></strong>
		- 如：有的时候想要在字符串中直接使用html标签来修改文字属性 ，element.innnerText = ' <strong>今天是</strong>：2021，7，10'
	- innnerText 是非标准的ieee推荐的，innerHTML是标准的w3c推荐的
	- 更不更改原有样式
		- innerHTML
			- 保留空格和换行
		- innerText
			- 只取出text，不保留空格和换行
- 注意：
	- 这是object类中拥有的成员？？不然为啥每一种标签元素对象都能使用？？
	- 还有哪些操作的方式
#### 改变元素属性


### 节点操作

### 事件基础
#### 事件三要素：事件源|事件类型|事件处理程序
- 事件源
	- 如：按钮
- 事件类型
	- 如何触发，触发的方式：按下出发onclick、经过出发、
	- onclick
	- onfocus
	- onblur
	- onmouseover
	- onmouseout
- 事件处理程序
	- 类似于C#中的时间的内部委托队列，要提前向发布者订阅注册的

#### 事件的常规搭配步骤
1. 获取事件源
2. 绑定事件
- 每一个元素对象均有事件成员吗？？处于object基类的？？
3. 往事件注册行为
4. 触发事件
##### button做事件的流程
![]()

#### 养成分析事件三要素的习惯
1. 用的事件源是什么
2. 用的事件类型是什么
3. 用的


## debug技巧

console.log()
console.dir()