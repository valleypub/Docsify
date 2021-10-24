[toc]


# 前言
- 在我配置docsify的时候，我突然发现对于linux我竟如此的陌生，研一一年的时间我对linux的掌握可以说是毫无半寸的精进。我仍然不知道在linux中如何下载一个软件、如何给软件配置环境变量、软连接是什么、如何彻底的删除一个软件、linux下载一个软件都会在那些地方多出哪些文件(这一块说白了是对linux的文件系统不熟悉)，甚至对于nodejs的报错我都看不懂。此刻我下定决心，要将我对linux学习的经验总结于此，


- 我根据我自身的因素，分析发现适合我的书应该是一本很短小精悍，实践性很强，主干脉络讲的很清晰的小册子，这种书我读了会收获最大，对我而言当然是最好的书。


- 由于我云服务器上使用的是centos7 ,使用[此linux教程](https://www.runoob.com/linux/linux-tutorial.html)最合适



## linux启动的过程

## linux文件系统
### 系统目录结构
![]()
### 文件基本属性
### 文件与目录管理
### 用户和用户组管理

### 文件的下载-安装-配置-100%删除

- 要养成像windows下那样的下载-安装位置的提前制定，这样做到下载-安装的位置都在那里，删除的时候就知道怎么删除了

- linux下之所以删除个 node ，docsify , apache , mySQL不知道怎么删，通过自省发现：主要是因为不知道文件都下载-安装哪去了、不知道linux下提供的的卸载软件的模式以及该怎么用、

- 如何自制定linux下的下载-安装位置？？


### 文件软|硬链接
在Linux的文件系统中，保存在磁盘分区中的文件不管是什么类型都给它分配一个编号，称为索引节点号(Inode Index)。在Linux中，多个文件名指向同一索引节点是存在的。

- 硬链接和软连接解决的任务是不同的：
	硬链接：像C#中给同一个实例(某一Inode Index的文件)多增加几个引用(硬链接)防止GC(误删)。硬链接只是创建了一个指向索引号的有效路径
	软连接：

#### 硬链接
- 是什么
	硬连接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬连接到重要文件，以==防止“误删”==的功能
- why need it
	硬连接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬连接到重要文件，以==防止“误删”==的功能。其原因如上所述，因为对应该目录的索引节点有一个以上的连接。只删除一个连接并不影响索引节点本身和其它的连接，只有当最后一个连接被删除后，文件的数据块及目录的连接才会被释放。也就是说，文件真正删除的条件是与之相关的所有硬连接文件均被删除。
- how use it
	1. 创建硬链接：
		ln  [源文件或目录]  [目标文件或目录]

#### 软链接
- 是什么
	软链接文件有类似于 Windows 的快捷方式。它实际上是一个特殊的文件。在符号连接中，文件实际上是一个文本文件，其中包含的有另一文件的位置信息。
- why need it
	当我们需要在不同的目录用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在其它的 目录下用ln命令链接（link）就可以，不必重复的占用磁盘空间。
- how use it
	1. 创建软连接：
		ln  -s  [源文件或目录]  [目标文件或目录]，如：
		ln –s  /var/www/test   /var/test
	2. 修改软连接(更改目标文件|目录所指向的源目录|文件)：
		ln –snf  [新的源文件或目录]  [目标文件或目录]，如：
		ln –snf  /var/www/test1   /var/test
	3. 删除软连接：和删除文件一样
		rm –rf /var/test

#### 硬|软链接的实验验证区别
```shell
[oracle@Linux]$ touch f1          #创建一个测试文件f1
[oracle@Linux]$ ln f1 f2          #创建f1的一个硬连接文件f2
[oracle@Linux]$ ln -s f1 f3       #创建f1的一个符号连接文件f3
[oracle@Linux]$ ls -li            # -i参数显示文件的inode节点信息
total 0
9797648 -rw-r--r--  2 oracle oinstall 0 Apr 21 08:11 f1
9797648 -rw-r--r--  2 oracle oinstall 0 Apr 21 08:11 f2
9797649 lrwxrwxrwx  1 oracle oinstall 2 Apr 21 08:11 f3 -> f1
//从上面的结果中可以看出，硬连接文件 f2 与原文件 f1 的 inode 节点相同，均为 9797648，然而符号连接文件的 inode 节点不同。

```
```bash
[oracle@Linux]$ echo "I am f1 file" >>f1
[oracle@Linux]$ cat f1
I am f1 file
[oracle@Linux]$ cat f2
I am f1 file
[oracle@Linux]$ cat f3
I am f1 file
[oracle@Linux]$ rm -f f1
[oracle@Linux]$ cat f2
I am f1 file
[oracle@Linux]$ cat f3
cat: f3: No such file or directory
//通过上面的测试可以看出：当删除原始文件 f1 后，硬连接 f2 不受影响，但是符号连接 f1 文件无效
```



# 一些实际需求

## 使用nfs + mount远端挂载
mount -t nfs -o nolock 192.168.0.131:/home/smm/work/hisi /nfsroot

- 需要提前设置NTFS 和 互相ping通


## linux远程登陆&&密码遗忘怎么办



## 文件的下载-安装-配置-100%删除
- windows中，如果我不提前约定一个规范(不同的文件下载到哪里)，只使用默认的下载-安装方式，那就可能会导致我删除的时候无法100%删除 -> 有的软件下次无法正常安装(ps:之前有一次因为jvm没有完全卸载干净，导致下次jvm安装报错，组后把我气晕了，听信网上的胡言改了注册表然后系统崩了​😒​)。
- 就像windows一样，linux默认也是按照它默认的逻辑安装一个软件时会分别在对多个目录产生影响，如果我们事先不约定好一个规范，那么我们可能就无法对齐进行彻底删除干净，可能一般时候不会有什么影响，但是有的时候这会导致同类型软件无法正常安装，甚至严重的时候只能重装系统。






# 疑问

- 我现在最没底的是：linux下每次删除软件怎么删？如何100%删除？(这个在windows我是很熟悉的：删除：1. control中的卸载程序等图形化操作 2. 明白了大致windows下安装一个程序文件系统会在那些地方有变化 -> 可以直接在explorer中去删除文件夹的方式来100%删除)  怎么下载软件？(下载软件：打开浏览器 -> 进官网 -> 下载安装包 -> 双击安装包安装，只需要更改一下安装包的位置，可以说是相当的简单易用了) 下载后需要怎么设置？(windows下一般就是需要设置一下环境变量，大部分是什么都不用额外设计)
	- 但是linux下安装软件、卸载软件这一部分我却心里一点底都没用：平时都是需要什么软件，直接去csdn山搜=="centos下如何安装XXX，然后将搜到的指令一行行的输入进去"==，但是我自己却完全不懂每一行指令是什么意思、背后又会给linux文件系统带来哪些改变。-> 我卸载软件的时候也不知道怎样才能100%卸载。==将linux的安装、卸载、配置软件结合linux文件系统好好学习一下==

2. 如何从符号链接 找到 原始文件的位置？？符号链接不是串行指向源文件的吗？如果只删除符号链接，那源文件没有删除


3. linux不使用图形界面，也太不友好了，连chrome这种需要鼠标点击的应用都没法用，这要怎么测试一个本地网站啊，感觉云+浏览器时代，没有图形界面系统真不行。

# bug

1. DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.


# 细节

1. linux下如何像windows下在浏览器URL栏中粘贴http://localhost:35902 一样登陆网址？？？
	1. curl http://localhost:35902
		- 只能读取出html内容，以文字版显示
	2. 在命令行下，使用浏览器来渲染html内容
		1. 安装chrome：https://cloud.tencent.com/developer/article/1722762
			- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\chrome安装.PNG" style="zoom:60%;" />
		2. 命令行下使用chrome：

2. centos下安装GUI系统
	1. 安装 : 
	2. 符号链接创建位置
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\GUI安装.PNG" style="zoom:60%;" />

3. centos下 命令行模式 && GUI模式的切换：


4. centos下删除文件
	- rm 文件名
5. 删除文件夹
	- rm -rf 文件夹名

6. 移动文件夹
	- 覆盖方式移动


7. 复制文件夹到某处
```shell
CP命令
格式: CP [选项]  源文件或目录   目的文件或目录
选项说明:-b 同名,备分原来的文件
        -f 强制覆盖同名文件
        -r  按递归方式保留原目录结构复制文件
 
cp -rf /home/user1/* /root/temp/
将 /home/user1目录下的所有东西拷到/root/temp/下而不拷贝user1目录本身。
即格式为：cp -Rf 原路径/ 目的路径/
```

