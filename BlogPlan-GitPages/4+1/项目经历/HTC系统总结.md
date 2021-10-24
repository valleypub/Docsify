[toc]


# 概述




# 系统设计
- 总系统架构图：

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\MR总系统搭建图.png" alt="MR总系统搭建图" style="zoom:40%; float:center" />

- Webrtc建立流程图：

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\webrtc建立流程.png" style="zoom:70%; float:center" />


- 配上图的文字描述

# 各部分实现
## 目前使用的
### 1.Azure Kinect采集数据部分

#### 1.1标定部分
1. 采集部分
采集双目彩色图像和深度图并生成点云。
2. 标定部分
标定地面：裁剪点云保留大部分地面；ransac拟合地面方程；再地面建立坐标系；求相机1坐标系到地面坐标系的RT。
双目标定：使用opencv例程stereocalib.cpp的方法，修改为固定内参标定，获得相机2到相机1的RT。
计算相机2到大地坐标系的RT。
#### 1.2图像采集和点云生成
此处为概述，具体环境搭建和代码说明在《代码说明及环境配置步骤.docx》。

- 发送端：采集并发送2台相机的彩色图和深度图
- 接收端：接收到深度图和彩色图，利用相机内参和深度图生成相机坐标系下的点云，进行坐标系转换，分别将两台相机的点云转换到大地坐标系，将所有点添加到粒子系统显示。没有进行点云拼接。
#### 1.3数据传输
##### 1.3.1目前尝试过的方法
- 目前传输的数据为两台相机的数据，其中单台相机的数据为一张深度图和3通道rgb。传输的深度图大小540 * 384，彩色图的大小与深度图相同。
	- 彩色图在传输过程中的误差不大。
	- Kinect深度数据为16位，传输深度数据时首先确定传输的深度范围，计算有效的深度数据位数，例如1m范围需要用10位表示，将数据分为高低位，低8位直接传输，高2位左移后补0b100000。
- 单台相机 
	数据量占到可用空间的一半，对于有用数据压缩较小3-8，2-8测试，点云效果都还可以，观看流畅，帧率没有测过。（2-8表示高两位，低8位的传输方式）
- 两台相机 
	图像大小540 * 384，占用所有可用的1920 * 1080的Y空间（uv未使用），各传输方式帧率如下：
|传输方式|fps|
|----|----|
|4-8| 在噪声较小的条件下不足8帧|
|3-8| 13帧|
|2-8| 15帧|

- 15帧的原因：帧率30时webrtc压缩较大，数据质量差，表现为点云的周围和高位变化的地方会有噪声。
##### 1.3.2接收到深度图的处理
- 单台相机15fps的条件下接收的数据基本不需要处理
- 两台相机数据量增大，对于压缩的要求变高，接收到的数据在高位衔接处以及边缘会产生噪声，这种条件下都做了简单的滤波处理：
	1. 去除高位变化处的点
	2. 用一个3 * 3的模板遍历，做边缘部分的腐蚀，去除边缘的噪声
	3. 用1 * 3的模板做简单的中值滤波，去除高位衔接处不连续的点
		- 由于模板较小效果不是特别明显，但是增大模板会使时间增加
		- 滤波还导致了一个另一个问题，由于高位变化处的点在接收时就已经做了一步去除，会有一部分空洞，在后续滤波后，该部分的缝隙会增大，但是两片点云叠加时，该问题并不明显。（接收的数据越差，问题越明显，高位位数越多，越明显）。尝试过使用一个模板遍历取众数填补空洞，有一定效果，但是该函数十分耗时，且在缝隙较大时效果不明显）
##### 1.3.3数据拆分对于传输的影响
1. 传输9位数据时候不需要拆分，丢弃最低位直接传输，可以表示的范围为512mm，由于传输深度图时不在深度范围的数据补0，在人体边缘的数据会出现损失，具体表现为在人边缘有一个框（错误的数据），对深度图进行边缘处理或者按照深度值的分布滤波可以去除。
2. 拆分数据后，上述边缘损失的问题仍然存在，另一个噪声产生的地方是高低位衔接的地方，这些点在编码后高低位不对应，例如真实数据是0x1f或者0x20，可能变成0x2f或者0x10。
##### 1.3.4数据放置位置对于传输的影响
- 目前的传输接口是1920 * 1080 I420格式的数据，也就是可以传输1080p的彩色图。深度图和彩色图的摆放尽量遵从分块存储的原则，将图片分块放置在1920 * 1080的大图中。I420格式中Y部分编码损失要少于uv部分。

### 2.WebRTC传输数据部分
经测试发现，目前because-why-not中只有I420p和ARGB两种方式是可以使用的，别的内置的传输方式YUV2 ，Native等都还尚不能用
1. 人体数据的传输使用I420p的方式传输
2. 参观者回显画面使用ARGB的方式传输


### 3.Unity中显示数据部分
基于ParticleSystem显示点云并通过滤波后处理优化显示效果



### 4.人机交互部分
#### 用户界面


#### 实时输入控制

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\实时输入控制图.png" style="zoom:40%; float:center" />


### 5. 动态内容加载
- 目前完成了image、video、model类型文件的动态加载。
- 使用Unity特殊文件夹机制和TriLib理论上支持任何形式文件的动态导入，但是对于不同类型的文件需要在Unity中编写不同类型的代码来对文件进行解析和展示，所以，此部分需要根据实际需求进行添加



## 下一步
### Azure Kinect采集数据部分&&WebRTC传输数据部分
1. 为了减少rgbd同时传输时的相互影响，准备使用多个CappApp，同一传输方向建立两条独立的传输通道，一条传RGB，一条传D，接收端接受数据后，对其整合处理。


### Unity中显示数据部分

- ParticleSystem与VEG的对比

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\两种粒子系统的对比.PNG" style="zoom:50%; float:center" />


- 经测试，WEBRTC VIDEO CHAT插件在Unity2020版也能正常工作，又因自Unity2019开始支持VEG功能，所以，下一步准备将项目整体迁移到Unity2020，使用VEG功能来渲染点云。





### 人机交互部分
#### 用户界面

#### 实时输入控制
基于steamVR新提出的动作层抽象，将集中式基于按键的输入控制改为基于动作的输入控制

### 动态内容加载










# 项目开发流程示例

## 硬件要求
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\htc\硬件要求.png" style="zoom:50%;" />


## 开发环境配置
本项目的VR设备采用的是HTC VIVE，这是HTC公司 和Valve公司联手开发的一款产品，其中HTC负责硬件方面，Valve负责开发软件。Valve为HTC VIVE设备开发的软件就是基于Steam和openVR开发出来的steamVR。为了便于Unity工程师工程开发，steamVR推出了steamVR Plugin这款Unity下的插件，Unity下的HTC VIVE开发需要通过这个插件进行。下面，分别对这两部分进行配置：
### Vive SetUp
1. 安装软件

2. 硬件连线

3. Room SetUp

4. 测试


### Unity安装SteamVR Plugins

- 安装：
1. 在菜单栏，找到window -> Asset Store，搜索SteamVR，找到SteamVR Plugin添加至我的资源
2. 再打开window -> Package Manage，选择My Assets，从列表中选择steamVR Plugin，然后import进工程即可
3. 如果成功导入SteamVR Plugin，那么会在Project窗口中多出SteamVR、SteamVR_Input、SteamVR_Resources三个文件夹。

- 测试：在Project窗口中，进入到Assets\SteamVR\InteractionSystem\Samples目录，双击打开Interactions_Example，看工程能否成功运行


## 新建Unity工程，对各部分进行开发

|插件名|版本号|
|----|----|
|WEBRTC VIDEO CHAT |  0982|
|steamVR Plugins | Version 2.7.3 (sdk 1.14.15) - February 24, 2021|

### 1. 详细过程版

#### 1. 新建两个工程
使用Unity3d 2020新建两个3d工程，分别取名为：Listner 、Explainer


#### 2. steamVR Plugins分别导入工程


#### 3. WEBRTC VIDEO CHAT分别导入工程

#### 4. 导入脚本
- Listener端：
	1. 在Project窗口中，新建一个MyScript文件夹，用来存放导入的脚本
	2. 将HTC工程中的MR_HTC\HTC移植到2020\MyScript\Listener下的所有脚本文件，拖到1.中的MyScript文件夹中。有两种拖动方法均可以：
		1. 直接将MR_HTC\HTC移植到2020\MyScript\Listener下的所有脚本文件直接拖到打开的Unity 的Project窗口下的Myscript中
		2. 先找到Unity 的Project窗口下的Myscript在Native文件夹系统中的位置，再将MR_HTC\HTC移植到2020\MyScript\Listener下的所有脚本文件复制粘贴到这个位置

- Explainer端:
	1. 在Project窗口中，新建一个MyScript文件夹，用来存放导入的脚本
	2. 将HTC工程中的MR_HTC\HTC移植到2020\MyScript\Explainer下的所有脚本文件，拖到1.中的MyScript文件夹中。有两种拖动方法均可以：
		1. 直接将MR_HTC\HTC移植到2020\MyScript\Explainer下的所有脚本文件直接拖到打开的Unity 的Project窗口下的Myscript中
		2. 先找到Unity 的Project窗口下的Myscript在Native文件夹系统中的位置，再将MR_HTC\HTC移植到2020\MyScript\Explainer下的所有脚本文件复制粘贴到这个位置


#### 5. Explainer端工程引入Azure Kinect支持
因为Explainer端需要使用Azure Kinect，所以需要在Explainer端引入Azure Kinect相关的dll。而Listener端不需要


#### 6. 将初始Scene导入工程
- Listener端：
	1. 将MR_HTC\HTC移植到2020\MyScenes\Listener下的MR_Listener.unitypackage导入Listener工程。具体步骤如下：
		1. 菜单栏 -> Assets -> Import Package ->Custom Package
			![]()
		2. 浏览到Native文件夹系统中的MR_HTC\HTC移植到2020\MyScenes\Listener下选择MR_Listener.unitypackage，选择all -> import即可
			![]()
		3. 将MyResource下的Prefabs全部拖进SampleScene中，并将SampleScene另存为MR_Listener


- Explainer端:
	1. 将MR_HTC\HTC移植到2020\MyScenes\Explainer下的MR_Explainer.unitypackage导入Explainer工程。具体步骤如下：
		1. 菜单栏 -> Assets -> Import Package ->Custom Package
			![]()
		2. 浏览到Native文件夹系统中的MR_HTC\HTC移植到2020\MyScenes\Explainer下选择MR_Explainer.unitypackage，选择all -> import即可
			![]()
		3. 将MyResource下的Prefabs全部拖进SampleScene中，并将SampleScene另存为MR_Explainer











### 2. 直接导入我设置好的最小初始Scene

#### 工程中分别导入unitypackage
- Listener端：
	1. 新建一个Unity3d工程
	2. 将MR_HTC\HTC移植到2020\MyScenes\Listener下的MR_Listener_AllInOne.unitypackage导入Listener工程。具体步骤如下：
		1. 菜单栏 -> Assets -> Import Package ->Custom Package
			![]()
		2. 浏览到Native文件夹系统中的MR_HTC\HTC移植到2020\MyScenes\Listener下选择MR_Listener_AllInOne.unitypackage，选择all -> import即可
			![]()
		3. 点击reload
		4. 点击 accept all -> ok
		5. 将SampleScene另存为MR_Listener


- Explainer端:
	1. 新建一个Unity3d工程
	2. 将MR_HTC\HTC移植到2020\MyScenes\Explainer下的MR_Explainer.unitypackage导入Explainer工程。具体步骤如下：
		1. 菜单栏 -> Assets -> Import Package ->Custom Package
			![]()
		2. 浏览到Native文件夹系统中的MR_HTC\HTC移植到2020\MyScenes\Explainer下选择MR_Explainer.unitypackage，选择all -> import即可
			![]()
		3. 点击reload
		4. 点击 accept all -> ok
		5. 将SampleScene另存为MR_Explainer


- 此时分别在两台能正常联网的电脑上运行上述两个工程，两端点击Join按钮后，应该会在Explainer端显示Listner端的Game视图，如下图所示：

![Listener端]()

![Explainer端]()






----
__至此，steamVR Plugins 和 WEBRTC VIDEO CHAT正确导入工程，并且最基础的Scene也已成功搭建，下面可以在这个最小Scene的基础上增添功能__

----








# 参考文档
