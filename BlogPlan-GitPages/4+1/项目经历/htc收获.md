[toc]


## htc vive 手柄控制设计部分

#### 1
- 使用```gameObject.GetComponentInChildren<Transform>()```
	- 返回值
		- 获取儿子层(子一层)的Transform组件数组
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\子一层.PNG" alt="子一层" style="zoom:60%;" />
	- 用法
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\子一层_1.PNG" alt="子一层_1" style="zoom:60%;" />
- 使用```gameObject.GetComponentsInChildren<Transform>()```
	- 返回值
		- 深度优先遍历的方式获取儿子层以下的all亲子层的Transform组件数组
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\all亲子层.PNG" alt="all亲子层" style="zoom:60%;" />



2. 获取某一游戏对象的子游戏对象列表问题化为 -> 使用Transform or 别的组件来作为选择标志 + 使用Transform获取它附加在的gameobject  
	- ![]()



3. StartCoroutine 和 yield return 和 IEnumerator的关系没弄懂



4. unity下经常用到的两种事件机制，本质相同、触发事件的方式不同
	- C# 官方的
		- EventArgs
			- ![]()
		- EventHandler
			- ![]()
		- 像函数一样触发：事件名(参数列表)；
			- ![C#版事件触发的方式](C:\Users\king-kong\Desktop\要做的事情\picture\C#\事件触发.PNG)
	- Unity官方的
		- 使用Invoke()来触发
			- ![unity版事件触发的方式]()

5. 减运算比加运算耗时？？？
	- 腐蚀-膨胀操作，使用减运算会卡掉


6. unity中同一cs脚本挂载到多个不同游戏对象上后，这些不同游戏对象上的cs脚本组件是同一副本吗？？
	- 不是。Unity脚本系统中有一句话，Asset中的cs脚本只是一个类(即，只是一个类型)，将cs脚本挂载到Scene中的游戏对象上 == 将cs脚本实例化了一个对象。根据OO我们知道，一般情况下同一类的不同对象是不同副本，只有使用static关键字 声明的 成员or类 才是共享副本的


#### 动画系统
- 支持哪些格式的model ??
- 怎么将文件夹中的 动画资源 读取出来并添加到 ModelPool的子游戏对象？
	- 这其实是属于unity的导入部分的知识https://docs.unity3d.com/cn/2019.4/Manual/ImportingAssets.html

- animation clips

- 可在unity中使用的model从哪下载
	- - StandardAssets要自己安装才能使用，比如：一些material 
	https://assetstore.unity.com/packages/essentials/asset-packs/standard-assets-for-unity-2018-4-32351?_ga=2.31862781.256443471.1627004494-44388462.1603200264&_gl=1*1glew5i*_ga*NDQzODg0NjIuMTYwMzIwMDI2NA..*_ga_1S78EFL1W5*MTYyNzAwNDQ5NC4yMy4xLjE2MjcwMTExMDUuMA..



#### 如何从资源中读到场景中？？
- fbx格式文件 && obj格式文件的区别


- fbx文件如何读取？？
	- C#有没有专门的api??
	- fbx能否和txt互转？？
	- 

##### 1. 读取阶段
- Resources.Load()方法可以直接读取FBX？？
- 使用WWW通过url的方式下载？？

- 运行时加载资源
	- [官方文档地址](https://docs.unity3d.com/cn/2018.2/Manual/LoadingResourcesatRuntime.html)
	- Resource Folders
		- 是什么
			- Unity 支持项目中的__资源文件夹__，允许在主游戏文件中提供内容，但在请求之前不加载这些内容
		- how use it
			- 创建：
			- 要将任何内容放入资源文件夹，只需在 __Project 视图__中创建一个新文件夹，并将该文件夹命名为“Resources”。可在项目中以不同方式组织多个资源文件夹。每当想从其中一个文件夹加载资源时，请调用 Resources.Load()
				- 在Unity外的电脑的资源管理器中创建Resources文件夹行不行？？
			- 加载：
			- 通过 Resources.Load() 只能访问 _Resources 文件夹_中的资源。然而，更多资源可能最终出现在“resources.assets”文件中，因为它们是依赖项。（例如，Resources 文件夹中的材质可能引用 Resources 文件夹之外的纹理）
				- [Resources.Load()官方文档](https://docs.unity3d.com/cn/2018.2/ScriptReference/Resources.Load.html)
			- 释放：
			- 如果要在加载另一个关卡之前销毁使用 Resources.Load() 加载的场景对象，请对这些对象调用 Object.Destroy()。要释放资源，请使用 Resources.UnloadUnusedAssets()。



##### 2. 实例化阶段
- 预制件(Prefabs) && 实例化(Instantiate())
	- https://docs.unity3d.com/ScriptReference/Object.Instantiate.html#:~:text=Instantiate%20can%20be%20used%20to%20create%20new%20objects,or%20particle%20systems%20for%20explosion%20effects.%20using%20UnityEngine%3B
	- https://docs.unity.cn/cn/2019.4/ScriptReference/Object.Instantiate.html



##### 搭配方案
- Resources.Load() + Instantiate()
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\运行时加载.PNG" alt="示例" style="zoom:100%;" />
	- 由于以下原因没有使用此种方案：
		- Resources.Load()只能读unity下的project视下的Resource文件夹下的文件
		- unity下的project视下的Resource文件夹下的文件和本机FileSystem下的Resource文件夹下的文件不一致
		- 最重要的一点：
			- 使用Resources文件夹必须是在unity Editor中进行操作，首先要将fbx拖到unity project视图下的Resources文件夹中，而我们只提供给客户打包后的程序，他们知恩能通过本机FileSystem来加载模型。

- 使用 本机 -> WWW -> Resources文件夹 -> Resources.Load() + Instantiate() -> Scene
	- 比较繁琐，没有测试

- 使用TriLib插件
	- good




##### bug

1. prefabs直接拖进scene中会直接转成GameObject，


2. 要给model物体上加上BoxCollider组件
	- 不然射线是没有办法与他进行物理碰撞的(即，Physics.Raycast(ray, out hit)会不起作用)，具体的表现是：1. 即使我给model组件设置了tag = model 还是射线不变色 2. 正常情况射线射到model上会产生一个终点，但是这个射线会从model中穿透过去

2. 要给model物体设置tag
	- 不然ray碰撞没法变色
2. 要给model添加OrderReciver组件
	- 因为update中 if(isLocked){}中用了```var orderReciver = objCheck.GetComponent<OrderReciver>();if (orderReciver != null)```不然没法使用鼠标控制  放大、缩小、旋转等手柄操作

4. obj.transform.positon 和 obj.transform.localPosition的区别。why设置```HKMJFBX.transform.position = new Vector3(0.01f, 0.06f, 0.01f);```无效；但是设置```HKMJFBX.transform.localPosition = new Vector3(0.01f, 0.06f, 0.01f);```却可以？？？？
	- 1. position是根据世界原点为中心
	- 2. localPosition是根据父节点为中心,如果没有父节点,localpositon和position是没有区别的
	- 这就是why ```HKMJFBX.transform.localPosition = new Vector3(0.01f, 0.06f, 0.01f);``` 效果 == ```HKMJFBX.transform.position =HKMJFBX.transform.parent.position + new Vector3(0.01f, 0.06f, 0.01f);```

5. 目前到这：将model prefabs拖入unity的project视图下的Resources文件夹下 + 使用Resources.Load() + Instantiate() 是可以的，但是直接从(win + e)中的Resources中使用Resources.Load() + Instantiate()操作fbx文件却不行。why??
	- 测试发现是卡死在了GameObject newInstance = (GameObject)Instantiate(obj);这一步
	- 那，既然使用Resources.Load()直接从fbx读不行，那就分两步，1.从fbx读成prefabs 2. 从prefabs 经过Instantiate(Resources.Load())变成gameobject


6. why 将fbx文件放在(win + e)中的Resources文件夹下，会在```GameObject newInstance = (GameObject)Instantiate(obj);```这一步失败，但是将fbx文件直接拖到Unity的project视图下的Resource文件夹下就整个都会成功？？？
	- 而且，(win + e)中的Resources文件夹 和 unity中project视图下的Resources文件夹不是实时同步的
		- 要下一次打开才会生效吗？？？？
			- 不是。下一次打开仍没有用。仿佛 win+e中的Resource文件夹 和 Unity Project中的Rsources就是两个东西

7. Resources这种动态加载方式是只读的，在游戏打包后，就无法对文件夹的内容进行修改
	- 因为我们最终只给打包版 -> 无法使用Resource的方式来动态加载fbx文件了


- why 在unity Project视图中显示的是prefabs ,但是从unity外部的计算机资源管理器(win + E)中看到的却是fbx文件？？而且why在C:\Learning\MR_kinect_test3_19\Assets\Models中打开SciFi_Fighter_AK5.FBX是有纹理的，但是单将SciFi_Fighter_AK5.FBX拖到桌面再打开却又是无纹理的？？？
	- [如何给fbx文件设置纹理](https://www.cnblogs.com/ezhar/p/13258974.html)



- 使用 http + resource.load()的方式？？

- 明天试一试这个https://www.cnblogs.com/wuxingJS/p/13954400.html
	- 使用TriLib插件确实可以进行本机FileSystem的导入
		- 测试的同步方式可以的
		- 测试了使用"C:/Learning/MR_kinect_test3_19/Assets/MR/MyModels/SkyCar.FBX"这个是可以的

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 现在能进行传fbx了
- 但是，人有以下几个待解决的问题：
	- fbx的纹理怎么通过脚本传过去？？为什么传过去的是没有纹理的？？
	- fbx上带的动画怎么传过去？？
	- 怎么通过脚本对动画进行播放设置？？ play pause stop 前进指定帧 后退指定帧

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 有的FBX是完整打包的：即一个FBX就含有结构、纹理、Animation，这种FBX怎么制作？？？？或是说怎么确定制作的FBX是包含纹理、Animation的？？


- 怎么控制FBX导入进来后的Animation动画？？

- Animator 和 Animation的关系

- 导进来的FBX上的动画可能是以多种插件的方式来的：
	- unity下捕获fbx上的动画会捕获成哪几种组件格式？？
		- Animation组件
		- Amator组件
	- 对不同的组件进行不同的控制
	- 首先肯定是在选中态下(objCheck == 当前模型)才能对Model上的动画进行控制
		- 不，不能使用选中态，要使用非选中态下来播放model的动画，因为选中态下为了实现对不同游戏对象的控制的统一性(PPT、 ModelPool)，导致手柄上的按键都被占用了，而非选中态下的按键还有空余，就选在非选中态下。
		- 











- 模型制作的规格上的问题：
	- model导入的位置我是可以通过localPosition来设为new Vector3(0.01f, 0.06f, 0.01f);这个位置
	- 但是，
	- 我不知道他导入的模型的原始scale，我该让localScale在一个合适的大小？？？？

- 而且我发现，当scale缩小的太多时，就不好通射线 + BoxCollide + 来进行选中了，选中的好像是很小的一部分，必须知道那一部分才能选中，以缩小那一部分也跟着缩小就不好选中了



- C# Application类的dataPath、streamingAssetsPath、persistentDataPath、temporaryCachePath


- unity 的WebRequest（原WWW功能）整理一下






- 对于Screen物体上的play 使用的是CallApp.controlMsg 和 OrderType 的rotate标记，是由于手柄上按钮有限的缘故，但是对于键盘这种按钮众多的设备，还是新增一个专门的枚举flag一个比较好



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 实际上，讲解端和参观端是功能不对称的，但是我们之前开发的时候都是将他们当成对称的来进行开的，这样其实给结构带来了不必要的复杂和混乱，如下：
	- 讲解者端才有PPT 和 Model这些文件内容怎么同步到参观者端？？？
		- 使用云服务器？？+ 文件服务器？？
	- 由于讲解时需要双方看到的Model和PPT是一致的，故需要设计一个状态同步功能，即：
		- 讲解者对PPT Model的操作（上一页、下一页、video Play Pause  animation Play Pause 快进 倒退 放大 缩小等）要立即传递到参观者
		- 参观者对PPT Model的操作（上一页、下一页、video Play Pause  animation Play Pause 快进 倒退 放大 缩小等）也要立即传递到讲解者端
		- 我设想的只是基于展示内容抽象级别的同步，即，只需要同步双方对PPT currentModel的操作,而参观者通过ray选中别的什么游戏对象并不需要进行同步
	- 现在问题是同一端需要在多少个组件上加上ManageMessageFromCallApp()这个状态更新函数？？
		- 按理说，有一个组件上有这个函数应该就能更新场景中的这些状态了，因为都是引用的关系

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


- 为什么使用基于事件的<img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\unity按键检测ppt更新_基于事件的.PNG" alt="基于事件的" style="zoom:60%;" />就会出奇怪的问题![](), 而使用基于组件直接调用的![基于组件直接调用的]()就没有问题
	- 基于事件更新的：
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\unity按键检测ppt更新_基于事件的.PNG" alt="基于事件的" style="zoom:60%;" />
		- 出的bug:
		- 按下一次下一页ppt
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\unity基于按键的PPT更新_基于事件的_出的bug.PNG" alt="出的bug" style="zoom:60%;" />
	- 基于组件直接调用的：
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\unity基于按键的ppt切换_基于组件直接调用的.PNG" alt="基于组件直接调用的" style="zoom:60%;" />
		- 这个就没有bug




- 鉴于ControlPPTAndModelByExplain不通过当前选中对象objCheck的方式来进行的ppt model的切换和更新，故不能直接使用callApp.Send(CallApp.controlMsg.zoomOut.ToString());来将信息发送到对端，ControlPPTAndModelByExplain中对端控制信息发送部分是错的
	- 因为接收端ControlerHighlightAndOrders脚本中的状态更新，是通过接受对端发来的CallApp.controlMsg然后通过作用到当前的选中对象objCheck上来进行的同步，但是发送端可能是由ControlPPTAndModelByExplain脚本组件发来的，此时是直接对ppt model的操作而不一定是对当前的objCheck的操作，而接收端会将这个操着莽撞的作用到objCheck上，极大可能会导致不一致的情况。(如：ControlerHighlightAndOrders脚本操作的是ppt物体，但是当前选中物体是Model，此时对端会将接收到的作用到ppt上的操作作用到当前的objCheck = Model上，必然是不合理的)
	- 故，我的考虑是：对于每一端只让一个ManageMessageFromCallApp()函数起作用(防止出现混乱的情况)，将这个函数关在到某一个组件上，通过这个组件统一接受对端的同步数据和统一对scene中的游戏对象进行同步更新处理



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 鉴于上述的种种隐藏问题，在此重新设计两端的同步方式
- 要将参观者端一开始是没有展示内容(PPT Model)的，这一点考虑进去，如果此时两端的同步只是收发指令的话，很可能对不齐：如：讲解着这端当前指向第4张ppt，然后将内容通过服务器发送到接收端，此时在接收端还没有接受好的时候，如果讲解端就开始切换ppt，此时讲解端便指向第5张，接收端指向初始的第0张
	- 解决方案：发送的时候，连带着将当前的iIndex也发送过去，而且在接收端接受内容成功前讲解端不能操作 PPT or Model
		- 使用Icall中提供的文件发送来试试

- 下面的是两端内容同步后的问题：现在假设两端都拥有了内容(PPT Model)，而且当前iIndex都是一样的(即，已经同步了)
	- 1. 如何在允许多种输入设备操作(手柄，键盘，蓝牙键盘)的方式下实现统一同步？？
		- 重新设计全局同步更新逻辑
		- 不能在基于当前物体检测了来实现同一指令不同当前对象不同执行方式的复用(短板效应：由于键盘更新方式无法选中游戏对象故，直接在键盘方式中直接弃用选中对象更新的模式)，故整个需要在将控制指令发送给对端时就必须完全标识出是对哪个游戏对象的控制指令，这需要增加ICALL中的CallApp.controlMsg中的枚举flag数目
	- 2. 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- CSharp类内的成员可以像C++一样使用外部定义，平时使用VS跳转观察的都只是类内生命，类外的成员定义写成源文件编译成dll,

- 因为两端的工程一样，两端使用explainerToggle区分讲解者、参观者

- 之前的不按功能来附加脚本组件，而是将脚本组件乱加到不相关的游戏对象上，导致结构混乱，违背了软件开发的原则：不额外引入混乱
	- 如：
	- why要将leapmotion相关手势控制的组件附加到telephone电话对象上？？
	- why要分两套全局状态更新函数分别在ControlerHighlightAndOrders和LeapControl内？？这样不好做全局统一吧
		- 基于此，我将全局状态更新剥离成一个单独的SynchronizePPTAndModelByControlFromOpposite组件，专门用来进行对端控制的更新


- why public enum controlMsg里面的成员开头不能大写？？
	- PPTUp死后不行
	- pptup就一点问题没有


- 为什么使用because-why-not使用空白(即，使用免费的信令服务器) + 设置turn ice服务器网址  无法穿透校园网，但是可以穿透手机热点组成的局域网
	- 但是，我使用MRTK的信令服务器 + 设置同样的turn ice服务器网址 却可以穿透校园网，why???
	- 是不是因为，because-why-not免费的信令服务器 并没有用上这个设置的turn ice服务器网址 ???因为我在MRTK中实验出来这个设置的turn是可以的


- 按键一点一点的太累手了，能不能设计个长按机制？？？？


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 实现Screen组件上的videoplay的播放和暂停
	- 还没有写
- 实现fbx上的动画的播放暂停问题
	- 还没有写

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


- 将原先的vive手柄上的操控-同步方式也改成全局统一的
	- ok了，除了一点：vive的rotate时一直旋转，但是键盘的是转一个角度，这一点怎么解决？？


- 为什么有的FBX就是没法使用TriLib读进去呢？？改文件名也不行
	- 能正常使用TriLib读进去的，改了名字后仍然能读进去，说明能不能读进去和文件名无关，那就是fbx本身的问题了？？？究竟什么样的FBX文件才能正常读进去呢，好方便人家照这样的模式来开发FBX呀

- 写一个自动获取指定文件夹下所有指定后缀名的完整文件路径的函数
	- 不同层按深度优先遍历来，同一层按什么标准来排序？？
	- 1. 判断一个"xxxxxxxxxxx"是目录or文件夹
	- 2. 是文件的话如何获取他的绝对路径
	- 3. 是目录的话，如何读取它内的所有内容

- 判断一个FileSystemInfo info 是文件 or 路径
```
	//判断一个FileSystemInfo info 是文件 or 路径
	private void GetAllFile(FileSystemInfo info)
    {	
    	//判断是否存在
    	if(!info.Exist){
		}else{
            //是否是文件
            FileInfo file = new FileInfo(info);
            if((file.Attributes & FileAttributes.Directory) != 0){
            //是目录
            }else{
            //是文件
			}
         }
	
```
```
	List<string> fileAbsolutePathArr = new List<string>();

	private void GetAllFile(FileSystemInfo info)
    {	
    	//判断是否存在
    	if(!info.Exist){
		}else{
            //是否是文件
            FileInfo file = new FileInfo(info);
            if((file.Attributes & FileAttributes.Directory) != 0){
                //是目录
                DirectoryInfo dir = info as DirectoryInfo;
                //DirectoryInfo dir = new DirectoryInfo(info);
                FileSystemInfo[] temp = dir.GetFileSystemInfos();
                //每一个变为第一级的info
                foreach(var i in temp){
                    FileInfo fileTemp = new FileInfo(i);
					if((fileTemp.Attributes & FileAttributes.Directory) != 0){
						//是目录
						GetAllFile(i);//使用递归
					
					}else{
						//是文件
						fileAbsolutePathArr.Add(fileTemp.FullName);
					}
                }
            }else{
                //是文件
                fileAbsolutePathArr.Add(file.FullName);
            }    
    
    }

```

-  另一个版本:深度优先递归

```
	private void GetAllFile(FileSystemInfo info)
    {	
    	if(!info.Exits){
    	
    	}else{//只要存在，必定只有两种可能性：文件、目录
    		//是否是文件
            FileInfo file = new FileInfo(info);
            if(file != null){
            //不能使用if((file.Attributes & FileAttributes.Directory) ==0){
            //如果file为null的化会卡死在这一步，因为null没有Attributes属性
            	//是文件后要判断是不是我们要的制定后缀的
            	if(ExtansionIsXXXX(file.Extension)){
					fileAbsolutePathArr.Add(file.FullName);		
				}
			}else{
				DirectoryInfo dir = info as DirectoryInfo;
                //DirectoryInfo dir = new DirectoryInfo(info);
                FileSystemInfo[] temp = dir.GetFileSystemInfos();
                //每一个变为第一级的info
                foreach(var each in temp){
                //因为每个都是FileSystemInfo类型的和最外层的，已经可以使用递归了
                GetAllFile(each);         
                }
			}
    	}
    
    
    }
    
    
    bool ExtansionIsXXXX(string path){
		string[] imageName = { ".jpg", ".png", ".gif", ".bmp", ".psd", ".tga", ".psd", ".JPG", ".PNG", ".GIF", ".BMP", ".PSD", ".TGA", ".PSD" };

        for (int i = 0; i < imageName.Length; i++)
        {
            if (name.Equals(imageName[i]))
                return true;
        }
        return false;
	}

```

- 如何制定读取的顺序？
	- 文件名靠前的优先读？？
	- 我上面写的深度优先的版本同一级是按什么优先级来的，即本质是FileSystemInfo[] temp = dir.GetFileSystemInfos();这一个函数是怎么读的，，什么准则？？能否自指定准则？？


- 使用最简单的复制粘贴方式时，此时使用trilib按深度优先的方式读取出来的顺序是什么：
	- 测试：
		- ppt的顺序
			- 命名规则按：
				- 各字母不区分大小写，尽量全使用小写方式
				- a
				- aa
				- aaa
				- aab
				- aac
				- ...
				- ab
				- aba
				- abb
				- abc
				- ...
				- ac
				- ..
				- b
				- ba
				- baa
				- bab
				- bac
		- video的顺序
			- 同样
		- model的顺序
	- 因为文件夹中对这类文件是按文件名这样比较排列的


- 使用Input.GetKeyDown("r")后，无论是大小写的 R r均可以识别


- 将视频和ppt进行分离，场景中专门做一个Watch游戏对象，专门用来播放视频。将video ppt model变成三个平行对等的内容部分
	- 由于要让讲解者能从本机file sysytem中添加video文件到scenen，故不能使用video clip的方式，因为video clip的方式，需要使用拖动的方式来从原始视频文件(.mp4 .avi)创建video clip
		- 最简单的是使用url的方式
			- 但是这个方便使用脚本进行播放控制吗：快进、倒退、播放、暂停
			- 方便读取多个吗？？
				- 通过一个函数读出指定文件夹下的所有指定后缀(如：.mp4)文件的全部绝对路径，然后添加file://前缀，然后再C#脚本中通过更改url来实现videoUPDown ？？？？
		- 能不能使用TriLib来读？？
			- 这个方便设计读多个，
			- 但是，这个读进来的video源文件是video clip吗？？(即，和拖动方式建立的有没有区别？？，即，能不能用)
			- 

- 如果使用inspector设置video clip+ Material Override + __mainTex__的方式会出bug: 音轨能播放，但是没有画面，unity版本为2018.2.0f2
	- 最后的解决方案是：
		- 不使用Material Override转而使用RenderTexture的方式，通过提前设置一个用于缓存videoPlayer的输出Target Texture的RenderTexture预制件，再创建一个Material预制件引用前面创建的RenderTexture预制件，RenderTexture预制件、Material预制件是随videoPlayer更新的，然后Watch上的MeshRender引用Material预制件即可。
	- 但是，使用C#脚本 + video clip+ Material Override + __mainTex__的方式就一点都问题没有：
		- ![使用C#脚本](C:\Users\king-kong\Desktop\要做的事情\picture\unity\C#脚本方式使用videoPlayer.PNG)


- 由于考虑到切换videoUpDown的时候，焦点在video上，故。此时直接播放视频是只有好处没有坏处
	- 在程序上就是，每次切换视频的时候，直接紧跟着一次Play操作

- 讲些好的videoPlayer这一部分同步到键盘方式-讲解者端脚本中，和手柄段-参观者脚本中，并且由于两端声音可能不一样标准，故此部分传输只传IIndex索引，Volume的操作不穿

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 设置分屏播放display
	- 怎么__自动化的__将用户的视角图输出到外接的第二显示屏上？

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 可能是通过steamvr 的某些方式将 头显的视角关联为VisitCamera的视角
	- 后续就直接认为VisitCamera的视点为参观者视角

- 获取参观者视角并发送可以放在任何脚本上，或者放在一个专门的脚本，专门的空物体上，只需要通过获取一个CallApp的引用来使用send()发送功能即可，
	- 当前，是将采集这部分放在了CallApp上
	- 我，准备写成个独立的脚本


- 由于callApp是两端p2p的，是webrtc核心，我们在一端发的，都会在另一端被接受到，故，要在CallApp中的接受事件中(因为使用的send()故接受时的事件类型为Message)，在对端CallApp的Mesage中写接受了发来的头衔数据后该作何中处理：
	- 当前的同步头显位姿的方式为：先缓存到CallApp中，再被VisitCamera上的visitView脚本引用来更新接收端的VisitCamera组件的位姿和发送端的VisitCamera组件的位姿一致，然后再将VisitCamera组件的当前捕获的Texture缓存到预制件VisitRenderTexture -> VisitMaterial 再将材质渲染在接收端的visitObj屏中屏物体上
	- 这一个大过程，是有很多步的优化空间的：尽量让结构变得简单，不要可以引入混乱
		- 在我看来：中间有几步可以不要



- display设置分屏显示的问题
	- 1. camera组件上的Target Texture要设置为none，不然即使设置了camera的Target Display也不会真的将画面投到display而是投到Target Texture上
	- 2. 使用第2 、3、屏幕，不是简单的设置多个camera，meigecamera设置Target Display ，将各个屏幕连接到主机上就行了。即使将显示屏接到主机上了，只要不设置使用C#脚本激活第2，3，屏幕，屏幕就不会被检测、使用
	- 3. 统一display上若有多个camera同时使能，会显示depth值最大的那个camera捕获的画面
	- 4， 为什么有的camera设置的好好的为什么就是画面全黑(没有画面)呢？？
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\camera问题.PNG" alt="camera没有画面" style="zoom:60%;" />




- Awake()和Start()谁先执行？？
- Awake()是不是只在Editor方式存在，对于打包好的unity程序还存在这个过程吗？？


- 关于unity的长安旋转，直接单独写成一个版本，触按写一个版本
	- 

- 因为我键盘的方式操控，只允许screen的翻页，model的翻页、缩放、6各方向的旋转、动画的控制，video的播放
	- 防止两端的内容不同步，对于内容相关的物体(ppt model video)，必须从程序运行开始到程序结束期间完全同步，这就需要键盘方式操控&&手柄方式可操作种类必须完全一致



--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

体验提升上的几点改进

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 将鼠标的相关功能去除


- 将ppt video model的操作先知道connect建立后才能进行操作来保证连续性


- 将接收端的渲染计算量移到发送端来实现






--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- 同样的程序 + 同样的网卡 ，PC不同：
	- 主机：刚开始还行，过个几分钟(甚至1分钟)会很卡，用不了多久就会"奇怪的卡掉"(即，ppt切不了，data更新不了，但是并不是程序卡死，因为此时“关闭按钮”还能按还能正常退出)，经测试(通过段输出测试)发现是由于CallApp进入了新的连接状态：CallEnded，(注意：如果连着多台，此时每两两都会建立连接，哪怕只其中一台退出时，所有的与退出这台相连接的都会进入CallEnded而不管是不是仍与某几台正连接着)
	- PC：从一开始就挺卡的，但是等了好久程序就是不会进入"奇怪的卡掉"(即，ppt切不了，data更新不了，但是并不是程序卡死，因为此时“关闭按钮”还能按还能正常退出)状态

- 同样的程序 + 同样的主机 ，网卡不同：
	- 自带的网卡：不太卡
	- 使用RTL8188：很卡

- 同样的程序 + 台式机 ，网卡|网线
	- 网卡：会发生奇怪的卡掉
	- 网线：很正常

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------







--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

对于camera还是不够熟悉，对unity的图形系统也不够熟悉，后续再深入研究一下图形系统、camera系统

- why 有时候同一scenne中有多个camera使能时，why有时更改相机的depth没用？？是因为运行时更改不起效果？？那更改还有什么意义呢

- 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------




- 由于htc头显定位是相对地址，要将头显融进Unity场景里，需要给头衔指定一个初始位置，头显基于这个初始点进行相对运动。现在有一个问题：由于定位器的高度设置，

	- 通过一个extra的比头显的eye相机优先级(depth更大)的StaticCameraForListner相机来实现，参观者端显示头显eye camera所看画面，讲解者端在一个更高的位置观看画面(这样讲解者端才能看到模型)，这样才能只使用一份APP来实现两端的不同的效果，但是由于多了一个脚本挂载在VisitCmaera上不同的Update势必会耗费性能

- 不能将控制游戏对象A的 SetActive()的脚本挂载在游戏对象A上，因为一旦A被SetActive(false)了，那脚本也就不不能使用了，没法进行后续的控制了
	- 如：我对于使用callApp.explainerToggle来控制StaticCameraForListner最开始的bug




----
最后几个bug

----


- 为什么callApp脚本中的mCall = null；后，Update()不运行了？？mCall和callApp本身没有关系的吧，就算mcal =null; callApp组件应该继续运行啊
	- 应该是引用建立失败导致的，在做传屏幕数据的时候也遇到过这个问题，那时候就是因为众多引用中有一个引用的建立有问题，导致monobehavior的start update均无法运行。


----
第二显示屏的、画中画的刷新问题：

----

1. 使用获取相机数据 + webrtc传输的方式还是有点慢，是哪一部份慢了：
	- webrtc这一部分应该没问题，因为传输粒子用的一模一样刷新率就没有问题
	- 应该是Render Texture 或 ReadRawTexture出的问题，我记得MRTK中有传屏幕的这一部分的实现，看看他们是怎么优化的


- render Texture的方式不能用，太卡了，update中有个函数在不停的new，只使用GC的话就会很卡


2. 对于Texture2D要想使用loadRawByte readRawBytes 必须在Texture2D声明的时候就对齐，采集和显示两部分的格式(width height TextureFormat.ARGB32)均要一致才行，不然会出现图片条状乱码的问题，

3. 使用Screen.width Screen.height获取的是Editor下Game视窗的pixel的大小，如果手动改变Game视窗的大小(拉大，缩小)这个值会变

4. 为什么在monobehavior中读出的Screen的width height 和在 OnPostRender中读出来的不一样？？差了一。而且使用如下图的方式：无法进行正常渲染，在Editor下将图的规模缩小为967 598能显示但是是错位的，在runtime下，直接用1920 1080直接不显示了
	- ![]()


5. 如果按下面的方式写，会报这个错误：ReadPixels was called to read pixels from system frame buffer, while not inside drawing frame.UnityEngine.Texture2D:ReadPixels(Rect, Int32, Int32)
	- ![](C:\Users\king-kong\Desktop\要做的事情\picture\htc\屏幕截图报错.PNG)
	- 错误的意思就是说ReadPixels是从系统缓冲区帧里找像素而不是从图框内找。简单说就是，你的图应该先在Camera渲染完，存进缓冲之后再ReadPixels。所以修改方法就是，把Update换成OnPostRender，这个函数只有在摄像机下才会执行，摄像机每帧渲染完执行。在Update后执行。
	- 解决办法：
		1. 协程的方式
		2. OnPostRender



6. 为什么有时候Editor下，运行后没办法关闭，运行一会之后电脑屏幕都黑了
	- 是因为new 太多对象没有释放 GC崩了？？？


7. 是GetRawDataByte	 LoadRawDataByte 比较慢吗？？为什么刷新率这么低呢？？？



----

最后的几个bug：

----
1. 由于时延导致的动画暂停位置不同步问题。因为每次传的是指令(pause、play)，假如A、B端在同时运动，此时A端pause,然后将pause指令发到B端，B端接收到pause指令然后pause，由于Pause指令的传输需要一段时间，但这段时间内A端的已经停了，B端的还在运行，就会导致B端和A端的暂停位置不同。
	- 改进思路一：既然指令传输有时间，A端先发送指令再执行指令，这样可以节省一点时间

2. 在一端断开连接再连上后，此时两端PPT会不一致。比如：A端在断开连接时，AB两端正在放映5号ppt，但是A端断开后，重新连接，此时A端从0号ppt开始初始放映，但是B端仍停留在5号ppt,就会产生不同步问题。
	- 解决办法，使用绝对的号码(索引)来进行ppt切换，这样不管中间是什么顺序，只要播放一个就会立马同步



3. 一个Scenen中如果有两个Canvas且一个Canvas投到dispaly1 一个投到display2，此时如果程序运行的环境没有接display2，此时canvas1上的UI元素无法正常点击。如果此时，外接一个display2就可以displa1上的canvas1也就能正常点击了
	- 我一开始还以为程序的问题




4. 为什么会出现 update（）中会有很多不执行的bug?? 只有call == null时update（)不执行，且发送端就没这个问题，，，引用也没有问题，因为在call 变得 !=null的一瞬间 内容reset了，说明成功的在update()中趁着connecte建立连接这个空挡执行了几十针 update,,,,,为何call == null就不行，且接收端 call == null就行？？？太不稳定了吧



## unity几个系统的学习

### 动画系统

### 视频系统
#### unity视频概述
- 一切物体(游戏对象)均可以播放视频，即变成一个视频播放器。
	- 1. 不管游戏对象形状(即mesh)
	- 2. 只要游戏对象上拥有MeshRender组件
	- 3. 同时，在游戏对象上加上VideoPlayer组件，游戏对象即变成了一颗播放视频的奇形怪状的电视机
#### VideoPlayer组件的使用
- videoPlayer组件支持的视频文件格式：
	- .mp4
	- .mov
	- .webm 
	- .wmv
##### 通过Inspector + 拖动的方式使用VideoPlayer组件
###### Material Property栏设置
- 默认情况下，视频播放器组件的__材质属性 (Material Property)__ 设置为 __MainTex__
	- 这意味着视频播放器组件附加到具有渲染器的游戏对象时，它会自动将自身分配给该渲染器上的纹理（因为这是该游戏对象(VideoPlayer组件所附加在的游戏对象)的主纹理）。

###### Render栏设置
- VideoPlayer组件的Render栏中的值
	- 如果VideoPlayer组件所在的游戏对象上具有Mesh Render组件，则VideoPlayer组件会默认自动将Mesh Render组件分配给 Renderer 字段，这意味着video Clip会在Mesh Render的纹理上播放
	- 如果VideoPlayer组件所在的游戏对象上不具有Mesh Render组件，则Renderer 字段默认为空
###### Video Clip栏设置






##### 通过C#脚本的方式使用VideoPlayer组件

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\videoPlayer组件使用.PNG" alt="脚本方式使用1" style="zoom:80%;" />

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\videoPlayer组件使用1.PNG" alt="脚本方式使用2" style="zoom:90%;" />



##### VideoPlayer组件使用的简单例子

#### 视频源
- 用来导入videoPlayer组件的原始视频文件

- videoPlayer组件支持的视频文件格式：
	- ![ videoPlayer组件支持的视频文件格式](C:\Users\king-kong\Desktop\要做的事情\picture\unity\videoPlayer支持的视频文件格式.PNG)

- videoPlayer组件支持的导入的视频源方式
	- video Clip
		- 通过拖动video的方式创建video clip
		- 将video clip拖动到video Player的video Clip栏
	- url
		- URL 源选项会绕过资源管理，这意味着您必须手动确保 Unity 可以找到源视频。
			- 例如，一个 Web URL 需要由 Web 服务器托管源视频，而普通文件必须位于 Unity 可以找到该文件的位置（用脚本表示）。但是，如果内容不在 Unity 的直接控制之下，或者您希望避免在本地存储大型视频文件，则此功能非常有用。
		- 本机文件使用file://前缀
			- 如：file://C:/Learning/video.mp4
		- web文件使用http:// 或 https://前缀

#### 输入系统
- 通过 Input.GetKeyDown("up") 起作用，Input.GetButtonDown("up")不起作用 Input.GetButtonDown("Jump")又起作用，发现 按键Key和按钮Button还是有一些区别的
	- 对于keyboard上的全体而言
		- 使用 "left ctrl" KeyCode.Return 等两种使用方式
		- 所有Key都是原生支持：Input.GetKeyDown() Input.GetKeyUp() 的，但是要想Key支持GetButton系列如：Input.GetButtonDown()，是需要在虚拟轴中进行设置的：Edit -> ProjectSetting -> Input
			- 如：之所以Jump可以使用Button是因为Jump虚拟轴名称是提前设置好的，可以看到：<img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\Junp和space的关联.PNG" alt="Jump与space按键的关联" style="zoom:60%;" />


##### unity键盘的使用
- 本质是充分利用keyboard上的各个key
	- 直接使用
		- 通过GetKey系列方法  GetKey GetKeyDown() GetKeyUp()
	- 通过虚拟轴，将key当成buttton
		- 建立Key和虚拟轴名的关联
			- 如：Jump -- space
		- 通过GetButton系列方法来使用 GetButtonDown()


##### unity鼠标的使用

- 直接使用
	- 通过GetMouse系列方法 GetMouseButtonDown(int)
		- 鼠标左键-- 0 鼠标右键--1 鼠标滚轮 -- 2
- 通过虚拟轴的方式，将MouseButton当成Button
	- MouseButton与Button建立关联
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\MouseButton与虚拟轴关联.PNG" alt="建立关联" style="zoom:60%;" />
	- 通过GetButton系列方法来使用，如：Input.GetButtonDown("Mouse X");

- 鼠标左键 -- mouse 0 -- 0
- 鼠标右键 -- mouse 1 -- 1
- 鼠标滚轮 -- mouse 2 --2 
- 鼠标滚轮怎么使用？？？
	- 直接使用
	- 与虚拟轴怎么进行关联？？
	- 我想要的使用方式是，能检测出是向上滚动or向下滚动，即我想将滚轮当一般button来使用



#### 图像系统
##### camera组件的学习
###### camera的输出渲染
一般情况下，摄像机直接渲染到屏幕，但对于某些效果， 将摄像机渲染到纹理会非常有用。当 targetTexture 为 null 时，摄像机渲染到屏幕(即，Target Display)。

- 摄像机直接渲染到屏幕

- 摄像机渲染到纹理
	- 使用RenderTexture方式
		- 可以创建一个 RenderTexture 对象， 在摄像机上将其设置为 targetTexture，相机会将将输出输出到targetTexture中设置的RenderTexture 对象上，而不再输出到屏幕。随后，可在程序运行期间灵活的使用这个RenderTexture 对象来实现一些功能，如：	
			- RenderTexture 对象提前关联到一个Material上，然后再将这个Material赋给别的游戏对象的Render组件的Main Teture上，这个物体就会被实时渲染为camera捕获的画面(即，可以当一个TV来使用)
			- [官方文档](https://docs.unity3d.com/cn/2021.2/ScriptReference/Camera-targetTexture.html)
	- 使用SetTargetBuffers方式
		- 让摄像机渲染到单独的 RenderBuffers
		- [官方文档](https://docs.unity3d.com/cn/2021.2/ScriptReference/RenderBuffer.html)


Screen类

RenderTexture 

RenderBuffer

Camera

Graphics

###### 获取camera呈的像并使用webrtc进行发送
- 原始版本是将 camera_eye(头显)的坐标 实时传给 visitCamera，在将visitCamera视角的画面Target Texture到预制的RenderTexture，再将这个RenderTeture 贴到 VistObj小窗口物体上，实现画中画功能。
- 现在的版本是，获取头显camera_eye看到的的所有画面，Target Texture到 预制的RenderTexture上，然后使用{GetRawTextureData LoadRawTextureData(bytes) Apply}而不是{EncodeToPNG LoadImage(bytes)}(这种或有一个问题：同样的camera_eye使用EncodeToPNG读出的byte的长度不同，即两端不对应) 读出bytes ,将bytes使用webrtc传到讲解者端，讲解者端使用{LoadRawTextureData(bytes) + Apply}来将byte恢复为Texture2D，然后再将这个Texture2D应用到游戏物体(如：visitOBJ)orUI元素(如：rawImage)上

- 注意：必须严格将接受的266144长的byte数组按照camera_eye的render Texture的width heigh尺寸先恢复成Texture2D格式的backup，然后对于将backup应用到什么尺寸的物体or rawimage上没有要求，why????

- 必须将camera_eye设为Target Render才能将输出传到对端，如果Target Render为空，讲解这段一直收不到数据，是因为根本就不会发数据过来

- 测试发现一个大bug:
	- 正常情况下，如果visitcamera、 camera_eye设为Target Display那么他们两个的tansform会随头显实时变化。但是他们两个中一旦哪个设为Target Render那么这个camera的transform便不会再变化了，因为transform不变 -> 这个render texture中的数据为固定的，就无法实现动态的双端画面同步了 
		- 如何将camera变化的画面输到render texture？？？
		- 如何获取一个camera的动态的画面？？？？
		- ==由于我发现，有一种使用camera使用render texture能实现画面动态：将cameraA设为Target Render ，运行时我们动态的设置cameraA的transform，那么cameraA会自动将不同transform下的视图输出到Taarget renderTexture上== 。 可以另外设一个camera ,在脚本中动态的将camera的transform与camera_eye的同步(此时camera_eye已经不作为Target Render输出，只需要用到他的变化着的tansform)，然后再将camera的render texture发送过去
			- 但是，这样肯定还没有原始版本快呢，因为在原始的版本的全部工作都做的基础上 还外加了webrtc
		- ==能不能以更快的方式获取camera位姿下的试图？？？==


###### bug

- 为什么按下面的方式使用Tetxur2d的大小不敏感？？

```
Texture2D backup = new Texture2D(100,100);
				if (backup.LoadImage(bytes)) {
				//rawImage1.texture = backup;
				Screen.GetComponent<MeshRenderer>().materials[0].mainTexture = backup;

				}
```

- camera.targetTexture.width值是不是固定的？？是跟unity里的camera有关还是跟pc的显示屏尺寸有关？？

- why 在两个不同平台 bytes都是85592 camera.targetTexture.width都是256 ？？？


- why 2018中没法使用并行循环？？添加 using System.Threading.Tasks;会报错？？？



1. 接收不到是因为，rawpointdata里的引用找不到，导致后面卡死，start update均不能执行 ，且时间也没法加进去
	- 解决方法
		- 不适用拖动的方式，使用gameobject.find  
		- 将在start阶段建立引用移到await阶段

2. 发现：如果引用游戏对象(脚本方式or拖动方式）就会导致及不报错也不console中打印，monobehavior函数也会卡死(如：start,update)



3. 对于Texture2D的


4. 为什么能这么不稳定？？
一会拖动引用正常
一会又是脚本引用方式正常





5. 为什么只改参观这段的UnityVideoCapture中的DeliverImage中的UpdateFrame为UpdateFrame(VideoType.kARGB, sendData, (uint)sendData.Length, 788, 585, 0, false);此时会：讲解者端只能接收到id = -1即本地的。id = 1的接收不到 ，而且id = -1的本地的frame.Buffer = null



6. why 参观者端MediaConfig使用I420p不改，讲解者端MediaConfig改为ABGR32，IdealWidth IdealHeight也跟着改，此时会出现：参观者端只有id=1的数据、参观这段的frame.Format为I420p，但是接受度的数据frame.Buffer为null. 讲解者端：id = 1的 id =-1的都有，id = 1的frame的Format = ABGR  Buffer.Length = 参观者端发的长度  id = -1的frame的Format =ABGR Buffer.Length = 2764800,why?????


7. why当双方建立连接后，断开一方，再连接，此时接受的对端的数据id = 2而不是 id = 1; why？？？


8. 如果CallApp中MediaConfig.Format设的什么，那么DeliverImage中的UpdateFrame()中的VideoType.kABGR也必须设为什么，即使是一个是ARGB 一个设为AbGR也会导致讲解者端收不到远端数据，只有id= -1的

9. DeliverImage中的UpdateFrame中的长度和width  heingh一旦不匹配，根本就不会发送出去，接收端一直收不到数据


10. 为什么使用kARGB时，如果使用```temp = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);```收发的数据就是正确的，但是如果使用temp = new Texture2D(Screen.width, Screen.height, TextureFormat.ARGB32, false);就会出现：长度正确，但是第四个Byte错误

11. why往CallApp中的UpdateFrame中写Debug.Log()会影响双端握手



12. 如何将一张image占满屏幕

13. why 这两个能形成差不多的结果？？？感觉第一个明显逻辑有点问题，但还是可行
```c#
	void Start()
    {
        temp = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
        texture = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
    }
    
    public Texture2D CaptureScreen()
    {
        
        StartCoroutine(CaptureScreenshot(texture));    

        return texture;
    }

    IEnumerator CaptureScreenshot(Texture2D texture)
    {
        //只在每一帧渲染完成后才读取屏幕信息
        yield return new WaitForEndOfFrame();

        //读取屏幕像素信息并存储为纹理数据
        texture.ReadPixels(new UnityEngine.Rect(0, 0, Screen.width, Screen.height), 0, 0);
        texture.Apply();// 这一句必须有，像素信息并没有保存在2D纹理贴图中

        //bytes其实每次读的数据，是上一次通过指令 temp = CaptureScreen();return texture;将textur读进了temp ,后又错位读进了bytes
        bytes = temp.GetRawTextureData();
      
    }

    void Update()
    {
       
        temp = CaptureScreen();           

    }
	
```

```c#
	
	void Start()
    {
        temp = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
        texture = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
    }
	
	public void CaptureScreen()
    {
        
        StartCoroutine(CaptureScreenshot(texture));
        
    }

    IEnumerator CaptureScreenshot(Texture2D texture)
    {
        //只在每一帧渲染完成后才读取屏幕信息
        yield return new WaitForEndOfFrame();

        //读取屏幕像素信息并存储为纹理数据
        texture.ReadPixels(new UnityEngine.Rect(0, 0, Screen.width, Screen.height), 0, 0);
        texture.Apply();// 这一句必须有，像素信息并没有保存在2D纹理贴图中

        bytes = texture.GetRawTextureData();
      
    }
    
    void Update()
    {                  
        CaptureScreen();
    }
```



### C#收获
#### 索引器的使用
- 不仅能用int index来索引，还能用string name来进行索引，如：Unity的Animation组件就使用了这个
	- ![索引器的使用]()


- update()中执行回调函数时，之所以使用 yield return是不是由于默认函数回调是同步的，如果函数内使用了while(){}可能会卡死？？？？？


#### 多线程的使用
- 我对C#对线程的使用可以说只会一种最简单的模式，很多精妙的组合都不知道，具体原理也不知道
- 我连 Thread  ThreadStart有什么区别我都不清楚


#### IO-文件读写 全收录


#### 各种类型转换的 全收录



#### string的等段裁剪
```c#
		private static string[] SplitLongMsgs(string s)
        {
            const int maxLength = 2048;
            int count = s.Length / maxLength + 1;
            string[] messages = new string[count];
            for (int i = 0; i < count; i++)
            {
                int start = i * maxLength;
                int length = s.Length - start;
                if (length > maxLength)
                    length = maxLength;
                messages[i] = "[" + (i + 1) + "/" + count + "]" + s.Substring(start, length);

            }
            return messages;
        }
```


#### is运算符的使用
```c#
 protected virtual void Call_CallEvent(object sender, CallEventArgs e)
 {
     switch (e.Type)
     {
         case CallEventType.FrameUpdate:
             {
                 if (e is FrameUpdateEventArgs)
                 {
                     UpdateFrame((FrameUpdateEventArgs)e);
                 }
                 break;
             }
     }
        
 }
```

- 主要是用在，拿一个子类的实例传给父类的引用变量，然后再由这个引用变量来使用is 才有意义，即是对继承链上实际对象is哪一级的做的一个判断。如果父类变量引用(指向)的本就是父类的实例，那他肯定不is子类的类型。即，is一般用于基类做继承链上子类实例的入口时来进行恢复


#### ```list<T>``` 转 T[]
```c#
    List<string> devices = new List<string>();
    string[] videoDevices = UnityCallFactory.Instance.GetVideoDevices();
    devices.Add("Any");
    devices.AddRange(videoDevices);
    return devices.ToArray();
```




#### 通过static只读属性来类内实例化
- UnityCallFactory那样类内创建一个Instance static只读属性，那样UnityCallFactory使用时不用实例化了，直接UnityCallFactory.Instace来使用



#### 协程的使用
- 使用协程实现停等待
```
 private IEnumerator ConfigureDelayed(float startInSec)
        {
            yield return new WaitForSeconds(startInSec);
            Configure();
        }
```



#### ```List<T>```使用
1. 获取第一个元素
2. 获取最后一元素
	- timeSpan[-1]不能用？？不能像pyhton那样
	- timeSpan[timeSpan.Count -1]
3. 头插
4. 尾插
5. 插入一段连续的(可以往List中插入通过类型的一个数组)
	- 





### unity收获
1. why 在update()里面调用while()会卡死？？明明写的就没问题啊
	- 为什么使用 update + if 来代替 while就可以？？？？

2. 


#### Application类学习

#### Texture类

#### Texture2D类
##### 读取屏幕截图，并发送出去
1. Texture2D只需要在new 的时候 width height format设置的收发端一致，一旦Texture2D读成apply之后，就可以随意不考虑size的使用这个texture了，如：将这个texture赋给大小不一的游戏对象 or UI等游戏对象上的Texture上

2. 使用ReadPixels  GetRawTextureByte LoadRawTextueByte版
- because-why-not源码中用的就是这种，速度也挺快的：1920 1080 RGB32的也就几毫秒级
- 
###### 完整代码
- 发送端的
```c#
	private Texture2D temp;
    public Texture2D texture;
    public byte[] bytes;

	void Start()
	{
        temp = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
        texture = new Texture2D(Screen.width, Screen.height, TextureFormat.RGBA32, false);
    }

	public void CaptureScreen()
    {
        StartCoroutine(CaptureScreenshot(texture));
    }

    IEnumerator CaptureScreenshot(Texture2D texture)
    {
        //只在每一帧渲染完成后才读取屏幕信息
        yield return new WaitForEndOfFrame();

        //读取屏幕像素信息并存储为纹理数据
        texture.ReadPixels(new UnityEngine.Rect(0, 0, Screen.width, Screen.height), 0, 0);
        texture.Apply();// 这一句必须有，像素信息并没有保存在2D纹理贴图中

        bytes = texture.GetRawTextureData();   
    }

    void Update()
    {       
    	CaptureScreen();        
    }

```

- 接收端
```
public RawImage image1;

private Texture2D backup;

void Start()
{


}

    private void UpdateTexture(ref Texture2D tex, IFrame frame)
    {
        //texture exists but has the wrong height /width? -> destroy it and set the value to null
        if (tex != null && (tex.width != frame.Width || tex.height != frame.Height))
        {
            Texture2D.Destroy(tex);
            tex = null;
        }
        //no texture? create a new one first
        if (tex == null)
        {
            tex = new Texture2D(frame.Width, frame.Height, TextureFormat.RGBA32, false);
            tex.wrapMode = TextureWrapMode.Clamp;
        }
        ///copy image data into the texture and apply
        tex.LoadRawTextureData(frame.Buffer);
        tex.Apply();
    }
    
    
    

```




3. 使用RenderTexture版
- 有许多bug:
- because-why-not最新的InputVideo使用的是这种



#### RenderTxture

#### WebCamTexture类







#### 索引器怎么用
![]()


#### 通过一个Object类型对象 实现锁
- 这是什么原理？？

```c#
    private static object sLock = new object();

    lock(sLock){

    }
```

- 对数据结构进行读写保护：同一时刻只允许一个进行操作
```c#
    public static List<UnityVideoCapturer> mActiveCapturers = new List<UnityVideoCapturer>();

    var v = new UnityVideoCapturer(device.name);
    if (v != null)
    {
        lock (mActiveCapturers)
        {
            mActiveCapturers.Add(v);
        }
        return v;
    }

```



#### Object类的几个用法
```
(T)FindObjectOfType(typeof(T));
```

```
singleton.name = typeof(T).Name;
```



#### 运行时动态加载Prefabs到Scene中，并设置他的父对象位置
- 不同的prefabs的加载均一样吗？？不管什么类型都是使用预制件名字(string)加载？？
	- cs脚本预制件
	- FBX预制件
	- CallApp预制件



#### 如何将图片组件(RawImage)铺满整个屏幕

- pivot
	- 1. 此组件旋转的中心点
	- 2. 此组件的子组件的Position的参考原点，即：设置子组件的position的值就是相对于父组件的canvas的pivot为原点来将子组件的pivot移动到position指示位置处。
		- ru:父组件为canvas，pivot设为0.5 0.5 ，将子组件的pivot设为0,0 ，子组件的width height设为和canvas一样，那么将子组件的position.x = - canvas.Width/2 positon.y = -canvas.Height/2，此时子组件的pivot会移动到canvas平面的左下角，并且子组件整体都会随pivot一起进行移动，pivot只是一个移动式的特殊点，便于分析和计算，实际子组件上每个点都会同时进行移动



- canvas的width height这个值为什么可以变？？canvas不是始终会投放到整个屏幕display的吗，那这个值有什么用，，，如果canvs随意设置了一个width height，其上的一张图片(rawImage)设为和canvas一样大，那么如果canvas的Screen Match Mode使用match with width，那么canvas铺满屏幕时，图片也会跟着铺满屏幕吗？？？？如何设置canvas上的组件的大小一直等于RawImage的大小，即使canvas扩展铺满屏幕，RawImage也跟着变？？==对于绝对尺度无法保证的时候，此时就要使用相对跟随来==，此时就轮到Anchor登场了



- 通过我的实验发现：此对象的pivot更改只针对于此对象，不管此对象的pivot改成什么值，其上的子对象都会以它(父对象)的中心为position的参考原点.
	- ![]()



- Anchor
	- 四个三角形代表四个值，默认是0.5，此时位于父对象的Pivot处(canvas的pivot固定为0.5，0.5不能更改)







### 其他
1. 同样都是VGA输出口，why一个连上显示屏有信号，一个没有信号？？？说是一个是集成VGA显卡接口和独立的VGA，这两个区别是什么？？？
	- 原因解释：外壳上是有两个VGA接口，但是一个是给主板上的集成显卡的VGA输出，一个是预留给独显的VGA输出
		- 只要电脑主板没问题，一般集显都是能正常工作的 -> 此时VGA上能有信号输出
		- 但是，如果电脑主板上没有外接独显的化，此时这个VGA接口肯定没有输出啊
	- 集成显卡一般有IntelGMA900、GMA950、GMA3000，nV的GeForce 6100、GeForce 6150、GeForce 7050等，AMD-ATi的X1250，ATi的X1150等等
	- 上面的解释错了：
	- 我把vga接口插在了独显上有输出，连到集显输出vga接口上反而没有输出，咋回事？？？？是因为如果插上独显，集成显卡就不再工作？？？
		- 是的。插上独显后，主板会自动屏蔽集成显卡，集成显卡也就不能用了。但是笔记本上好像不适用，因为我通过计算机管理 -> 显示适配器 能看到有两个显卡，但是经过我的逐个屏蔽发现，默认情况下会启用的是集成显卡，独立显卡只有在禁用了集显后才会启用，why？？？？有智能检测控制？？？一般情况为了省电使用的是集显，玩游戏等吃性能的程序运行时才会使用独显？？？

- 为什么台式机上插上独显后，使用计算机管理 -> 显示适配器 只能看到有一个显卡？？


2. 我看主机上有两对 （VGA + DVI输出），是不是说明每个显卡，无论是集显or独显都会有两个输出接口？？？



3. 通过什么方式能查看电脑的所有的可用输出接口信息？？？


4. 使用开源框架or付费框架时，对于自己想要的需求，不要直接看源码去笨找，要先去看changelog 和 FAQ 或 issues，自己遇到的问题一般别人也容易遇到，站在别人的肩膀上来加速开发


