[toc]


# MR系统文档
# 概述


# 需求分析


# 系统设计

![总框架图]()

## Azure Kinect采集数据部分


## WebRTC传输数据部分


## 在Unity中显示数据部分


## 人机交互部分





# 硬件要求
1. 两台Azure Kinect
2. 两台电脑
3. 一台Hololence2


# 开发环境搭建

## 安装必备工具
需要安装的所有软件如下：
1. 最新版本的win10
2. Visual Studio 2019（16.8 或更高版本）
3. Windows 10 SDK
4. Unity Editor（推荐使用Unity Hub安装Unity 2020.3.18f1c1(LTS)版本）

__注意：__推荐使用手动安装。因为如果有的工具已经安装就可以跳过，这样可以避免出现版本冲突等问题

### 使用一键式安装脚本
1. 进入“MR资源”文件夹中的

### 手动安装
如果使用一键式安装失败，则请按照[安装清单](https://docs.microsoft.com/zh-cn/windows/mixed-reality/develop/install-the-tools)来手动进行安装。

所有的安装包均在 MR系统 -> 安装工具 -> 手动安装 目录下。根据电脑已安装情况选择安装文件夹下的各个安装包。

__注意：__
1. 文件夹里没有Unity 2020.3.18f1c1(LTS)的安装包，因为这里使用Unity Hub来安装Unity 2020.3.18f1c1(LTS)，故先装Unity Hub，再通过Unity Hub安装Unity 2020.3.18f1c1(LTS)。
2. 如果已经安装了Unity 2020.3.18f1c1(LTS)则可以跳过这一步

#### 使用Unity Hub安装Unity 2020.3.18f1c1(LTS)
1. 进入MR系统 -> 安装工具 -> 手动安装目录，双击UnityHubSetup.exe安装UnityHub至一个合适的位置。
2. 待UnityHub成功安装后，打开UnityHub软件，进入如下界面：
	__注意：__初次登陆可能需要注册账号，根据指示进行注册-登陆即可。

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\UnityHub登陆界面.PNG" alt="UnityHub软件界面" style="zoom:40%; float: center;" />

3. 点击安装按钮，进入安装界面

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\UnityHub安装界面.PNG" style="zoom:40%; float:center" />

4. 从所有版本中选中Unity 2020.3.18f1c1(LTS)，按照指示一步步安装即可成功安装。

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\选择Unity2020.png" style="zoom:40%; float:center" />



## Unity环境配置
1. 创建unity3d项目(2019 、2020)
2. 更改平台： PC -> UWP
3. 导入TextMeshPro
4. 导入MRTK
- auto:
	- 如果不先做1.2.3.步，使用auto导入会一直卡死
- self:
	- 使用官方的
5. 配置MRTK，在build setting中设置
- XRPlugin: install 
- player:  name
6. 新建scene
- 将mrtk 添加进 新建的scene
	- mtrk -> toolkit -> add to ...

7. 在scene中进行开发 
8. unity下打包
9. vs下部署
- usb将hololence与pc相连
- 打开7中生成的.sln
- master
- arm64
- 设备
- 调试->运行但不调试

10. 一些error不会影响部署和功能
- 2019 + auto的报错比较少，只有一个



## 环境搭建结果测试
- 这是一个用来测试开发环境是否搭建成功的测试工程，包含：untiy项目创建和开发、unity项目部署到Hololence2。







# MR系统各部分实现

## Azure Kinect采集数据部分
### 相机标定
#### 球标定

#### 棋盘格标定


### 数据采集&&对齐




### 多相机同步








## WebRTC传输数据部分
### NAT穿透服务器
### 信令服务器



## 在Unity中显示数据部分
### Particle System

### VFX




## 人机交互部分




# 系统运行步骤
## 1. 开启node-dss-master服务器
1. 通过cmd登录到云服务器，按下图方式输入云服务器的账号密码。
	__登陆密码为：Kang249550__

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\使用shell登陆云服务器.PNG" style="zoom:50%; float:center" />

2. 如下图表示成功进入云服务器

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\成功登录云服务器.PNG" style="zoom:50%; floatcenter" />


3. 进入/home/work/server/node-dss-master目录，在此目录下依次输入如下指令：

<img src="C:\Users\king-kong\Desktop\MR系统\Picture\开启nodeDss服务器.PNG" style="zoom:50%; float:center" />


## 2. 双方接入信令服务器






# 其他
## 与多个用户共享hololence2
https://docs.microsoft.com/zh-cn/hololens/hololens-multiple-users



# 主要参考文档
1. [Microsoft混合现实文档](https://docs.microsoft.com/zh-cn/windows/mixed-reality/)
2. [hololence2介绍](https://docs.microsoft.com/zh-cn/hololens/hololens2-hardware)
3. [使用Unity开发Hololence](https://docs.microsoft.com/zh-cn/windows/mixed-reality/develop/unity/unity-development-overview?tabs=arr%2CD365%2Chl2)
4. [Unity官方文档](https://docs.unity3d.com/cn/2019.4/Manual/Packages.html)
5. [MixedReality-WebRTC官方文档](https://microsoft.github.io/MixedReality-WebRTC/index.html)
