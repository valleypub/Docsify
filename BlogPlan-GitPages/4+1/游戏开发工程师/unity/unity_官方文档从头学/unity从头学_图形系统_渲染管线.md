[toc]

# 渲染管线(Render pipelines)
- 是什么
	- 渲染管线执行一系列操作来获取场景的内容，并将这些内容显示在屏幕上。概括来说，这些操作如下：
		- 剔除
		- 渲染
		- 后期处理
- why need it
- 注意事项
	- 将项目从一个渲染管线切换到另一个渲染管线可能很困难，因为不同的渲染管线使用不同的着色器输出，并且可能没有相同的特性。
	- 必须要了解 Unity 提供的不同渲染管线，以便可以在__开发早期为项目做出正确决定__。

- Unity provides __three__ prebuilt render pipelines with different capabilities and performance characteristics, or you can create your own
	- prebuilt:
		- 内置渲染管线
			- 是Unity的__默认渲染管道__
			- 它是通用的(general-purpose)渲染管道，其__自定义选项有限__
				- 主要目的是对于不同应用领域的通用性
		- 通用渲染管线URP
			- 是一种可快速轻松自定义的可编程渲染管线，允许您在各种平台上创建优化的图形
		- 高清渲染管线HDRP
			- 是一种可编程渲染管线，可让您在高端平台上创建出色的高保真图形，AAA级游戏多使用此渲染管线
	- self-def:
		- 可编程渲染管线SRP
			- SRP是一项可以通过 C# 脚本来控制渲染的功能
			- SRP 技术可以强化通用渲染管线 (URP) 和高清渲染管线 (HDRP)
			- URP和HDRP有着广泛的自定义选项，是Unity 提供的两种预构建的可编程渲染管线 (SRP)，但是，如果还想在更大程度上控制渲染管线，可以创建自定义 SRP。



## 内置渲染管线

## 通用渲染管线
http://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@12.0/manual/index.html
## 高清渲染管线
http://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@12.0/manual/index.html
## 可编程渲染管线
http://docs.unity3d.com/Packages/com.unity.render-pipelines.core@12.0/manual/index.html
## 选择合适的渲染管线(Switching render pipelines)
- 在Unity编辑器中设置active渲染管道后，Unity便开始使用它进行渲染。This includes the Game view, the Scene view, and previews for Materials that are displayed in the Project panel and the Inspector.

### Activating the Built-in Render Pipeline
要将活动渲染管道设置为内置渲染管道，您必须告诉Unity您没有使用任何基于脚本的渲染管道的渲染管道。从项目设置中删除所有SRP渲染管线(Scriptable Render Pipeline)的引用后，Unity默认使用内置渲染管道。



### Activating URP, HDRP, or a custom render pipeline based on SRP