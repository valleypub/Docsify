[toc]



# 1. 本质is什么


# 2. 能用来干什么



## 1. 通常是用cmake做什么？(大众)

### 使用cmake  source code --> 编译 --> 库文件

- 1. cmake编译opencv库
```
为什么cmake可以编译opencv库，vs却不可以编译opencv??vs不是能将源文件编译成库的吗？？
```

- 2.




## 2. cmake还能做什么？？(小众)

### 封装  != 编成库？？(将C++的源码给JAVA用)







# 3. 实战

## 使用cmake 编译 vs2019使用的 opencv

### 1. 下载cmake组件

- 1. 发现cmake-gui刚好给configure按钮遮挡了，要下托才行，可把我给害惨了。

### 2. 下载opencv源码

### 3. cmake对源码进行编译

![]()

- 1. 在源码的目录下新建一个build目录
- 2. 在cmake中选则相应目录
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\11.PNG" style="zoom:60%;" />

- 3. 开始configure,会报一系列的错误：无法下载IPPCV、FFMEG

![]()

- 4. 解决3.中的错误
	- 1. 打开build下的CMakeDownloadLog.txt，根据http开头的link地址，自行翻墙下载5个文件
	- 2. 个文件名前加上MD5前缀
	- 3. 将文件复制到.cache文件夹下的相应文件夹内
	- 4. 重新configure
- 5. 开始generate

### 4. 最后一步，在vs2019中进行生成

- 6. 进入build双击OpenCv.sln文件，进入vs2019界面，如下
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\屏幕截图(2).png" style="zoom:33%;" />

- 7. 生成ALL_BUILD
	- 按下图的顺序点击，然后选择生成
	- 会在build下产生一个lib文件夹
	- debug、release均要进行一遍
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\屏幕截图(2).png" style="zoom:33%;" />
- 8. 生成INSTALL
	- 会在build下产生一个install文件夹
	- install里的include是全的
	- debug、release均要进行一边
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\屏幕截图(3).png" style="zoom:33%;" />




## bug
- why  cmake使用的下载方式是生成一个https://raw.githubusercontent.com/opencv/opencv_3rdparty/e81ccda615672833b578c6cefdb859ad69c560ba/ffmpeg/ffmpeg_version.cmake 这样的连接？？且 e81ccda615672833b578c6cefdb859ad69c560ba好像是唯一的，用别人的链接为什么不能下载，我的链接我可以使用啊，难道这种链接是一旦有一人下载成功就立马失效？？？