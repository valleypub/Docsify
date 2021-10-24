[toc]


	docker必须运行在linux内核的机器上
	1.如果是linux做内核的系统：ubuntu、Debain、centos等
	2.如果是windows、macOS则需要先虚拟出一个linux环境（使用虚拟机的方式）

# windows下使用Docker

## 1.安装虚拟机

### 1.使用官方推荐的Hyper-V 

	注意：Hyper-V 是微软开发的虚拟机，类似于 VMWare 或 VirtualBox，仅适用Windows10。这是 Docker Desktop for Windows 所使用的虚拟机。但是，这个虚拟机一旦启用，QEMU、VirtualBox 或 VMWare Workstation 15 及以下版本将无法使用！如果你必须在电脑上使用其他虚拟机（例如开发 Android 应用必须使用模拟器），请不要使用Hyper-V！

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\a.PNG" style="zoom:60%;" />



#### 1.1使用 **控制面板** 开启Hyper-V支持
	cmd->control->程序和功能->启用或关闭windows功能->Hyper-V
<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\1513668234-6433-20171206211858191-1177002365.png" style="zoom:70%;" />


#### 1.2使用 **命令行方式** 开启Hyper-V支持
	管理员身份运行powershell，输入:
	Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All

## 2.Get Docker(安装Docker for Windows版）

[Docker for Windows Installer下载链接](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

[Docker for Windows 用户手册 链接](https://docs.docker.com/docker-for-windows/)

	不能直接运行docker for windows,出现下面的问题

<img src="C:\Users\king-kong\Desktop\essence\blog-plan\IMG\b.PNG" alt="docker for windows不能运行" style="zoom:70%;" />



[wsl2更新链接](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package)



[docker学习官方文档](https://docs.docker.com/get-docker/)

## 3.GetStarted
	


## 4.Guides
	learn how to set up the Docker environment, and start container the applications


	常用命令
[docker常用命令](https://docs.docker.com/engine/reference/commandline/docker/)
	docker version
	docker ps       ;查看docker有无在运行
	docker stop     ；docker的七种状态
	docker start
	docker pause
	'docker' + 'docker command --help' 
	如：
	docker stats --help


## 5.实例（使用Docker构建 opencv(c++)开发环境）




