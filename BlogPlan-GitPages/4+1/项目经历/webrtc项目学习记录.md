[toc]

### 属性可以关联的成员
- 委托类型的委托变量
	- 类中通过自动属性 关联 委托类型的委托对象成员，可通过(=>表达式主体定义 )来对属性进行set
```
public delegate void DelegateOnAddTrack(MediaStreamTrackEvent e);

//通过自动实现属性的方式，关联到它默认隐式产生的一个 private委托类型的委托变量成员
//相当于 private DelegateOnAddTrack _OnAddTrack;
public DelegateOnAddTrack OnAddTrack { get; set; }

//然后给这个属性set一个匿名方法，实际上来实现安全的给private型的委托变量加入一个匿名方法
receiveVideoStream1.OnAddTrack = e =>
        {
            if (e.Track is VideoStreamTrack track)
            {
                receiveImage1.texture = track.InitializeReceiver(1280, 720);
            }
        };
```

- 引用类型的引用变量
	- 这样有什么用？

```
        public IReadOnlyList<MediaLine> MediaLines => _mediaLines;
        private readonly List<MediaLine> _mediaLines = new List<MediaLine>();
```

- class类型的实例对象

```
public Transceiver Transceiver { get; private set; }
//将属性赋给只读属性
public LocalMediaTrack LocalTrack => Transceiver?.LocalTrack;
```

### 自动实现的只读属性is不是还有更快捷的方式？
- 最原始是2段式：
	- 1. 先声明字段
	- 2. 声明属性
	- 3. 属性关联private字段
```

```

- 然后为了方便->自动实现方式
	- 只声明属性，字段会自动创建
```
public MediaKind MediaKind { get; }

public override MediaKind MediaKind => MediaKind.Video;
```

- 对于只读字段的 -> 表达式主体定义实现版本

```
private readonly List<MediaLine> _mediaLines = new List<MediaLine>();
//不用使用set,get访问器，直接使用  普通字段声明 + => -> 进化为表达式主体定义实现只读属性 
public IReadOnlyList<MediaLine> MediaLines => _mediaLines;



```



### 抽象类竟然也有构造函数，而且构造函数不用加abstrc
- 抽象类不用实例化，构造函数用来做什么？？

### Regex类


### Unity的MonoBehavior方法
https://docs.unity3d.com/cn/2019.4/Manual/ExecutionOrder.html

- void Awake()
	- 如果游戏对象是激活状态&&程序在运行期间，则将C#脚本(拖动or )附加到游戏对象上的时候立马调用，
	- 如果游戏对象处于非活动状态，则在激活之后才会调用 Awake
	- 程序未开始运行
		- 怎样都不会调用Awake
	- 程序开始运行
		- 对象处于激活状态
			- C#脚本已经附加游戏对象上
				- 直接调用Awake ->优先于 OnEnable ->优先于 Start
			- C#脚本未附加游戏对象上
				- 在将脚本附加到游戏对象上的瞬间 调用Awake
					- 拖动方式附加
					- 脚本方式怎么附加？？？
		- 对象处于未激活状态
			- 在激活之后才会调用对象上脚本组件的 Awake
		- 对象激不激活对awake有影响，但是脚本组件本身激不激活都会执行其上的awake
- void OnEnable()
	- 在非激活(如调用了OnDesable) -> 激活时，调用
		- 注意：对象非激活or激活 -> 其上的C#脚本组件亦非激活or激活
			- 船毁了，船上的一切亦全毁了
	- 对象一直处于激活状态时，一旦启动Appilication会立马调用优先于Start()
- void OnDisable()
	- 退出时(场景退出？ 应用退出？？)，会在__所有对象上__调用此函数(如果存在的话)
	- 1.处于非活动状态&&2.运行时 调用此函数，两条件缺一不可
		- 怎样算非活动状态？？
			- inspector中去掉此脚本的勾
			- 脚本中怎么操作能使使非活动？？
- void Start()
	- 程序为开始运行
	- 程序开始运行
		- 仅当启用脚本实例后(脚本处于激活状态)，才会在第一次帧更新之前调用 Start
- void Update()
- void OnDestroy()
	- 当对象由存在->不存在时，对象存在的最后一帧完成所有帧更新之后，调用此函数
		- 对象存在 -> 不存在的可能原因：
			- 运行期间删除对象，如：运行期间删除脚本 会 触发脚本上的OnDestroy()方法
			- 可能应 Object.Destroy 要求或在场景关闭时销毁该对象 -> 触发对象上所有脚本组件的OnDestroy()
- void OnApplicationQuit()
	- 在退出应用程序之前在__所有游戏对象上__调用此函数。
	- 在编辑器中，用户停止播放模式时，调用函数。



### unity中特殊的类
#### unityEvent
https://docs.unity3d.com/ScriptReference/Events.UnityEvent.html

- ![用法]()

#### PlayerPrefs类


#### JsonUtility
- ```JsonUtility.ToJson(T msg)```
- ```JsonUtility.FromJson<T>()```


#### 协程 && yield return
- why 协程要配合 yield 来使用
	- 使用yield语句可以暂停(pause)协同程序的执行，yield的返回值指定在什么时候继续(resume)协同程序。
	- 有时候协程是这样的任务，先执行一部分( ru:发送请求) -> 等待返回结果部分完成 -> 在进行下一步分(ru：对返回的结果进行分析)
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\协程的用法.PNG" alt="请求式协程" style="zoom:60%;" />
	- 多级链式控制型
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\协程的用法2.PNG" alt="协程的用法2" style="zoom:100%;" />
- yield的几种经典语句搭配
		- yield return null; 
			- 暂停协同程序，下一帧再继续往下执行
		- yield new WaitForFixedUpdate ();
			- 暂停协同程序，等到下一次调用FixedUpdate方法时再继续往下执行
		- yield return new WaitForSeconds(2);
			- 暂停协同程序，2秒之后再继续往下执行
		- yield return StartCoroutine("SomeCortoutineMethod");
			- 暂停此协同程序，开启SomeCortoutineMethod协同程序，直到SomeCortoutineMethod执行完再继续往下执行




### C#中特殊的结构体
#### CancellationToken


### C#中特殊的类
#### Task  Task<> 相关的

#### TaskCompletionSource<TResult> 类

TaskCompletionSource<T>  专门用于生成 Task<T>类型的任务

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\TaskCompletionSource.PNG" alt="用法组合1" style="zoom:50%;" />


<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\TaskCompletionSource2.PNG" alt="用法组合2" style="zoom:60%;" />



#### CancellationToken结构体



#### GUID
- 是什么
	- GUID（全局统一标识符）是指在一台机器上生成的数字，它保证对在同一时空中的所有机器都是唯一的。
	- 生成算法很有意思，用到了以太网卡地址、纳秒级时间、芯片ID码和许多可能的数字
	- GUID的唯一缺陷在于生成的结果串会比较大。” 
	- 通常平台会提供生成GUID的API。
		- 在 Windows 平台上，GUID 应用非常广泛：注册表、类及接口标识、数据库、甚至自动生成的机器名、目录名等。
		- 一个GUID为一个128位的整数(16字节)，在使用唯一标识符的情况下，你可以在所有计算机和网络之间使用这一整数。
		- GUID 的格式为“xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx”，其中每个 x 是 0-9 或 a-f 范围内的一个十六进制的数字。例如：337c7f2b-7a34-4f50-9141-bab9e6478cc8 即为有效的 GUID 值。
		- 世界上（Koffer注：应该是地球上）的任何两台计算机都不会生成重复的 GUID 值。GUID 主要用于在拥有多个节点、多台计算机的网络或系统中，分配必须具有唯一性的标识符。
- why need it
	- 我们有些时候需要全局唯一的标识符来(作为各种name(文件名、线程名、)、)等，guid就是解决这个需求的。
		- GUID（全局统一标识符）是在一台机器上生成的数字，它保证对在同一时空中的所有机器都是唯一的。
		- 世界上（Koffer注：应该是地球上）的任何两台计算机都不会生成重复的 GUID 值。GUID 主要用于在拥有多个节点、多台计算机的网络或系统中，分配必须具有唯一性的标识符。

- how use it
	- .NET中使用GUID
		- Guid.NewGUID() 生成一个新的 GUID 唯一值
		- Guid.ToString()将 GUID 值转换成字符串，便于处理
		- 构造函数 Guid(string) 由 string 生成 Guid 结构，其中string 可以为大写，也可以为小写，可以包含两端的定界符“{}”或“()”，甚至可以省略中间的“-”，Guid 结构的构造函数有很多，其它构造用法并不常用。
		- 应用场景：
			- name存在用存在的，name不存在使用guid生成一个
			- ![mrtk-webrtc中使用Guid作为name](C:\Users\king-kong\Desktop\要做的事情\picture\C#\guid用法1.PNG)



#### Utils类

#### IntPtr结构体
- 是什么
	- Object -> ValueType -> IntPtr
- why need IntPtr

- how 使用 IntPtr

#### Marshal类
- 是什么
	- 是一个静态类，模拟的是一个方法集合，这些方法用于：
		- 分配非托管内存
		- 复制非托管内存块
		- 将托管类型转换为非托管类型
		- 此外还提供了在与非托管代码交互时使用的其他杂项方法
	- Marshal就是把一个结构（类）序列化成一段内存，然后送到另一个进程
- why need it
	- 在两个不同的实体(两个线程或者进程甚至机器、在Managed和Unmanaged之间）进行方法调用和参数传递的时候，具体的调用方法和参数的内存格式可能需要一定的转换，这个转换的过程叫做Marshal
		- 





#### ManualResetEventSlim


#### GCHandle

####  StringBuilder类



#### SystemInfo类

- 是什么
	- 存储 CPU 信息、电池寿命、内存量和操作系统版本等设备信息
	https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/bb397572(v=vs.90)

- 常用搭配
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\SystemInfo类的使用.PNG" alt="常用搭配" style="zoom:50%;" />



#### System.Text.Encoding类



#### Buffer静态类


### C#中特殊的接口
#### IDisposable


#### IEnumerable



- why 要使用接口类型的属性？？
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\接口的使用方式1.PNG" alt="接口类型的属性" style="zoom:70%;" />




#### 

### else

- c#允许类内初始化


- static成员
	- 怎么声明
	- 怎么初始化
	- 怎么使用
	- C#和C++的上述3点的处理不同
- C#类内不对static成员进行初始化 -> 此时static成员 == 全局成员 -> 内存中会分配具体的存储区域，此时这个区域中存的值是什么？？是怎么进行存的？？（通过static成员的默认初始化？？）
	- C#都有哪些成员有默认初始化？？
		- 按static const 普通 等关键词来分
			- 普通的有默认初始化？
			- const成员有默认初始化？
			- static
		- 按 字段成员() , 方法成员(属性、索引器、事件、方法)来分
- C#中string类的 Empty成员没有进行初始化(没有类内初始化、也没有构造函数内初始化)，但是却将String.Empty用给别的类中的成员的初始化
```
public string Name { get; } = string.Empty;
```


- as运算符



- 事件成员也可以通过赋值null来清空
```
        private event I420AVideoFrameDelegate _videoFrameReady;
        private event Argb32VideoFrameDelegate _argb32VideoFrameReady;

		//code here
		
        _videoFrameReady = null;
        _argb32VideoFrameReady = null;
```

- Utils.MemCpyStride和System.Buffer.MemoryCopy()的区别
	- // Note : System.Buffer.MemoryCopy() essentially does the same (without stride), but gets transpiled by IL2CPP into the C++ corresponding to the IL instead of a single memcpy() call. This results in a large overhead, especially in Debug config where one can lose 5-10 FPS just because of this.




- C#中对于接口中成员的实现&&覆盖的方式
	- C#接口中可以有的成员：
		- 属性
		- 方法
	- 对接口中的实现，接口中不需要进行virtual，直接只写声明式即可
	- 对接口中的同名属性的覆盖
		- ![类中重写的](C:\Users\king-kong\Desktop\要做的事情\picture\C#\接口重写2.PNG)
		- ![接口中的](C:\Users\king-kong\Desktop\要做的事情\picture\C#\接口重写.PNG)


- default运算符
	- default(int)
	- default(T)
- default文本推断
- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\default运算符.PNG" alt="default的两种方式使用" style="zoom:50%;" />

#### 事件
- 事件event是一种成员不是类型，故不能分值类型or引用类型，但是事件变量存储的是引用or实际值？？
	- 事件本质上也是一个功能单元，也要有一种组织方式吧，他是像一个对象那样来使用？？还是有专门的使用方式？？？

- 事件成员本质上是一个委托对象？？public event看做是一个特殊的标识符？？
	- 因为我在vs中通过鼠标悬停发现，事件成员的类型是委托类型
	- 还可以声明为可空类型  Associated?.Invoke(this);


- 是什么
- why need it
- how use it
	- 发布(符合.NET准则的)事件共别人订阅
	- 订阅和取消订阅事件
	- 如何触发事件
		- 在事件成员所在类触发事件
			- 有几种事件触发的方式？？有什么区别吗？？
			- 事件成员名(参数)；？？？？
			- 事件成员名?.Invoke(参数)；？？？
			- 事件成员名?.BeginInvoke(参数)；？？？
		- 在事件成员所在类的派生类触发事件
			- 难点：
				- 不能：
				- 事件是特殊类型的委托，只能从声明它们的类中进行调用。
					- 派生类不能直接调用在基类中声明的事件。
					- 即使，派生类集成了事件成员，但它(派生类)没有资格触发这个事件(有资格往这个事件加入方法没？？)，即，不能直接  ```事件成员名?.Invoke()```来调用，必须使用 在派生类中通过base来调用基类的方法的方式
						- 1. 将```事件成员名?.Invoke()```封装在一个基类的virtual方法A里
						- 2. 在派生类中override这个方法A，在这个方法内部通过base.funA()来调用基类的方法
						- ![]()
				- 又需要：
				- 虽然有时可能需要只能由基类引发的事件，不过在大多数情况下，应使派生类可以调用基类事件。







- yeild return 




- Debug.Assert()
	- 检查条件 ；如果条件为 false，则输出消息，并显示一个消息框，其中显示调用堆栈。这个断言如果不成功是会弹窗的：
	- 默认情况下, Debug.Assert该方法仅适用于调试版本。 如果要在发布版本中进行断言, 请使用方法。Trace.Assert 有关详细信息，请参阅托管代码中的断言。


- Action 是 无输入-无输出的 特殊委托类型，常用于event
![]()
![]()



- add , remove关键字


- ?.   ?[]



- 通过复合关系实现对象间的相互能找到对方的双向关系


- VideoTrackAdded?.Invoke(track);
	- 在这个有啥用？？明明根本没有往事件里面添加方法，，，这一句有啥用？？？
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\事件机制1.PNG" style="zoom:50%;" />
	- 
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\事件机制2.PNG" style="zoom:50%;" />



#### interop概念

- 是什么
	- 让受管代码对象和非受管对象协同工作的过程称为互用性(interoperability)，通常简称为 interop。
- why need it
	- 有时需要在C#环境中使用C#不含有的功能，只能通过与外部互操作的方式来实现
		- 如：webrtc功能，要基于google开源的C++的底层功能




- 通过 returnType functionName(params object[] args){ };来实现任意类型，任意个数的输入参数列表？？？？
	- 通过returnType functionName(params string[] args){ };联想来的



UnityEngine.Debug.Assert(


#### C#关键字
##### await - async - 异步编程






- Unity和C#是大小写敏感的
	- Debug.Log（） OnEnable()等 大小写不对会报错




- unity中的预制件的自定义inspector是怎么弄出来的？？
	- 正常的脚本在cs文件中修改后会在脚本组件的inspector界面中体现出来，但是webcamsource这种为什么就算修改了cs脚本inspector界面中的仍然不会修改？？？？
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\unity\脚本无法修改inspector.PNG" alt="脚本无法修改inspector" style="zoom:50%;" />






- 在C#中同名-同输入方法即使使用了override，仍能使用base来访问基类中的同名方法，
	- 因为基类中的同名方法是只作用于继承来的基类区的成员，故可以通过子类-父类同名方法的混合嵌套使用，来设置良好的方法结构
		- ![子类-父类同名方法的混合嵌套使用](C:\Users\king-kong\Desktop\要做的事情\picture\C#\继承中子父同名方法的嵌套使用.PNG)



#### frame debugger

#### 




#### unity数组对象的new初始化在start中才算数，why在start外进行初始化长度，在使用时还是会报错


- 还是会忘记，ref需要在声明处和定义处均显示表示出来



- System.Diagnostics.Debug.Assert(rgbdByte.Length > 0);  

- 

### 不错的编写风格
- 善用 ? :
![2级三目的写法](C:\Users\king-kong\Desktop\要做的事情\picture\C#编程风格1.PNG)

- 工程的组织
	- 工程 == 几个namesapce
	- namespace 分为 中每个class写成几个cs文件，关联性强的几个类可以写成一个文件中
	- ![]()


- 类内声明类型
	- 是什么
	- why need 在类内声明类型？？
		- 所有类内声明的类型都可以通过类外声明来代替，那为什么还要声明类内的类型？有什么好处？

- 类|接口|结构中的属性的书写风格
	- 只读属性
		- 声明处初始化
		- 声明处使用=>来从指定从哪都读
	- 普通属性


- unsafe{}
- fixed{}
- using(){}
- lock(){}
	- C#中实现资源锁的一种方式
	- 1. 随便创建一个readonly object的类型
	- 2. 通过lock 1. 中创建的object来实现资源锁
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#中资源锁的实现1.PNG" alt="资源锁的实现" style="zoom:80%;" />



- Utils.ToWrapper<Transceiver> 是什么



#### 使用readonly限制类内的容器成员
- C#通过使用readonly 来实现 定向指针的功能(like :  int *  const p = new int(3));，即指针只能指向一个地址，但是指向的地址出的内容却可以变，这样的好处是什么？？为什么C# webrtc源码中一直这样使用？？
	- ![readonly用法1](C:\Users\king-kong\Desktop\BlogPlan\picture\C#\readonly的用法.PNG)
	- ![readonly用法2](C:\Users\king-kong\Desktop\BlogPlan\picture\C#\readonly的用法1.PNG)


#### 对封装的理解更深了
- 使用继承进行组间的功能的分层和完善
- 使用复合来将组件像装wifi模组的方式来使用功能
- 封装 = 复合组件 + 额外的新功能



#### 基于task作为返回函数类型的函数多级调用模式
![]()

![]()

![]()



#### 继承中的构造函数的写法
- 使用base构建基类区的
- 新增区使用新增去来
- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\构造函数的写法.PNG" alt="使用base写构造" style="zoom:50%;" />


#### C#中使用代码选择编译(预编译指令) 代替 if()做代码选择
- 使用预编译的```#if # endif ```代替 ```flag变量 + if()```的的好处：
	- 只需要更改一个#define就可以选择编译哪些部分的代码
		- 如：选择编译particleSystem部分的 or gpu部分的 or Test部分的
	- 而，if()则是全编译，在运行阶段选择执行
	- 功能上差不多，但是有细微的差异：
		- #define + #if 从逻辑上更是为真的代码选择编译 
		- #define + #if比if()多了颜色上的标识
			- 非选择编译代码会以黑色的来突出表示


- 这种编写风格由于会破坏代码结构的简洁简单，故：一般只在以下一些种情况下使用：
	- 非用不可时：
		- 如：一个文件要求具备跨平台性。如：unity下的一份源码要求：在unity Editor方式运行时 按莫一部分代码逻辑来编译，WSA平台时，按另一种代码逻辑来编译，Android平台时再按另一种逻辑来编译，但是实际使用时只能是一个文件
	- 只有少量修改时：


- 注意：
	- 不要将三份差不多的相似的代码糅合成一份，这样会使结构变得混乱
		- ![结构混乱三倍]()


#### 有相互引用依赖的获取引用方式
- 好的：
	- ![好的](C:\Users\king-kong\Desktop\要做的事情\picture\C#\好的编程书写方式.PNG)

- 错的：
	- ![错的](C:\Users\king-kong\Desktop\要做的事情\picture\C#\好的编程书写方式1.PNG)


### 编程阶段

1. 可编程深度相机 不属于 webcam？？？？
- why 使用两种不同的深度相机均无法正常在webcamsource中进行配置？？
	- azure kinect：使用webcamsource作为源，直接程序异常退出，错误都不打印
		- 即使，只是将azure kinect连上电脑，不打印，不显示，只要使用了webcam都会异常退出，why？？？？
	- Intel(R) RealSense(TM) Depth Camera 435i Depth.至少插上能检测出来，但是仍无法使用，也无法检测出formats等信息
	- ![]()


### 泛型类
#### 泛型类可继承非泛型类
#### 非泛型类可继承泛型类
- 非泛型类（即，具体类）可继承自封闭式构造基类，
```
//No error
class Node1 : BaseNodeGeneric<int> { }
```
- 但不可继承自开放式构造类或类型参数，因为运行时客户端代码无法提供实例化基类所需的类型参数。
```
//Generates an error
//class Node2 : BaseNodeGeneric<T> {}

//Generates an error
//class Node3 : T {}
```

#### 类型约束
- 是什么
- why need 类型约束
```

```

- how use 类型参数约束
	- 同一参数可以有多个约束![同一参数可以有多个约束](C:\Users\king-kong\Desktop\要做的事情\picture\C#\类型参数约束.PNG)
	- 可以对多个类型添加约束
	- 可以在类内对类型参数做一些判断![类型参数约束_类型判断](C:\Users\king-kong\Desktop\要做的事情\picture\C#\类型参数约束_类型判断.PNG)


#### 泛型类的构造函数怎么写
- 泛型类构造函数的写法
- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\泛型类的构造函数怎么写.PNG" alt="泛型类构造函数的写法" style="zoom:70%;" />
- 泛型类构造函数的使用
- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\泛型类构造函数的使用.PNG" alt="泛型类构造函数的使用" style="zoom:50%;" />