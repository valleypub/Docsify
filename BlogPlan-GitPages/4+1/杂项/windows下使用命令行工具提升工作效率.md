[toc]

# cmd的原理
1. 运行窗口的原理？
2. cmd使用环境变量的原理？
3. windows系统自带的一些功能基本都在C:\Windows\System32文件夹下
4. C:\ProgramData\Microsoft\Windows\Start Menu\Programs这个目录是干什么的？？为什么好多工具要弄个快捷方式存在这个目录下？
- 为什么蓝屏了也能通过组合键进入taskmgr?
- 但是好多应用需要显示屏正常工作来交互才行？
	- ru: cmd+输入软件名 or 双击图标进入软件，他们的共同点是都要在显示屏下进行
# 实用组合	
- 这下功能都是基于windows自带的一些实用工具，通过在cmd下便捷的打开来实现的
- 强制进入cmd模式，哪怕是在安装系统的时候都能进入cmd模式，说明这个运行环境不依赖于系统?boot下？
	- win + r进入强制进入 "运行"
## 软件开机自启动
### 启动目录的原理

### 将软件加入开机自启动
#### 两个启动目录(系统的、用户的)
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp
C:\Users\king-kong\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
#### 手动粘贴快捷方式
1. 右键创建软件的快捷方式
2. 将快捷方式粘贴进上述任意一个目录下

#### cmd + 快捷方式
1. win + r 调出启动输入框
2. 输入 shell:startup 直接跳转到用户启动目录
3. 粘贴快捷方式进2中打开的目录

#### 注册表方式

#### 任务计划程序
即注册一个事件、设置事件触发方式
1. 创建事件描述
2. 创建事件触发方式
3. 绑定事件



### 修改应用的开机自启动
下述能开关的都是已经加入开机自启动目录的软件，如果软件未加入开机自启动目录，根本就不会出现在可开关范围内，默认均是开机不启动

- 1. 使用msconfig工具
	- 步骤：
		- win + r -> 运行窗口
		- 运行窗口中输入 cmd
		- cmd下输入 msconfig，进入系统配置窗口
		- 点击进入启动 -> 控制管理器 -> 启动
- 2. 直接使用Taskmgr.exe
	- 进入上方的启动
## 创建三方快捷热键
- 怕不同版本的windows的组合热键不同？
- 怕不同品牌电脑的组合热键不同？
- 有些好用的组合热键不清楚，一个个搜索又太麻烦？
1. 如果有上述的疑问，那windows官方推出的PowerToys就是为机智又好奇的你准备的
### 准备PowerToys
- 1. 下载PowerToy
[下载链接]()

- 2. 安装PowerToy
- 3. 将PowerToy加入启动文件夹
### PoweToys的使用
- 查看你的电脑+wndows下的支持的组合热键
	- 长安 win
- 快速搜索
	- alt + 空格


# windows提供的自带软件
C:\ProgramData\Microsoft\Windows\Start Menu\Programs
C:\Users\king-kong\AppData\Roaming\Microsoft\Windows
这两个目录下的目录结构差不多，但目录里的软件不太一样，一个系统的、一个用户的？？？

![windows自带的实用工具]()

- 任务管理工具
	- 任务管理器
		- taskmgr.exe
	- tasklist.exe
- windows管理工具
	- 计算机管理
		- compmgmt.msc
	- 磁盘管理
		- diskmgmt.msc
		- diskpart.exe
		- disksnapshot.exe
	- 磁盘清理 
		- cleanmgr.exe
	- 服务
		- services.msc
	- 性能监视器
		- perfmon.msc
			- 可以查看网卡驱动的型号，传输的bps等
	- 注册表编辑器
		- regedit.exe
	- 任务计划程序
		- taskschd.msc
	- 系统配置
		- msconfig.exe
	- 系统信息
		- msinfo32.exe
	- 防火墙
		- WF.msc
- windows附件
	- write
	- notepad
	- control
	- mspaint
	- SnippingTool.exe
	- quickassist.exe
	- mstsc.exe

## 任务计划程序

### 背后的原理是什么？？基于驱动层的什么接口？使用的事件机制？


# else

## 网络相关的
- nslookup
- ipconfig /all
	- 可以查看 mac，网关，dns服务器
- route print
- arp -a


