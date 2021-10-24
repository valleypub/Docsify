[toc]

# webrtc


## WebRTC概述
- 是什么
	- 网页浏览器中进行实时语音对话or视频对话的__解决方案__
	- 2011.6.1日，在google , mozilla, opera的支持下被纳入W3C推荐标准
	- webrtc的原则是：开源、免费、标准化、浏览器内置、比现有技术高效
- why need rtc
	- 数据量的增长远超带宽(bps)的增长 -> 数据的新的压缩传输方案

- webrtc的优点：
	- 跨平台
	- 实时传输(rtc)
	- 音视频引擎
	- 免插件
		- 打开浏览器即可使用
	- 免费
	- 强大的打洞能力
		- webrtc技术包含了使用STUN,ICE,TURN,RTP-over-TCP的关键NAT和防火墙穿透技术，并支持代理
	- 主流浏览器的支持

- webrtc的应用场景：
	- 音视频会议
	- 音乐播放器
		- 网易云音乐
	- 远程桌面共享
	- P2P网络加速
	- 文件传输工具
	- 即时通讯工具
	- 游戏
	- 实施人脸识别
## webrtc整体架构
- webrtc目前形成了一个HTML5规范，由W3C来制定并维护这个标准

[webrtc官网](https://webrtc.github.io/webrtc-org/architecture/)
https://www.w3.org/TR/webrtc/
![webrtc总体架构图]()

- Web API层：
	- 
- C++ API层

- Session Management层：
	- 是一个抽象的会话层，提供会话建立和管理功能
	- 该层协议留给开发者自定义实现
	- 对于web应用，建议使用WebSocket技术来管理信令Session

- Transport
	- transport为webrtc的传输层，涉及音视频数据的发送、接收、网络打洞等内容，可以通过STUN,ICE组件来建立不同类型的网络间的呼叫连接

- VoiceEngine
	- voiceEngine是google在收购GIPS后开源的，目前在VoIP技术上处于业界领先地位。
	- iSAC
	- iLBC
	- NetEQ For Voice
	- Acoustic Echo Canceler
	- Noice Reduction

- Video Engine
	- VPx是google收购ON2公司后开源的视频图像编解码器，现在是webM项目(google致力于推动的HTML5标准之一)的一部分
	- ImageEnhancements模块
	- Video Jitter Buffer模块

## WebRTC通话原理

### 概述
- webrtc通话最简单的应用场景is一对一视屏通话，如：微信等视频聊天
#### 简化的连接建立流程
- 通话的过程很复杂，简化为三步：
1. 媒体(SDP)协商
	- 交换双方交换建立连接需要的信息，如：双方使用的音视频编解码格式等
	- 要交换的信息通过SDP来进行描述
		- SDP是一个描述多媒体连接内容的协议，如：分辨率、格式、编码、加密算法，以便于在数据传输时两端能理解彼此的数据
		- SDP更像一种数据格式
	- 两端SDP的生成
	- SDP的发送
		- 1. 需要一个双方都能访问的服务器
		- 2. 一般是使用Socket进行SDP交互，但也可以使用Node.js，Golang或其他技术，只要能使双方交换SDP数据便可
2. 网络(Candidate)协商
	- 通信双方需要彼此了解对方的网络情况，这样才可能找到一条通信链路，需要做以下两个处理：
		- 1. 获取外网IP地址映射
			- 使用STUN/TURN/ICE
		- 2. 通过信令服务器交换网络信息
			- 可和媒体协商共用同一个server
	- 理想的网络情况是每个浏览器所在的IP都是公网IP，可以直接进行点对点P2P连接
		- 实际情况是，我们的计算机都是在某个局域网下的并且有防火墙，需要进行网络地址转换(NAT)
3. 建立连接


####  NAT
[NAT介绍](https://en.wikipedia.org/wiki/Network_address_translation)

![]()

- NAT是为了解决ipv4下的IP地址匮乏而出现的一种技术
- NAT会阻止外网地址的访问，必须使用NAT穿透
- NAT穿透技术
  - 借助一个公网IP服务器进行穿透：
    - webrtc就是使用的这种思路

#### ICE
[ICE介绍]https://en.wikipedia.org/wiki/Interactive_Connectivity_Establishment

- ICE是由IETF的MMUSIC工作组开发出来的一种framework，可集成各种NAT穿透技术，如STUN、TURN（Traversal Using Relay NAT，中继NAT实现的穿透）、RSIP（Realm Specific IP，特定域IP）等。
	- 该framework可以让SIP(Specific IP，特定域IP)的客户端利用各种NAT穿透方式打穿远程的防火墙。
#### STUN

#### TURN
https://zh.wikipedia.org/wiki/TURN
https://www.voip-info.org/turn/

- TURN 是STUN-bis协议的扩展，以便在 NAT 后面有一个或两个端点时促进 NAT 横穿。
- 使用 TURN 时，会话的媒体流量必须转到中继服务器(relay server)。由于中继费用昂贵，在提供者必须提供的带宽和媒体流量的额外延迟方面，当端点无法直接通话时，TURN 通常用作最后的手段。
- TURN uses STUN-bis binary protocol, but it defines new requests, attributes, and a totally new set of functionality. Unlike STUN-bis, TURN is a stateful protocol: it defines sessions, and each session has its own lifetime and its own context.
- ICE框架为两个端点提供了一个机制，以发现用于媒体流量的__最优化路径__。


#### STUN||TURN服务器的搭建
- 1. 使用coturn开源项目来搭建
- 2. 使用golang版的pion项目来搭建


#### 信令服务器(signal server)


## webrtc三大部分
1. MediaStream:捕获音视频流
2. RTCPeerConnection:传输音视频流（一般用在 peer-to-peer 的场景）
3. RTCDataChannel: 用来上传音视频二进制数据（一般用到流的上传)




## webrtc建立
### 本地设置

### 连接建立

### 数据通道
- 作为WebRTC的三大模块之一，数据通道(DataChannel)执行短消息、二进制数、文本数据的传输作为传输音视频数据以外的补充
- webrtc的数据通道 与 websocket的区别
	- DataChannel是P2P的直连，websocket需要中间服务器中转
	- websocket基于TCP协议，DataChannel基于SCTP协议
		- SCTP是一种和TCP,UDP同级的传输协议
		- SCTP默认情况下能可靠有序的传输，但也可配置成为不可靠的传输
	- 构造websocket需要一个url，与服务器建立连接，创建一个唯一的SocketSessionId。DataChannel的连接依赖于一个RTCPeerConnection对象，当RTCPeerConnection建立起来以后，可以包含一个or多个RTCDataChannel
	- 