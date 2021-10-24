[toc]

# scripts系统
- why unity need 脚本系统？
	- 1. 使游戏开发更加灵活
		- 比如游戏对象运行期间动态传值
	- 2. 
## Setting Up Your Scripting Environment
### 1. 为自己选择一款编辑-调试C#代码所用的IDE
- 可以使用unity自带的，也可以自己根据喜好diy，自己diy需要进行一些设置
#### unity默认的
#### 自定义
### 2. 在 Editor 中调试C#脚本
- You can debug C# code that is running in the Unity Editor while the Unity Editor is in Play Mode.
- To debug in the Editor, you need to set the Editor’s Code Optimization mode to Debug Mode, then you can attach a code editor with a debugging feature.
- To change the __Code Optimization mode__, select the Debug Button in the bottom right of the Unity Editor Status Bar.
	- 1. 手动随时切换：在unity的右下角的小虫子
	- 2. 设置开机进入时的默认mode：Edit > Preferences > General > Code Optimization On Startup.

#### debug和release两种模式的区别
- 1. why 他们被称为Code Optimization mode？
	- 因为它们只是两种不同的编译选项的组合，都是对编译进行了一些优化和方便调试上的权衡
#### debug方式
- 加断点
- 单步执行
- 变量检查

### 3. Unity Test（自动测试）
- As your project grows, and the number of scripts, classes and methods in your project increases, it can become difficult to ensure that a change in one part of your code doesn’t break things somewhere else.
- __Automated testing__ helps you check that all parts of your code are functioning as expected.
	- It saves time by identifying where and when problems occur as soon as they are introduced during development, rather than relying on manual testing, or even worse - bug reports from your end users.
- The__ Unity Test Framework package__ (formerly the “Unity Test Runner”) is a tool that allows you to test your code in both Edit mode and Play mode, and also on target platforms such as Standalone, Android, or iOS.
	- [com.unity.test-framework page](https://docs.unity3d.com/Packages/com.unity.test-framework@1.1/manual/index.html)

### 4. Roslyn analyzers and ruleset files

## Scripting concepts
- Unity 对脚本使用标准 Mono 运行时的实现方案
- 但在从脚本访问引擎方面，仍然有自己的惯例和技术
- 本部分讲述2方面：
	- 介绍如何通过脚本控制 Unity Editor 中创建的对象
	- 详细说明 Unity 的游戏功能与 Mono 运行时之间的关系。

### 1. use__脚本组件__控制 Unity Editor 中创建的对象
- 游戏对象的__行为__由附加的__组件__控制。
- 内置的组件很多，但还不够。
	- 内置的都是common的
	- 专用的组件要通过脚本来进行扩充
- 在创建脚本时，实际上是在自定义新的组件类型
	- 可以像任何其他组件一样将这种组件附加到游戏对象
		- 通过__拖动__来进行附加
	- 脚本只定义了组件的蓝图(== 只是声明了一个class，但并没使用class创建对象)，因此在将脚本实例附加到游戏对象之前，不会激活任何代码
	- 组件实际上是类的实例
#### 脚本组件相关
#### 1. 创建脚本组件
#### 2. 使用脚本组件
#### 3. 变量和inspector
- Unity 通过在变量名称中出现大写字母的位置引入空格来创建 Inspector 标签。但是，这纯粹是出于显示目的，在代码中应始终使用变量名称。
- inspector界面能显示的变量
	- 1. public限制的变量直接会显示
	- 2. private限制的变量
		- 必须通过添加 [Serialized]才能在inspactor显示
- Unity 实际上允许您在游戏运行时更改脚本变量的值。
	- 此功能很有用，__无需停止和重新启动__即可直接查看更改的效果。
	- 当游戏运行过程结束时，变量的值将重置为按下 Play 之前所处的任何值。
		- 这样可确保自由调整对象的设置，而不必担心会造成任何永久性损坏。

#### 4. 使用脚本组件控制GameObject
- 脚本组件存在的意义就是控制GameObject

##### 组件控制GameObject的两种方式
	- 1. 直接在inspector中修改
		- 使用组件的 Inspector 来更改组件属性 -> 控制组件 -> 控制游戏对象
	- 2. 使用脚本更灵活的修改
		- 脚本可以随着时间推移而逐渐改变属性的值，或者响应用户的输入，这是通过inspector不可能做到的
		- Inspector 中所没有的一项额外功能是以脚本方式可以在组件实例上调用函数
		- 通过在适当时间更改、创建和销毁对象，可以实现任何类型的游戏运行过程
##### 1. 脚本组件访问组件
###### 同一游戏对象上
1. 最简单和最常见的情况是脚本需要访问附加到同一游戏对象的其他组件
	- 组件实际上是类的实例，因此第一步是获取对需要使用的组件实例的引用。
	- 获得对组件实例的引用后，可以像在 Inspector 中一样设置其属性的值：
	- Inspector 中所没有的一项额外功能是可以在组件实例上调用函数：
```
void Start () 
{
    Rigidbody rb = GetComponent<Rigidbody>();
    
    // 改变对象的刚体质量。
    rb.mass = 10f;
    // 向刚体添加作用力。
    rb.AddForce(Vector3.up * 10f);
}
```
2. 可以将多个自定义脚本附加到同一对象。从一个脚本访问另一个脚本
3. 如果在脚本中声明组件类型的公共变量，则可以拖动已附加该组件的任何游戏对象。这将直接访问组件而不是游戏对象本身。

###### 不同游戏对象上

##### 2. 脚本组件访问对象
- 脚本检索子对象和无关联的对象的方式是一样的吗？检索子对象会不会有什么特别的便利
###### 运行前确定对象
- 1. 拖放引用法
	- 向脚本添加公共的游戏对象变量 + 将对象从场景或 Hierarchy 面板拖到此变量上
	- 在处理具有永久连接的单个对象时，将对象与变量链接在一起是最有用的方法。
	- 可以使用数组变量来链接同一类型的多个对象，但仍然必须在 Unity Editor 中（而不是在运行时）进行连接。
- 2. 
###### 运行时再确定对象
1. 寻找子游戏对象
	- 之所以设置成子游戏对象而不是游离对象，is因为子对象和父对象有一些关系
		- 子对象便于父对象对其管理

- 1. 可以使用父游戏对象的变换组件来检索子游戏对象（因为所有游戏对象都具有隐式变换）???
	- 1. 在父对象的脚本组件中使用Transform数组
		- public Transform[] waypoints;
	- 2. 在父对象的脚本组件中使用 Transform.Find 函数按名称查找特定子对象
		- transform.Find("Gun");
2. 按__名称或标签__来查找无亲子关联的游戏对象
	- 只要有某种信息可以识别游戏对象，就可以在场景层级视图中的__任何位置__找到该游戏对象。
- 1. 可使用 GameObject.Find 函数按名称检索各个对象：
- 2. 可以使用 GameObject.FindWithTag 按标签来查找对象
- 3. 还可以使用GameObject.FindGameObjectsWithTag 函数按标签来查找对象集合：

#### 5. 事件函数(event functions)
- Unity 中的脚本与传统的程序概念不同。
	- 在传统程序中：
		- 代码在循环中连续运行，直到完成任务
	- Unity 中：
		- Unity 通过调用在脚本中声明的某些函数(event functions)来间歇地将控制权交给脚本。函数执行完毕后，控制权将交回 Unity。
			- [详细的事件函数介绍](https://docs.unity3d.com/cn/current/ScriptReference/MonoBehaviour.html)

##### 初始化事件
- 如果能在游戏运行过程中进行任何更新之前调用初始化代码，通常会很有用
	- 脚本组件 like 类
	- 脚本组件中的初始化函数 like 类的构造函数
		- 因为unity不支持类中使用构造函数

- 1. 场景加载时会为场景中的每个对象调用 Awake 函数。
- 2. 请注意，虽然__各种对象的 Start 和 Awake 函数的调用顺序是任意的__，但在调用第一个 Start 之前，所有 Awake 都要完成。(是所有对象的awake()都要完成 or 这个对象的awake()要完成？？)
	- 这意味着 Start 函数中的代码可以利用先前在 Awake 阶段执行的其他初始化。
- 3. 在第一帧之前或开始对象的物理更新之前需要调用 Start 函数。

##### 更新事件
###### 常规更新事件(Update)
- 游戏的帧率不是恒定的(取决于一次Update要花费的时间)
	- [Time.deltaTime](https://docs.unity3d.com/cn/current/ScriptReference/Time-deltaTime.html) 
		- 完成上一帧所用的时间（以秒为单位）（只读）。
		- 此属性提供当前帧和上一帧之间的时间
		- 这个值是怎么计算的啊？？？
- 两次Update 函数调用之间的时间长度也不是恒定的
###### 物理更新时间(FixedUpdate)
- 物理引擎也采用与帧渲染类似的方式以离散时间步骤进行更新。
- 在每次物理更新之前都会调用一个称为 FixedUpdate 的单独事件函数。
- 由于物理更新和帧更新__不会以相同频率进行__，所以如果将物理代码放在 FixedUpdate 函数而不是 Update 中，此代码将产生更准确的结果。
###### (LateUpdate)
- 为场景中的所有对象调用 Update 和 FixedUpdate 函数之后以及计算所有动画之后，如果能进行其他更改，也会很有用。
	- 一个例子是摄像机应该聚焦于目标对象；必须在目标对象移动后才能调整摄像机的方向。
	- 另一个例子是脚本代码应该覆盖动画的效果（例如，让角色的头部看向场景中的目标对象）。
- 可使用 LateUpdate 函数来处理这些类型的情况。

##### 物理事件
- 物理引擎将通过调用该对象的脚本上的事件函数来报告对象的碰撞情况。

##### 事件函数的执行顺序



#### 6. 时间和帧率管理
##### 普通帧间隔
- 在处理这种基于时间的动作时要记住的一项重要规则是：
	- 游戏的帧率不是恒定的
	- Update 函数调用之间的时间长度也不是恒定的。
##### 固定时间步长
##### Maximum Allowed Timestep
##### 时间标度
##### Capture Framerate

#### 7. 创建和销毁游戏对象
##### 1. 在运行之前创建游戏对象
##### 2. 在游戏运行过程中创建和删除游戏对象
- 有些时候具有在游戏运行中创建和删除游戏对象，如：
	- 20分钟龙坑处生成大龙对象
	- 大龙被打死消失
- 通过脚本组件的方式：
	- 创建对象：
		- 使用Instantiate 函数来创建游戏对象
	- 删除对象：
		- 使用Destroy 函数
			- 该函数将在__帧更新完成后__或选择在__短时间延迟后__销毁对象：
			- Destroy 函数可以在不影响游戏对象本身的情况下销毁个别组件
				- 避免使用```Destroy(this);```
				- …这种情况下实际只会销毁调用该函数的脚本组件，而不是销毁附加脚本的游戏对象。


#### 8. 脚本组件中的特性(Attribute)
- 特性 (Attribute) 是可以放在C#脚本中的类、属性或函数上方来指示特殊行为的标记。
- why要存在特性？？
- unity共有多少种特性？？
- .NET中也有特性这个概念，特性这个concept是一个通用的concept????
##### Unity 提供了在 API 参考文档中列出的大量特性：
###### UnityEngine 特性
- 在UnityEngine下的Attributes分支下均是：
###### UnityEditor 特性
- 在UnityEditor下的Attributes分支下均是：
###### .NET 库中还定义了一些有时可能在 Unity 代码中很有用的特性。
- [请参阅 Microsoft 关于特性 (Attributes) 的文档以了解更多信息](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/)
	- 注意：不要使用 .NET 库中定义的 ThreadStatic 特性；如果将其添加到 Unity 脚本，会导致崩溃。


#### 9. 平台相关的编译
##### Scripting Define Symbols 
##### 使用Scripting Define Symbols 

#### 10. 特殊文件夹和脚本编译顺序
##### 特殊文件夹名称
- 通常可为创建的文件夹选择任何名称来组织 Unity 项目。
- Unity 保留了一些项目文件夹名称来指示内容具有特殊用途
	- Unity 会将许多文件夹名称解释为应以特殊方式处理文件夹内容的指令。
	- 例如，必须将 Editor 脚本放在名为 Editor 的文件夹中才能使这些脚本正常工作。
	[特殊文件夹名称官方文档](https://docs.unity3d.com/cn/current/Manual/SpecialFolders.html)
###### Assets
- Assets 文件夹是包含 Unity 项目使用的资源的主文件夹。
- Editor 中的 Project 窗口的内容直接对应于 Assets 文件夹的内容。
	- 具备实时同步更改功能，在一端(add,delete,)另一端也进行相应的改变
- 大多数 API 函数都假定所有内容都位于 Assets 文件夹中，因此不要求显式提及该文件夹。但是，有些函数需要将 Assets 文件夹作为路径名的一部分添加（例如，AssetDatabase 类中的一些函数）。
###### Editor
- 放在名为 Editor 的文件夹中的脚本被视为 __Editor 脚本__而不是__运行时脚本__。
	- 这些脚本在开发期间向 Editor 添加功能，并在运行时在构建中不可用。
- 可在 Assets 文件夹中的任何位置添加多个 Editor 文件夹。
	- 应将 Editor 脚本放在 Editor 文件夹内或其中的子文件夹内。
- 如果脚本位于 Editor 文件夹中，Unity 不允许将派生自 MonoBehaviour 的组件(脚本组件)分配给游戏对象。
###### Editor Default Resources
###### Gizmos
###### Plug-ins
###### Resources
###### Standard Assets
###### StreamingAssets
###### 隐藏的资源

##### 脚本编译顺序
- 特殊文件夹名称会影响脚本编译的顺序。
###### 预定义的程序集
- Unity 根据脚本文件在项目文件夹结构中的位置，以__四个不同的阶段编译脚本__。
	- Unity 为每个阶段创建一个单独的 CSharp 项目文件 (.csproj) 和一个预定义的程序集。
	- 如果没有符合编译阶段的脚本，Unity 不会创建相应的项目文件或程序集。

- 四个阶段的编译顺序
	- 1. 
	- 2. 
	- 3. 
	- 4. 
	- 注意：Standard Assets 仅在 Assets 根文件夹中有效。
- 编译顺序很重要
	- 当脚本引用在不同阶段编译的类（因此位于不同的程序集中）时，编译顺序很重要
	- 脚本引用的基本规则：
		- 1. 前面阶段不能引用后面阶段的：
			- 无法引用在当前阶段之后的阶段编译的任何内容
		- 2. 后面阶段的可以引用前面的：
			- 在当前阶段或早期阶段编译的所有内容则是完全可用的。

###### 自定义程序集文件
- 可以创建__程序集定义文件(.asmdef文件)__，从而使用自己的程序集来组织项目中的脚本。
- 使用程序集定义文件(.asmdef文件)来管理项目的好处：
	- 可以减少在进行不相关的代码更改时需要重新编译的代码量
	- 并可提供对其他程序集的依赖性的更多控制

###### 程序集定义文件is什么
- 可使用程序集定义文件根据文件夹中的脚本来__定义您自己的托管程序集__。
	- 请将项目脚本分成具有明确定义的依赖项的多个程序集
		- 以确保在脚本中进行更改时仅重新构建所需的程序集。这样可以减少编译时间。
- 应将每个__托管程序集__视为 Unity 项目中的__单个库__。

###### how use 程序集定义文件
- 将一个程序集定义文件添加到 Unity 项目中的某个文件夹，即可将该文件夹中的所有脚本编译为一个程序集。
- 



### 2.  Unity 的游戏功能与 Mono 运行时之间的关系




## 高级开发
### 托管代码剥离
- 托管代码剥离将从构建中删除未使用的代码，从而可以显著减小最终构建大小。
	- 使用 IL2CPP 脚本后端时，托管代码剥离还可以减少构建时间，因为需要转换为 C++ 并进行编译的代码减少。
- 托管代码剥离将从托管程序集（包括从项目中的 C# 脚本构建的程序集、包含在包和插件中的程序集以及 .NET 框架中的程序集）中删除代码。
#### 托管代码剥离工作方式
- 托管代码剥离的工作方式是对项目中的代码进行__静态分析__，检测出在执行过程中永远无法访问的__类__、__类成员__甚至__函数的某些部分__
	- 可以通过 Player Settings 窗口中的 Managed Stripping Level 设置（在 Optimization 部分）来控制 Unity 删除无法访问的代码的激进程度。
	- __重要信息：__当代码（或插件中的代码）使用反射来动态查找类或成员时，代码剥离工具不能总是检测出项目是否正在使用这些类或成员，因此可能会删除它们。
		- 要声明某个项目正在使用这样的代码，请使用 link.xml 文件或 Preserve 属性。
#### 托管剥离级别
- 使用项目的 Player Settings 中的 Managed Stripping Level 选项来控制 Unity 删除未使用代码的激进程度。

#### 托管代码剥离工作原理

### unity的自动内存管理
- Unity 的 Mono 引擎等运行时系统会自动为您管理内存
- 创建对象、字符串或数组时，用于存储它的内存是从称为堆的中央池分配的。当此项不再使用时，其先前占用的内存可被回收并用于其他目的。
#### Unity的值类型||引用类型 
-  Unity 的结构类型（例如，__Color__ 和 __Vector3__）是值类型
#### unity的GC使用的是2种方式(标记清楚、引用计数)的哪一个？
#### GC的优化 (GC需要好的使用)
- 垃圾收集是自动完成的，对程序员来说不可见，但收集过程实际上在__后台需要耗费大量 CPU 时间__。
	- 如果使用得当，自动内存管理通常在整体性能上能达到或超过手动分配。
		- 但是，程序员必须避免错误以免导致不必要的频繁触发垃圾回收器并在执行中引起暂停。
##### 不良使用 + GC -> 糟糕的结果
- 有一些臭名昭着的算法虽然一眼看上去好像是无辜的，但可能成为 GC 的噩梦
	- 1. 他们会快速产生源源不断地垃圾
1. 重复的字符串连接
2. 在会被大量调用的函数内使用new分配内存
##### GC下应避免出现的操作

#### 禁用GC
1. 好处：降低CPU的使用率
	- 如果使用的是 Mono 或 IL2CPP 脚本后端，则可以通过在运行时禁用垃圾收集来避免垃圾收集期间的 CPU 使用率激增。
2. 坏处： 因为垃圾回收器不会收集不再有任何引用的对象，垃圾只会逐渐增多

#### GC的使用策略
- 最好尽量避免内存分配。但是，鉴于无法完全消除这些行为，可采用两种主要策略来__最小化这些行为对游戏运行过程的干扰__：
##### 快速和频繁进行垃圾收集的小堆
##### 慢速但不频繁进行垃圾收集的大堆
##### 可重用的对象池


### 平台相关的编译
#### Scripting Define Symbols 
- why要使用Scripting Define Symbols ？？能带给我们什么
- 相当于C中的预编译相关的宏？？
- 用来指示预编译器如何预编译代码？？
##### Unity自带的Scripting Define Symbols 
- 位于.rsp文件下？
##### 自定义Scripting Define Symbols 
###### 平台自定义 #define 指令
- 打开 Player Settings 的 Other Settings 面板，并导航到 Scripting Define Symbols 文本框。
- 输入要为该特定平台定义的符号名称，以分号分隔。
- 随后可以将这些符号用作 #if 指令中的条件，就像内置条件一样。
###### 全局自定义 #define 指令
您可以定义自己的预处理器指令来控制在编译时包含的代码。为此，必须将包含额外指令的文本文件添加到 Assets 文件夹。文件名取决于您使用的语言。扩展名为 __.rsp__：
举例来说，如果在 mcs.rsp 文件中包含单行 -define:UNITY_DEBUG，则 #define 指令 UNITY_DEBUG 将作为 C# 脚本的全局 #define 指令存在，但 Editor 脚本除外。

- 1. 使用PlayerSetting方式
	- 如果只想修改全局 #define 指令，请使用 Player 设置中的 Scripting Define Symbols__，因为此选项涵盖了所有编译器。
- 2. 使用.rsp__ 文件方式：
	- 如果选择 .rsp__ 文件，则需要为 Unity 使用的每个编译器提供一个文件。

#### 使用Scripting Define Symbols 
- 是不是C#支持的预编译指令均可以使用？？？
- 一般使用这个做什么？？
	- 对同一份代码依据不同平台进行不同的处理？
		- 如：using的包 ...
##### 通过#define来使用

##### 通过 #if #elif #else #endif来使用
- 可以在函数内使用，而#define必须在头部使用



### 托管插件
- Unity 本身只支持 C# 编程语言
- 除此之外，许多其他 .NET 语言只要能编译兼容的 DLL，就可以用于 Unity；
- 通常，脚本作为源代码文件保存在项目中，并在每次源代码更改时由 Unity 进行编译。但是，也可以使用外部编译器将脚本编译为动态链接库 (DLL)。然后可以将生成的 DLL 添加到项目中，并且它包含的类可以像普通脚本一样附加到对象。
- 源代码vsDLL方式的优缺点
	- 源代码方式：
		- 在 Unity 中，使用脚本通常比使用 DLL 更容易。但是，可以访问以 DLL 形式提供的第三方 Mono 代码。
	- DLL方式：
		- 使用DLL，这样就能使用 Unity 不支持的编译器进行开发项目。
		- 使用DLL可以对源代码进行保密
#### 创建DLL
#### 使用DLL




## 特殊概念
### editor脚本 || runtime脚本 || 普通脚本

### 托管程序集 

### Editor模式||Runtime模式

### mono运行时
### 脚本访问引擎
### ECS实体组件系统

### Burst编译器

### Unity原生作业系统

### Job || Job Scheduler
https://en.wikipedia.org/wiki/Job_scheduler
https://en.wikipedia.org/wiki/Job_(computing)

### Blittable
https://en.wikipedia.org/wiki/Blittable_types
Blittable类型是Microsoft .NET Framework中的数据类型，在托管和非托管代码中在内存中具有相同的表示形式。