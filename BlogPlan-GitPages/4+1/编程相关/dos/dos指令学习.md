[toc]

[windows官方文档](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/subst)


## 打印指令
### print
- 通过dos操作实际的打印机来打印一个文本文件(如：txt)
### echo 
- @echo off
### >




## 文件



## 文件夹(目录)
### DIR
1. 获取某文件夹下的所有文件名，并存储到一个文件中：
	- 1. cd 进入相应目录
	- 2. 运行 DIR /ON /B > D:\xxxxx.txt



## Start指令
1. 跳转执行另一个bat文件，并等待结束，再继续执行本bat文件的下一指令
	- start /wait call test.bat 
		- 其实在这里就没有必要使用start /wait了，因为使用了call命令后，test.bat已经控制了流程，一定是在call结束后才会继续下一步的操作

2. 顺序执行多个可执行文件，start a.exe默认是异步执行的
	- start /wait a.exe
	- start /wait b.exe
	- start /wait c.exe


3. 有顺序执行 a b c.exe肯定就有对应的异步执行了？？？使用cmd指令？？
	- cmd /c dir 是执行完dir命令后关闭命令窗口。 
	- cmd /k dir 是执行完dir命令后不关闭命令窗口。
	- cmd /c start dir 会打开一个新窗口后执行dir指令，原窗口会关闭。
	- cmd /k start dir 会打开一个新窗口后执行dir指令，原窗口不会关闭。 
		- 原窗口关闭、不关闭有什么区别？？不关闭的意思是异步向下执行？？？


## 环境变量相关


## 注释
### rem
rem 不显示这行
### % %
%不显示这些%
### echo

### ::
::不显示这行



## 磁盘相关
### subst
- 是什么
	- 它的功能是以磁盘驱动器符代替路径名称，以使驱动器符与指定的子目录路径等效
	- 即，将一个目录极逼真的等效模拟一个真正的硬盘
- why need it

#### subst的妙用
1. 通过使用subst可以解决 电脑原先有E盘+初次安装node.js时设置了E盘 -> 后续运行node-v14.17.5-x64.msi时会报invalid Driver E的问题，此时，使用subst 设置虚拟盘符可以解决
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\invalidDriveD问题.PNG" alt="invalidE的问题" style="zoom:60%;" />
	- 解决方案：
	- subst E: %TEMP%    //建立虚拟盘符映射
	- 再次运行node-v14.17.5-x64.msi手动更改安装目录为C盘下
	- subst E: /d		//解除虚拟盘符映射

##### 隐藏驱动器
- 虽然微软建议用户采用没有使用的盘符进行虚拟，但并不表示它不能虚拟已经存在的盘符，比如A盘、C盘等。用户可以通过Subst命令虚拟A、C等盘符，直接覆盖这些已经存在的盘符，使他人无法看到该盘的真正内容，以达到隐藏真实驱动器的目的
	- 现在已经不支持这样设置了，如：使用了C:盘，再使用subst C: C:/neirong来虚拟会报错
- 如：使用C:\neirong 虚拟为 A:盘
	- 虚拟前：
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\subst虚拟盘符.PNG" alt="虚拟前" style="zoom:60%;" />
	- 虚拟后：多了一个A：盘
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\subst虚拟盘符1.PNG" alt="虚拟后" style="zoom:60%;" />


# 其他
## bug记录
- 直接使用npm install不行
- 使用 start /wait npm install，会新开启一个窗口，需要我们在关闭新开期的窗口后还要输入y/n后才会运行下一条node server.js，但是不想输入y/n想做成全自动的 
	- 使用start /wait是不是都需要输入y/n这个操作？？？
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\start-wait方式.PNG" alt="start /wait call" style="zoom:60%;" />
- 使用call npmInstall.bat的方式可以全自动
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\直接call的方式.PNG" alt="直接call" style="zoom:60%;" />


## 自动批处理文件
- autoexec.bat是自动批处理文件，每次电脑开机会自动执行这个bat文件，具体的更确切的执行是在什么时候？？？
	- 

- 是什么
	- ![windows的自动批处理文件进化史]()

- why need it
	- 一般我们在里面装载每次必用的程序，如： path（设置路径）、smartdrv（磁盘加速）、 mouse（鼠标启动）、mscdex（光驱连接）、 doskey（键盘管理）、set(设置环境变量)等