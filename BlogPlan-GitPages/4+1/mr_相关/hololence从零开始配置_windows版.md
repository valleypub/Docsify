[toc]

# 1. 开发环境配置




# 2. 导入MRTK依赖的包

## TextMeshPro Essential Resources
- In the Unity menu, select Window > TextMeshPro > Import TMP Essential Resources to open the Import Unity Package window:
	- all
	- import
- The TextMeshPro Essential Resources are required by MRTK's UI elements. You can skip this step if you are not planning to use MRTK's UI elements in your project.
- 
# 3. 导入unity3d开发hololence2的助手包MRTK

- hololence可以显示unity3d内置的一些组件
- 可以使用开源社区提供的package（ru:MRTK）来加速开发的进程(如：一些button、menu、)

## MRTK-Unity

[unitypackage官方下载链接](https://github.com/microsoft/MixedRealityToolkit-Unity/releases)

[MRTK官方说明文档](https://docs.microsoft.com/zh-cn/windows/mixed-reality/mrtk-unity/configuration/usingupm)

### 1. 导入MRTK packasge

### 2. 配置MRTK

- Enable VR supported
	- Player Settings > XR Settings.
- Set Single Pass Instanced rendering path
	- Player Settings > XR Settings > Stereo Rendering Mode to Single Pass Instanced.
- Set default Spatial Awareness layer
	- 
- Audio spatializer
	- 

### 3. 将MRTK加入unity项目中

#### 配置 MRTK 和 unity 使用 XR SDK 管线
- XR SDK is Unity's new XR pipeline in Unity 2019.3 and beyond. In Unity 2019, it provides an alternative to the existing XR pipeline. In Unity 2020, it will become the only XR pipeline in Unity.
- 
#### 对各配置文件进行配置


# 3. 导入MRTK依赖的包

## TextMeshPro Essential Resources
- In the Unity menu, select Window > TextMeshPro > Import TMP Essential Resources to open the Import Unity Package window:
	- all
	- import
- The TextMeshPro Essential Resources are required by MRTK's UI elements. You can skip this step if you are not planning to use MRTK's UI elements in your project.



# 4. 打包工程-->可执行程序

- 1. 构建和部署步骤需要在unity项目中执行。
- 2. 构建和部署使用MRTK的应用程序就像构建和部署任何其他Unity应用程序一样，没有针对MRTK的特定说明。
- 3. 


## 1. unity3d构建
- 1. xr渲染管线的配置

	- 1. 是用旧版xr
	- 2. 使用新版xr sdk需要的配置：

		- 1.



- 2. build setting设置

![示例]()

## 2. visual stdio部署



# 5. 一个简单hololence项目的完整开发步骤

1. 创建unity3d项目(2019 、2020)
2. 更改平台： PC -> UWP
3. 导入TextMeshPro
4. 导入MRTK
- auto:
	- 如果不先做1.2.3.步，使用auto导入会一直卡死
- self:
	- 使用官方的
5. 配置MRTK，在buildsetting中设置
- XRPlugin: install 
- player:  name
6. 新建scene
- 将mrtk 添加进 新建的scene
	- mtrk -> toolkit -> add to ...
7. unity下打包
8. vs下部署
- usb将hololence与pc相连
- 打开7中生成的.sln
- master
- arm64
- 设备
- 调试->运行但不调试

9. 一些error不会影响部署和功能
- 2019 + auto的报错比较少，只有一个
![]()

![]()