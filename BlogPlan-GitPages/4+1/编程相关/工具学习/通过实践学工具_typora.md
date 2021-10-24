[toc]

# 问题&功能联想
**tab键开启的 代码段区间内 为什么不可以使用mardown的语法？？**
	**不可用**



# 第一段使用的命令(先用起来，熟悉它)
```
# 系列

__加粗__ **加粗**

[]()

![]()

缩进系列(- 1. )


```


# 第二阶段(第一阶段不够的，完善它)

[1. md内跳转](# 问题&功能联想)


----
2. 分割线

----


3. 图片的居左、居中、居右

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg" alt="3. 图片居中" style="zoom:25%; float: left;" />

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg" alt="3. 图片居中" style="zoom:25%; float: center;" />

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg" alt="3. 图片居中" style="zoom:25%; float: right;" />

4. 图片的同一绝对尺寸 + 位置
	绝对尺寸，默认是居中的

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg"  width = "80" height = "60" />

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg"  width = "80" height = "60" style=" float: right;" />

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg"  width = "80" height = "60" style=" float: center;" />

<img src="C:\Users\king-kong\Pictures\BingPicture\033015e262724a588464e58d7d73c11a_480.jpg"  width = "80" height = "60" style=" float: left;" />


4. 使用表情
	使用 ```:``` + 一个字母来提示： 如： ```:s```
	
	:scream_cat:
	
	使用微软自带的 win + ```.```。
	
	🤢


5. Toggle List
- [ ] a task list item
- [x] list syntax required
- [x] normal **formatting**, @mentions, #1234 refs
- [x] incomplete
- [ ] completed


6. ==高亮功能的使用==


7. 表格的使用
| 列1|列2|列3|
|---|---|---|
|康海泉|92|98|


8. 使用mermaid画图
	1. 先输入召唤出 mermaid输入框
	2. 在框中输入mermaid命令来画图，如：

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```


# 第三阶段(形成自己的风格，这些就是经验和审美的积累了)

- typora的主题是可以自己配置的，本质上是基于 html css js三件套
	- 内置的几个主题就是下载的别人提前设计好的css样式，这个样式我们可以用别人的，也可以自己搭配设计，只需要将css文件置于C:\Users\king-kong\AppData\Roaming\Typora\themes目录下即可


## 风格1

- 这是第一段
	1. 第一点
		第1.1点
		第1.2点
	2. 第二点
		第2.1点
	3. 第三点


- 这是第一段
	- 第一点
		- 第1.1点
		- 第1.2点
	- 第二点
		- 第2.1点
	- 第三点