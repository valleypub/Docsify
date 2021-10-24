[toc]


# ES6

# BOM

# DOM
- 是什么	
	- 抽象concept上是文档对象模型
	- 实际code上是一个w3c规定的标准编程接口
		- 通过这些接口可以改变网页的内容、结构、样式etc
- why need it

## DOM树

## 获取元素
### 根据元素ID获取
document.getElementById();
### 根据标签名获取
- document.getElementsByTagName();
	- 输入参数要求：
	- 返回的是：
		- 返回的是伪数组，
### H5新增获取元素方式
- document.getElementsByClassName()
	- 输入参数要求：
	- 返回的是：

- 一个统一的基于选择器的
- document.querySelector()
	- 返回指定选择器的第一个元素对象
	- 里面的选择器要加符号
		- .box  class用.
		- #nav  id用#
		- 
- document.querySelectorAll()

### 注意
- 按id搜的，id是要自己添加的一个标记
- tagname则是标签原本的名字


## 操作元素
### 改变元素内容
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
### 改变元素属性
#### 元素属性有哪些
1. innerText	innerHTML
2. src	href
3. id	alt		title


#### 操作input表单元素属性
- why要将表单元素的属性更改单独列出来？
	- 像input这种元素，不具有像innerHTML这些属性，更改这些没有的属性对于input元素不会有效果
- 利用DOM可以操作如下表单的属性：
	- type
	- value
	- checked
	- selected
	- disabled


### 更改元素样式属性
- 是什么
	- 通过js修改元素的大小、颜色、位置等格式
- how 
	- 通过元素的样式属性来进行更改的
		- element.style方式
			- 属于行内样式，优先级更高，会覆盖掉提前设置的style样式
			- <img src="C:\Users\king-kong\Desktop\BlogPlan\picture\front_end\行内样式.PNG" alt="行内样式" style="zoom:50%;" />
		- element.className方式
			- element.className = 'newClassName' 是覆盖式的，要想保留原先的类名，use: element.className = '原className  newclassName'
			- 提前定义好一个css样式+更改元素的className
	
- 元素样式修改项目少的使用style，修改多的使用className + 提前css定义好






### 不同种类元素有不同的属性
#### 按是否内置分
##### 内置属性
- className
- id
- 
##### 自定义属性
#### 按应用场景分
![元素种类]()
##### button
- innerText	innerHTML
- 
##### text
- innerText	innerHTML

##### img
- innerText	innerHTML
- src	href
- id	alt		title
##### input
- type
	- type = 'text' 明文方式(文本框)显示value
	- type = 'passward' 密码方式遮挡value
- value
	- 可以理解为 btoon text便签的innerHTML属性的input版本
- checked
- selected
- disabled


#### 按抽象关系分
##### 通用的属性(各个元素均有的)
##### 专门的属性



#### 操作元素属性
##### 获取元素属性
1. 使用__element.属性__获取元素内置属性
2. 使用__element.getAttribute()__
##### 移除元素属性
element.removeAttribute()
##### 增加元素属性
##### 设置元素属性
1. element.属性名 = ' '
2. element.setAtrribute()
3. 



### 元素的样式属性(style)的值
- backgroundColor
- display
	- display = 'none' 隐藏元素
	- display = 'block' 显示元素
- background
- backgroundPosition 
	- 使用此属性制作循环精灵图
- backgroundImage
	- 百度换肤就是使用事件更换的这个
- color
	- '#333' 浅色
	- '#999' 深色

### 操作元素的实际案例
#### 制作精灵图
#### 百度换肤
#### 表格隔行换色
#### 表单全选|取消全选

#### tab栏切换


- 注意
	- 一个个给需要的元素添加事件太麻烦，使用 __元素选择器 -> 伪数组 + 遍历__给每一个符合条件的元素来进行添加事件


# 学习js的模式
## 学习js内置对象的模式
1. 这个对象是模拟什么的
2. 
## 学习webAPI的模式
1. 是干什么的
2. 输入是什么
3. 返回的是什么
