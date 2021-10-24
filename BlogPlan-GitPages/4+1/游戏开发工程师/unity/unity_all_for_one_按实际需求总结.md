[toc]



# 动态加载资源
1. Resource文件夹 + ```Resources.Load<T>()``` 
2. WWW方式 or WebRequest
3. StandardAsset文件夹 + 
4. TriLib插件



# 输入系统


# Web服务器

- 仅使用Unity开发前端应用是不够的，要配合Web开发后端服务，这样才完整。

- Web后端开发涉及的内容：
	1. Web后端所需环境配置
	2. 数据库
	3. 前后端通信
		- 使用Unity提供的网络功能与后端进行数据通信



# 导出工程
1. 直接使用UnityHub定位到工程所在目录，将整个工程文件夹都拷贝过去
2. 使用Assets -> export package，将工程内的一切打包成一个unitypackage，然后在别的工程中使用Assets -> import package -> custom package来导入，单个的话和复制整个工程文件夹差不多，但是这种的好处是：
	1. 可以在一个工程中精确导入别的工程的一部分资源or整个资源
	2. 可以导入多个不同工程的资源


如：
1. 使用unitypackage的方式来将我配置好的基础插件和最小scenee的工程导出，别人就可以在这个基础上进行开发了
