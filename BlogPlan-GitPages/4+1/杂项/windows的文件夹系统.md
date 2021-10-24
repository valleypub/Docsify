[toc]


## 特殊的文件夹目录

1. 最近使用
C:\Users\king-kong\AppData\Roaming\Microsoft\Windows\Recent

2. typora主题所在文件夹
C:\Users\king-kong\AppData\Roaming\Typora\themes，将从别处下载的主题css文件放在这个目录下即可


### 开机启动文件夹

- 是什么
	- windows下有两种开机自启动文件夹：
		- 系统的：这里面设置的对所有用户均使用
			- ==\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp==
		- 用户的：只在特定用户登陆时，才会正常启动
			- ==\Users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup==

- why need it
	- 有时有这样一种需求：电脑一开机就自动的在后台运行而不需要我们双击方式开启，windows下这种需求是通过开机启动文件夹实现的。

- how use it
	1. 复制想开机自启动的软件的快捷方式
	2. 进入开机自启动文件夹
		- 在win + r -> shell:Common Startup
		- 在explorer中输入\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp
	3. 将快捷方式粘贴进2. 打开的的文件夹内
	4. win + r -> msconfig -> 在启动中，打开