[toc]



# 概述

此文档记录将HTC总工程从2018移植到2020的步骤、问题和解决。


# 将两端传数据+VFX最小系统弄好

## 0985版本的
0982 -> 0985

1. 在callApp中增加ServerUrl 、 ExplainerToggle
	- 在setupPanel中增加相应的UI组件，一番设置后
	- 在CallAPPUi中增加这两个组建的引用，并写这两个组件的回调函数


2. 0985移除了0982中的UnityVideoCapturer，而我们项目中不使用自带的webcam，而是传输custom video frame，使用0982的UnityVideoCapturer类来传输数据目前是能达到要求的，但是我之前运行了一下0985中的custom video的替代方案 Input video，光是运行示例程序就很卡了，我就没敢用。
	- 先将0982版本的移植到2020上，0985的后续再说

## 0982版本的


### 讲解者端用讲解者端的来覆盖




### 参观者用参观者端的来覆盖
直接复制-粘贴 callapp  callappui  unitycallFAactory 3个脚本，发现：还有别的需要的脚本：
1. KinectRawDataEventArgs

将Multisource 更改为 ScreenSource


目前在上三个脚本中暂时禁用了的：
1. SynchronizePPTAndModelByControlFromOpposite








# 将steam VR加进来



# 将输入控制加进来



# 将内容加载加进来






# 问题
1. UI设计中使用Anchor和pivot
	- ==pivot==主要旋转时使用？？
	- 在canvas or 父UI组件上布局相对位置时使用==Anchor==
		- because-why-not中使用的布局方式是：
			1. 先设好Anchor（即：相对父UI组件的位置），如：先设为 0 1 0 1 填满
				- 每一种不同的Anchor位置，2.中都有不同的可调方式
			2. 再设置留白边界
			- 如：先设为全覆盖父UI组件(即Anchor设为 0 1 0 1)，再设置左边距、右边距、上边距、下边距
		- 这样设置的好处是：相对性。


2. 先加入webrtc再加入steamVR Plugin会出问题。改为，先加入steamVR Plugin再加入webrtc，加入webrtc插件的步骤和上述相同


# Listner端的迁移
## 先导入steamVR + webrtc0982的完整过程（第一阶段）
1. 导入steamvr
2. 导入0982
3. 打开callapp场景，禁用callapp1，只留一个callapp
4. 进入setuppanel：增添ExplainerToggle，增添ServerUrl，适当的调整位置到合适
5. 直接复制-粘贴 callapp  callappui  unitycallFAactory 3个脚本，然后将增添ExplainerToggle，增添ServerUrl，拖拽到callappui 组件的inspector panel中
	1. 会缺少KinectRawDataEventArgs，直接新建一个KinectRawDataEventArgs.cs，然后从原始工程中复制过来
	2. 会缺少DebugHelper，同样，新建+复制
	3. 会注释掉showoverlay错误的那一行，直接注释掉

6. 用各自原工程(Listener的用Lisner的替换)的替换掉UnityVideoCapturer(在Assets\WebRtcVideoChat\scripts)和UnityCallFactory

7. 此时会在UnityVideoCapture中报MultisourceManage的错误，用ScreenSource替换掉MultisourceManage


### 对于Explaner端的
多了：
1. callapp中 ppt video model的 声明 start中的引用，以及NeirongRet中这三处注释掉了
2. Syschorriz内容同步的也注释掉了：在callapp的890 901两处

不同：
lisner是将multisource对象 换成了 screensource，并且挂在其上的Multisource脚本也变了，只传屏幕截图

explaner的multisource对象不变，挂在其上的multisource脚本也不变，但是要往其上增加

而且：
1. explaner端，multisource依赖因为需要管理Azure KInect，故需要在plugins中导入相关的kinect库，
2. 原先管理多个source设备故称为multisourcemanage，现在只管理一个Kinect故应该改名为AzureKinectSourceManage

----

上述所有操作完成后，Listner端和Explainer端应分别如下图所示

----

Listener端：

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\MR_HTC从头搭建\导入steamVR和webrtc的.PNG" style="zoom:40%; float:center;" />


Explainer端：

![]()


## 导入粒子特效支持
1. 创建一个ParticleSystem对象命名为AzureKinect专门用来显示粒子


2. 将原工程的RawDataToPointCloud复制进新工程的MyScript，然后挂载在AzureKinect游戏对象上
	1. 要更改KinectEventReached下的```this.transform.name.Equals("Kinect1") && e.kinectId == 1```这一句，的Kinect1改为自建的用于显示的游戏对象的名称，这里是改为AzureKinect1


3. 将Kinect标定的结果参数文件，放在StreamingAssets文件夹下







## 导入场景内容（第二阶段）
### 导入屋子
- 将ScenePool导出的同时还要将，各个Scene渲染需要使用的avator等连带着导出，否则只有ScenePool场景里不会有屋子出现
	- why 分开导进来后，我一将avator通过unitypackage加载进来，我还没拖拽建立引用呢，他就直接自动建立引用了？？？

- 能不能自己找几个不做的模型导进来？？？？

### 制作屋内用品
1. 制作PPT游戏对象

2. 制作Watch游戏对象

## 导入实时输入控制（第三阶段）


## 导入动态内容加载（第四阶段）



# Explainer端的迁移



## 先导入steamVR + webrtc0982的完整过程（第一阶段）
1. 导入steamvr
2. 导入0982
3. 打开callapp场景，禁用callapp1，只留一个callapp
4. 进入setuppanel：增添ExplainerToggle，增添ServerUrl，适当的调整位置到合适
5. 直接复制-粘贴 callapp  callappui  unitycallFAactory 3个脚本，然后将增添ExplainerToggle，增添ServerUrl，拖拽到callappui 组件的inspector panel中
	1. 会缺少KinectRawDataEventArgs，直接新建一个KinectRawDataEventArgs.cs，然后从原始工程中复制过来
	2. 会缺少DebugHelper，同样，新建+复制
	3. 会注释掉showoverlay错误的那一行，直接注释掉

6. 用各自原工程(Listener的用Lisner的替换)的替换掉UnityVideoCapturer(在Assets\WebRtcVideoChat\scripts)和UnityCallFactory

7. 此时会在UnityVideoCapture中报MultisourceManage的错误，用ScreenSource替换掉MultisourceManage


### 对于Explaner端的
多了：
1. callapp中 ppt video model的 声明 start中的引用，以及NeirongRet中这三处注释掉了
2. Syschorriz内容同步的也注释掉了：在callapp的890 901两处

不同：
lisner是将multisource对象 换成了 screensource，并且挂在其上的Multisource脚本也变了，只传屏幕截图

explaner的multisource对象不变，挂在其上的multisource脚本也不变，但是要往其上增加

而且：
1. explaner端，multisource依赖因为需要管理Azure KInect，故需要在plugins中导入相关的kinect库，
2. 原先管理多个source设备故称为multisourcemanage，现在只管理一个Kinect故应该改名为AzureKinectSourceManage


----

上述所有操作完成后，Listner端和Explainer端应分别如下图所示

----

Listener端：

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\MR_HTC从头搭建\导入steamVR和webrtc的.PNG" style="zoom:40%; float:center;" />


Explainer端：

![]()


## 导入Azure Kinect支持


1. 将AzureKinetc相关的dll复制进新工程的Plugins下,少一个都卡不开
	k4a.dll
	depthengine_2_0.dll
2. 将源.cpp编译的dll放于Plugins下
	AzureKinectDll.dll






## 导入场景内容（第二阶段）
### 导入屋子
- 将ScenePool导出的同时还要将，各个Scene渲染需要使用的avator等连带着导出，否则只有ScenePool场景里不会有屋子出现
	- why 分开导进来后，我一将avator通过unitypackage加载进来，我还没拖拽建立引用呢，他就直接自动建立引用了？？？

- 能不能自己找几个不做的模型导进来？？？？


### 制作屋内用品
1. 制作PPT游戏对象

2. 制作Watch游戏对象

## 导入实时输入控制（第三阶段）


## 导入动态内容加载（第四阶段）














