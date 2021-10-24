[toc]


- 新建一个3D project后，只有 camera（main camera 默认） 和 light（direct light 默认） 两个组件


# 核心组件篇

## Rect Transform

- 1. 每个gameobject都有此部分


## Game Object


## 两个区域

### display - camera - canvas的关系

### camera的区域

- 1. 一个scene下可以有多个camera，每个camera投影到一个display上
	- 单screen: 如果多个camera同时使能，只有一个能投影到screen上(depth最小的那个)
	- 多个screen: 可以设置camera的display选项-->让不同的camera视场里的画面投影到不同的screen上

- 2. camera视场里的画面--投影到--> display有三种方式：
	- 1. 
	- 
- 3. 只有位置在camera的视场区域中的gameobject才能显示
	- ru:我之前将一个particle system 放置到canvas下(心想，canvas区域的都能投影到camera上，应该只要在这个区域，particle system也能被看到)，但是，因为particle system没有位于camera区域内而没能显示 <-- 因为，canvas显示到screen的方式是强制的，所以，canva一般的位置不位于camera区域下，如下图：

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\camera-canvas.PNG" alt="canvas和camera区域的位置" style="zoom:40%;" />


- 4. 将gameobject作为camera的子对象
	- 好处：
	- 缺点：


### canvas的区域

- 1. 同一scene下可以有多个canvas
- 2. 以canvas来基元来投影到display上
	- 每个canvas可以指定到一个display上




# UI篇



## ui组件的层级关系

- 1. ui部分的组件必须位于canvas下
- 2. ui部分的各组件 都有 一个text子组件 来给组件贴字？？(注定要被text Mesh Pro取代？) 目前19版 Text \ Button \ InputFiled \ DropDown均有 text mesh pro版本。
- 3. 只要create UI区的组件，都会自动加入一个EventSystem，且无论加入多少组件，多少个canvas都只会有一个EventSystem, EventSystem是做什么的？？？
- 4. 





## ui组件



### EventSystem

- 是统一对UI组件进行设置的？？

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\eventsystem.PNG" style="zoom:60%;" />
	

### Toggle

- 常用的设置选项：
	- 1. interable (可交互)
	- 2. is on(默认时是否选中)
	- 3. 子组件：
		- backgroud:
			- 设置勾选框的图标
		- text:
			- 设置勾选框的名字



<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\toggle.PNG" style="zoom:50%;" />




<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\toggle-backgroud.jpg" style="zoom:50%;" />




### InputField



- inputField组件必须位于某一canvas下



![](C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\捕获.PNG)


- input filed组件主要是编写此部分




<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\inputfield.PNG" style="zoom:60%;" />





### Button



- 1. 也必须位于canvas下
- 2. button通过add text以外的子组件来改变按钮的形状，如何改变按钮的形状？？



![](C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\pure-button.PNG)



- button组件主要是编写on click部分:

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\button.PNG" style="zoom:60%;" />



### canvas

- 1. 只要是UI就一定要有一个canvas,不然也会自动加一个。如果同时有多个canvas，会怎么样？？
- 2. 组件如果不放在canvas下则无法被渲染（无法被camera投影到屏幕上）




<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\未放canvas下.PNG" style="zoom:40%;" />



<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\放canvas下.PNG" style="zoom:40%;" />




#### 3. 改变Game视窗的大小，为什么会改变 canvas的Width 和 Height

- canvas render模式有三种：
	- 1.screen space - overlay
	- 2.screen space - camera
	- 3.world space

- 只有在world space下，改变Game 大小，canvas不会改变，在另两种模式下都会自动改变




###  Scroll View


<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG-Unity\scrow view.PNG" style="zoom:60%;" />


### Drop Down



## 使用纯脚本编写UI程序
[学习链接](https://docs.unity3d.com/cn/2020.3/Manual/gui-Basics.html)

- 1. unity内置的IMGUI系统
- 


## 使用拖放UI组件+脚本控制的方式编写UI




# 数据传递

## 同一scene--不同脚本间传值

### 不同cs脚本间传值（挂载到gameobject   or  未挂载到）

- 1. 使用static成员共享的方式
	- 不同地方的更新的速度？？有没有延时误差？？
	- 

- 2. 


### 不同gameobject之间


## 不同scene间

- 通过static成员可以，因为static像全局变量一样，只要class一旦创建好，static就可以在全局使用（unity下的全局是all项目？？（all scene，all gameobject均属于全局下的局部？））
	- 如：socket中使用静态ip、port来从welcomeScene传值到connectScene




# 小鸡穷

- 1. 在多个脚本之间、多个gameobject，可以使用static型的信号量来构建顺序和通知？？
	- 能不能将event事件def成static静态的？？？
- 


# 奇怪的bugg

- 1. 在其中一个继承了monobehavior的类的start()中使用 System.Threading.Thread.Sleep() + while() 为什么会导致卡死？？别的脚本的也无法运行下去？
- 2. 