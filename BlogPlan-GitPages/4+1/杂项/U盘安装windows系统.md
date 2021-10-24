[toc]

## 准备阶段
- 一个U盘(硬盘可不可以、sd可不可以)	--本质是什么？？
- 一个ISO(正在使用的windows可不可以)	--本质是什么？？

## 理论原理
### 文件系统格式
- u盘的格式化的文件系统is什么意思 与 会影响写入其中的iso吗
- 最适合windows的是哪个文件系统
- 最适合linux的是哪个？


## 具体步骤

### 一、制作U盘启动盘

#### 使用ultraISO方式
- 0. 格式化U盘(使用NTFS格式)
- 1. 文件 -> 打开文件 -> iso所在目录
- 2. 启动->写入硬盘

[ultraios](https://www.ultraiso.com/)

#### 使用PE方式 ？？

### 二、更改电脑boot
1. 进入BIOS
- 不同型号电脑进入的方式可能不同
	- thinkpad t480 __F1__
	- 台式机Great Wall(长城) 按__F2__进入BIOS
2. 在BIOS下配置
- 将名字为你的启动盘名的usb启动设置为prioriy为第一的启动(boot -> -> 可能有多个USB DC 、 USB HDD、... )
- 进入usb引导
	- 有的时候，更改完boot priority后 -> 重启后，并不能进入usb启动
		- 1. 在boot右边的restart中 -> save && 立马启动 (推荐)
		- 2. 在boot最下面中设置  lock boot priority = enabled（不推荐）
			- 因为windows更新完后，-> 需要重启进行二次安装 -> 如果设置成每次都从priority最高的usb启动，则无法进入windows的二段安装，只是不停的进行第一段


### 出的bug

#### GPT格式无法进行安装

1. 在安装出现问题的环节进入cmd（安装系统的时候竟然也能通过 fn+ f10进入cmd）
2. 按下面代码进行设置
	- diskpart
	- list disk
	- select disk 0 
	- //进行格式化，也可以使用这个格式化U盘
	- //这种格式化是必须 -> 进入计算机管理 -> 磁盘管理 -> 新加卷才能用的
	- //u盘使用了这种方式，上面的分区全都没了，计算机无法识别
	- clean 
	- exit


#### 如果在上一步不小心把usb所在的disk也给clean了 -> 虚拟介质驱动器error -> 无法进行下一步安装
- 此时需要：将U盘插入另外一台正常工作的电脑，通过计算机管理 -> 磁盘管理 , 给插入的U盘新加卷，然后U盘就可以重新使用了
