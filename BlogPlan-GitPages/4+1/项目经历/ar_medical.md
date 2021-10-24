[toc]


# 完整项目创建流程
1. 创建unity3d项目2020 3d
2. 更改平台： PC -> UWP
3. 导入TextMeshPro
4. 导入MRTK
- auto:
	- 2.6.1版本的自动导入可以成功
	- 2.7.0版本的会导入报错
- self:
5. 应用 MRTK 项目配置器设置
- 使用默认的方式
	- 全选 -> apply
5. 配置MRTK，在buildsetting中设置
- 安装 XR 插件管理
	- XRPlugin: install 	
	- 确保转到“通用 Windows 平台”设置，然后选中“在启动时初始化 XR”和“Windows Mixed Reality”复选框。
		- ![配置]()
- player -> publishsetting -> package name 
	- “包名称”是应用的唯一标识符。 在部署应用之前应更改此标识符，以免覆盖以前安装的应用。
- 设置XR-plugin的深度缓冲格式为16bit
	- ![深度缓冲格式]()
6. 新建scene
- 将mrtk 添加进 新建的scene
	- mtrk -> toolkit -> add to ...


7. unity下打包
- 平台不用设置hololence直接uwp默认的any device即可
- 不需要add scenen
- ![unity打包]()
8. vs下部署
- usb将hololence与pc相连，连上就行不用管其他的
- 打开7中生成的.sln
- master
- arm64
- 设备
- 调试->运行但不调试


### bug:
- 当一个项目第二次使用auto方式导入mrtk报json错的时候，直接新建一个u3d工程重新来
- 一定及时保存scene，


## profile系统
- 为什么每次修改配置都要克隆
	- 默认情况下，MRTK 配置文件不可编辑。 这是一些默认的配置文件模板，必须先克隆它们，然后才能对其进行编辑。 
- 每次修改
- 配置配置文件是顶级配置文件。 因此，若要编辑任何其他配置文件，必须先克隆配置配置文件。

‘



## unity中有用的知识点
### GridObjectCollection类

### vertical layout group