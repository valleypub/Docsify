[toc]


# 各种无线数据传输方案



# webrtc的一种商业实现(WEBRTC VIDEO CHAT)

## 初识webrtc video chat

	是webrtc方案在unity下的一个实现。
	
	这些资产附带一个功能齐全的示例应用程序（“ CallApp”），以演示如何创建视频聊天。如果这是您所需要的，那么您可以简单地将UI更改为自己喜欢的方式，并在不进行任何编程的情况下使用它。
	
	该插件会自动为您处理所有音频/视频和网络功能。您需要做的就是创建一个Call对象，然后使用共享密码将其连接到另一端。然后，事件处理程序将在用户连接，发送消息，接收到新的视频帧等时返回事件。视频帧将作为原始图像返回。然后，您可以将其复制到纹理中（请参见示例），或将其用于其他库，例如用于面部识别或应用滤镜。



[版本更新日志](https://www.because-why-not.com/webrtc/changelog/)


## server端


### 同一子网中使用(在单个LAN / WIFI中)


### 不同子网中使用（上升到公网层面，需借助ice Server）

### 共享地址

### 12777/12776  与  80/443

### signaling server 安装-启动 步骤
	1. 安装node.js运行环境
	2. 安装npm
	3. npm --version 查看是否正确安装
	4. node --version
	4. npm install    第一次开启之前要运行此命令，安装依赖的包
	5. node server.js 在server.js所在目录运行此命令
	6. 使用浏览器输入：http://localhost:12776/ 进行测试（V0.981及以上）
	7. 如果打印：running则是正确的




​	

## client端

重要文件夹和文件
请注意，在V0.983中更改了结构。

- scripts/UnityCallFactory.cs – Main access for Networ/Video/Audio call functionality
- chatapp – contains the text only ChatApp example using a star topology
- callapp – contains a fully functional 1-to-1 video chat app
- examples – contains a few simple examples to learn how to use the API
- extras – contains experimental features that are not fully supported
- server.zip – Contains an open source node.js signaling server. More at [Server side info / Tutorials](https://www.because-why-not.com/webrtc/tutorials-server-side/)
- Plugins
  - Contains C# libraries that provide the API
  - The subfolders contain wrappers that map the API to platform and processor architecture specific code
  - Never move or rename this folder


















