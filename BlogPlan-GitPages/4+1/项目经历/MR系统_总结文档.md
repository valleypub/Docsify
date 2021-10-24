[toc]



整个工程分几大部分：
1. Azure Kinect数据采集部分
2. Webrtc传输部分(Because_why_not)
	1. 信令服务器搭建
	2. ICE服务器搭建
		- 用别人提供的免费的
		- 自己编译一个放于云服务器上
	3. 
3. 粒子系统显示部分
	1. cpu版的（简单、数千粒子、慢）
	2. gpu版的（复杂、数百万粒子、快速）
4. 用户界面系统设计
5. 输入系统设计
6. steamvr显示部分
6. unity动态数据加载部分
7. 



# Azure Kinect采集部分


# webrtc传输部分
## 信令服务器搭建篇
- 主要用于双端建立p2p连接。
- 主要做两件事：交换SDP ，交换IceCandidate信息(即NAT穿透：找出出的局域网ip一一对应分配的那个公网ip)

- 可以使用多种数据传输协议来设计
	- websocket
	- socket
- 目标：
	- 交换双方的sdp数据
	- 交换ice穿透后的iceCandidate信息



### server端

### client端(u3d版本:以u3d给出的方案实现)



## STUN 服务器搭建篇
because-why-not中这一部分的讲解还可以：
https://www.because-why-not.com/webrtc/guide/
https://www.because-why-not.com/webrtc/tutorials-server-side/
https://www.because-why-not.com/webrtc/faq/


