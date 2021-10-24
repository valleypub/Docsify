[toc]

# Scripting concepts

- Unity 对脚本使用标准 Mono 运行时的实现方案
- 但在从脚本访问引擎方面，仍然有自己的惯例和技术
- 本部分讲述2方面：
	- 介绍如何通过脚本控制 Unity Editor 中创建的对象
	- 详细说明 Unity 的游戏功能与 Mono 运行时之间的关系。

## use脚本组件控制 Unity Editor 中创建的对象
- 游戏对象的__行为__由附加的__组件__控制。
- 内置的组件很多，但还不够。
	- 内置的都是common的
	- 专用的组件要通过脚本来进行扩充
- 在创建脚本时，实际上是在自定义新的组件类型
	- 可以像任何其他组件一样将这种组件附加到游戏对象
		- 通过__拖动__来进行附加
	- 脚本只定义了组件的蓝图(== 只是声明了一个class，但并没使用class创建对象)，因此在将脚本实例附加到游戏对象之前，不会激活任何代码
	- 组件实际上是类的实例
### 脚本组件相关
### 1. 创建脚本组件
### 2. 使用脚本组件
### 3. 变量和inspector
- Unity 通过在变量名称中出现大写字母的位置引入空格来创建 Inspector 标签。但是，这纯粹是出于显示目的，在代码中应始终使用变量名称。
- inspector界面能显示的变量
	- 1. public限制的变量直接会显示
	- 2. private限制的变量
		- 必须通过添加 [Serialized]才能在inspactor显示
- Unity 实际上允许您在游戏运行时更改脚本变量的值。
	- 此功能很有用，__无需停止和重新启动__即可直接查看更改的效果。
	- 当游戏运行过程结束时，变量的值将重置为按下 Play 之前所处的任何值。
		- 这样可确保自由调整对象的设置，而不必担心会造成任何永久性损坏。

### 4. 使用脚本组件控制GameObject
- 脚本组件存在的意义就是控制GameObject

#### 组件控制GameObject的两种方式
- 1. 直接在inspector中修改
	- 使用组件的 Inspector 来更改组件属性 -> 控制组件 -> 控制游戏对象
- 2. 使用脚本更灵活的修改
	- 脚本可以随着时间推移而逐渐改变属性的值，或者响应用户的输入，这是通过inspector不可能做到的
	- Inspector 中所没有的一项额外功能是以脚本方式可以在组件实例上调用函数
	- 通过在适当时间更改、创建和销毁对象，可以实现任何类型的游戏运行过程
#### 1. 脚本组件访问组件
##### 同一游戏对象上
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

##### 不同游戏对象上

#### 2. 脚本组件访问对象
- 脚本检索子对象和无关联的对象的方式是一样的吗？检索子对象会不会有什么特别的便利
##### 运行前确定对象
- 1. 拖放引用法
	- 向脚本添加公共的游戏对象变量 + 将对象从场景或 Hierarchy 面板拖到此变量上
	- 在处理具有永久连接的单个对象时，将对象与变量链接在一起是最有用的方法。
	- 可以使用数组变量来链接同一类型的多个对象，但仍然必须在 Unity Editor 中（而不是在运行时）进行连接。
- 2. 
##### 运行时再确定对象
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

### 5. 事件函数(event functions)
- Unity 中的脚本与传统的程序概念不同。
	- 在传统程序中：
		- 代码在循环中连续运行，直到完成任务
	- Unity 中：
		- Unity 通过调用在脚本中声明的某些函数(event functions)来间歇地将控制权交给脚本。函数执行完毕后，控制权将交回 Unity。
			- [详细的事件函数介绍](https://docs.unity3d.com/cn/current/ScriptReference/MonoBehaviour.html)

#### 初始化事件
- 如果能在游戏运行过程中进行任何更新之前调用初始化代码，通常会很有用
	- 脚本组件 like 类
	- 脚本组件中的初始化函数 like 类的构造函数
		- 因为unity不支持类中使用构造函数

- 1. 场景加载时会为场景中的每个对象调用 Awake 函数。
- 2. 请注意，虽然__各种对象的 Start 和 Awake 函数的调用顺序是任意的__，但在调用第一个 Start 之前，所有 Awake 都要完成。(是所有对象的awake()都要完成 or 这个对象的awake()要完成？？)
	- 这意味着 Start 函数中的代码可以利用先前在 Awake 阶段执行的其他初始化。
- 3. 在第一帧之前或开始对象的物理更新之前需要调用 Start 函数。

#### 更新事件
##### 常规更新事件(Update)
- 游戏的帧率不是恒定的(取决于一次Update要花费的时间)
	- [Time.deltaTime](https://docs.unity3d.com/cn/current/ScriptReference/Time-deltaTime.html) 
		- 完成上一帧所用的时间（以秒为单位）（只读）。
		- 此属性提供当前帧和上一帧之间的时间
		- 这个值是怎么计算的啊？？？
- 两次Update 函数调用之间的时间长度也不是恒定的
##### 物理更新时间(FixedUpdate)
- 物理引擎也采用与帧渲染类似的方式以离散时间步骤进行更新。
- 在每次物理更新之前都会调用一个称为 FixedUpdate 的单独事件函数。
- 由于物理更新和帧更新__不会以相同频率进行__，所以如果将物理代码放在 FixedUpdate 函数而不是 Update 中，此代码将产生更准确的结果。
##### (LateUpdate)
- 为场景中的所有对象调用 Update 和 FixedUpdate 函数之后以及计算所有动画之后，如果能进行其他更改，也会很有用。
	- 一个例子是摄像机应该聚焦于目标对象；必须在目标对象移动后才能调整摄像机的方向。
	- 另一个例子是脚本代码应该覆盖动画的效果（例如，让角色的头部看向场景中的目标对象）。
- 可使用 LateUpdate 函数来处理这些类型的情况。

#### 物理事件
- 物理引擎将通过调用该对象的脚本上的事件函数来报告对象的碰撞情况。

### 6. 事件函数的执行顺序



### 7. 时间和帧率管理
#### 普通帧间隔
- 在处理这种基于时间的动作时要记住的一项重要规则是：
	- 游戏的帧率不是恒定的
	- Update 函数调用之间的时间长度也不是恒定的。
#### 固定时间步长
#### Maximum Allowed Timestep
#### 时间标度
#### Capture Framerate

### 8. 创建和销毁游戏对象
#### 1. 在运行之前创建游戏对象
#### 2. 在游戏运行过程中创建和删除游戏对象
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


### 9. 特性(Attribute)
- 特性 (Attribute) 是可以放在C#脚本中的类、属性或函数上方来指示特殊行为的标记。
- why要存在特性？？
- unity共有多少种特性？？
- .NET中也有特性这个概念，特性这个concept是一个通用的concept????
#### Unity 提供了在 API 参考文档中列出的大量特性：
##### UnityEngine 特性

- 在UnityEngine下的Attributes分支下均是：

##### UnityEditor 特性

- 在UnityEditor下的Attributes分支下均是：

##### .NET 库中还定义了一些有时可能在 Unity 代码中很有用的特性。

- [请参阅 Microsoft 关于特性 (Attributes) 的文档以了解更多信息](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/)
	- 注意：不要使用 .NET 库中定义的 ThreadStatic 特性；如果将其添加到 Unity 脚本，会导致崩溃。


### 协程
#### 有些任务使用协程比函数调用好

#### 有些任务只能使用协程替代函数调用

1. 动画刷新

### UnityEvent

### Null Reference Exceptions
#### Null Reference Exceptions产生原因
- 尝试访问未引用任何对象的引用变量时，便发生 NullReferenceException。
	- c# 和 JavaScript 中的引用变量在概念上类似于 C 和 C++ 中的指针。引用类型默认初始化为 null，表示未引用任何对象。
	- 如果引用变量未引用任何对象，则将其视为 null。当变量为 null 时，运行时将通过发出 NullReferenceException 来告知正在尝试访问对象。
- 发生 NullReferenceException的一些情况：
	- 脚本中使用Find()函数查找一个不存在此名称的游戏对象会返回 null
	- 另一个原因是使用了应该在 Inspector 中初始化的变量。如果忘记这样做，则变量将为 null。
```
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {

    // 使用此函数进行初始化
    void Start () {
    	//该代码简单地查找一个名为“wibble”的游戏对象。在此示例中不存在该名称的游戏对象，因此 Find() 函数返回 null
        GameObject go = GameObject.Find("wibble");
        Debug.Log(go.name);
    }

}
```
#### 处理Null Reference Exceptions的方法
- 虽然发生这种情况时令人沮丧，但这只是意味着需要更加注意脚本。
##### 使用NULL检查
- before we try and do anything with the 引用类型 variable, we check to see that it is not null. If it is null, then we display a message.
```
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {

    void Start () {
        GameObject go = GameObject.Find("wibble");
        if (go) {
            Debug.Log(go.name);
        } else {
            Debug.Log("No game object called wibble found");
        }
    }

}
```
##### 使用Try/Catch块
```
using UnityEngine;
using System;
using System.Collections;

public class Example2 : MonoBehaviour {

    public Light myLight; // 在 Inspector 中设置

    void Start () {
        try {
            myLight.color = Color.yellow;
        }       
        catch (NullReferenceException ex) {
            Debug.Log("myLight was not set in the inspector");
        }
    }

}
```


# Important Classes
1. This section provides an overview of some of the most commonly used and important built-in classes in Unity that you may want to use when scripting.
	- do not cover all classes in Unity 
	- do not cover every member of the classes which are covered.

## Object: 
The base class for all objects that Unity can reference in the editor.
## GameObject: 
Represents the type of objects which can exist in a Scene.
## MonoBehaviour: 
The base class from which every Unity script derives, by default.
## Transform: 
Provides you with a variety of ways to work with a GameObject’s position, rotation and scale via script, as well as its hierarchical relationship to parent and child GameObjects.
## Vectors: 
Classes for expressing and manipulating 2D, 3D, and 4D points, lines and directions.
## Quaternion: 
A class which represents an absolute or relative rotation, and provides methods for creating and manipulating them.
## ScriptableObject: 
A data container that you can use to save large amounts of data.
## Time (and framerate management): 
The Time class allows you to measure and control time, and manage the framerate of your project.
## Mathf: 
A collection of common math functions, including trigonometric, logarithmic, and other functions commonly required in games and app development.
## Random: 
### Random类的介绍
- Provides you with easy ways of generating various commonly required types of random values.

- Random的方法竟然可以直接使用在数组的[ ]之中

### Random类的应用
- unity中的添加随机游戏元素就是通过各种灵活地使用Random类来实现的

[官方讲解](https://docs.unity3d.com/cn/2018.4/Manual/RandomNumbers.html)

#### 从数组中选择一个随机项
- 随机选取数组元素值一般均可简化为随机选取下标值
- Random.Range 从包含第一个参数但不包含第二个参数的范围内返回一个值，因此在此处使用 myArray.Length 会得到正确的结果
```
var element = myArray[Random.Range(0, myArray.Length)];
```
#### 选择具有不同概率的项

#### 加权连续随机值
#### 列表洗牌
#### 从一组无重复的项中选择
#### 空间中的随机点

## Debug: 
Allows you to visualise information in the Editor that may help you understand or investigate what is going on in your project while it is running.
## Gizmos and Handles: 
allows you to draw lines and shapes in the Scene view and Game view, as well as interactive handles and controls.


2. a more complete reference of all the built-in classes and every member available, see the [Script Reference API](https://docs.unity3d.com/cn/2020.3/ScriptReference/index.html).




# Plug-ins
- 在 Unity 中，通常使用脚本来创建功能，但也可使用__插件__形式包含 Unity 外部创建的代码。
- 可在 Unity 中使用两种插件：
	- __托管插件__：使用 Visual Studio 等工具创建的__托管 .NET 程序集__
	- __原生插件__：特定于平台的__本机代码库__

## 托管插件
- 编译后的dll == 托管插件 == 托管 .NET 程序集
1. 托管插件是使用 Visual Studio 等工具创建的__托管 .NET 程序集__
	- 此类插件仅包含 .NET 代码，因此无法访问 .NET 库不支持的任何功能。
	- 但是，Unity 用来编译脚本的标准 .NET 工具可以访问托管代码。
	- 因此，托管插件代码(DLL)和 Unity 脚本代码之间区别不大，唯一的区别是插件在 Unity 外部编译而成，因此源代码可能不可用。
2. 编译后的 DLL 在 Unity 中称为托管插件
	- 通常，Unity 将脚本作为源代码文件保存在项目中，并在每次源代码更改时都会编译这些脚本。
	- 但是，您可以使用外部编译器将脚本编译为动态链接库 (DLL)。然后可以将 .dll 文件添加到项目中，并将该文件包含的类附加到游戏对象，就像普通脚本一样。

### 创建托管插件(DLL)
1. 如果 DLL 不包含依赖于 Unity API 的代码，则可以使用适当的编译器选项将它直接编译为 .dll 文件。
	- 并非所有能生成 .NET 代码的编译器都能保证与 Unity 协同工作，因此在使用编译器进行重要工作之前，应使用一些可用的代码来测试该编译器是否兼容。
2. 如果确实想使用 Unity API，则需要将 Unity 自身的 DLL 提供给编译器。
	- Unity API所在的路径(Unity DLL 的路径为)：
		- windows：
			- C:\Program Files\Unity\Editor\Data\Managed\UnityEngine
	- UnityEngine 文件夹包含多个模块的 .dll 文件，您可以引用这些文件来获取所需的特定命名空间。
	- 此外，某些命名空间需要引用 Unity 项目中某个已编译的库（例如，UnityEngine.UI），该库位于项目文件夹的目录中：
		- ~\Library\ScriptAssemblies

### 使用托管插件
1. 编译完 DLL 后，便可以像任何其他资源一样将 .dll 文件拖到 Unity 项目中。托管插件有一个折叠三角形，可用于显示库中的单独类。
2. 可以像普通脚本一样将从 MonoBehaviour 派生的类拖到游戏对象上。
3. 可以按常规方式直接从其他脚本中使用非 MonoBehaviour 类。
	- DLL内有命名空间的，别的脚本使用DLL中的类需先using 命名空间
	- DLL无命名空间的，别的脚本使用DLL中的类直接使用？？



## 原生插件
原生插件 == 用 C、C++、Objective-C 等编写的原生代码库 == UnityEngine??
1. 此类插件可访问__操作系统调用__和__第三方代码库__等功能；Unity 无法通过其他方式使用这些功能。
2. 但是，Unity 的工具无法以__托管库__的方式访问这些库。
	- 例如，如果忘记将托管插件文件添加到项目中，您将收到标准编译器错误消息。
	- 如果也忘记将原生插件添加到项目中，则只会在尝试运行项目时看到错误报告。

3. Unity 广泛支持原生__插件__，即用 C、C++、Objective-C 等编写的__原生代码库__。
	- 原生代码库是什么意思？？
	- 原生插件是自带的UnityEngine吗？？

### 创建原生插件

### 使用原生插件
- 在 iOS 上，插件以静态方式链接到可执行文件中，因此我们必须使用```[DllImport ("__Internal")]```。
- 其他平台会动态加载插件，因此传递插件动态库的名称```[DllImport ("PluginName")]```。
- 示例：
```
using UnityEngine;
using System.Runtime.InteropServices;

class SomeScript : MonoBehaviour {

    #if UNITY_IPHONE
    // 在 iOS 上，插件以静态方式链接到
    //可执行文件中，因此我们必须使用 __Internal 作为
    // 库名。
    [DllImport ("__Internal")]

    #else
    // 其他平台会动态加载插件，因此
    // 传递插件动态库的名称。
    [DllImport ("PluginName")]

    #endif
    
    private static extern float FooPluginFunction ();
    
    void Awake () {
    // 在插件中调用 FooPluginFunction
    // 并将 5 输出到控制台
    print (FooPluginFunction ());
    }
}
```
### else
[Mono 互操作性与本机库](http://www.mono-project.com/docs/advanced/pinvoke/)

## 低级原生插件接口


## 构建适用于桌面平台的插件
### macOS
### Linux
1. Linux 上的插件是具有导出函数的 .so 文件。这些库通常用 C 或 C++ 编写而成，但也可使用任何语言编写。
2. 与其他平台一样，应使用 C 链接来声明所有 C++ 函数以免发生名称错用问题。
### windows
#### 构建适用于windows桌面平台的插件
1. Windows 上的插件是具有导出函数的 DLL 文件。实际上，任何可创建 DLL 文件的语言或开发环境均可用于创建插件。 
2. 与 Mac OSX 一样，__应使用 C 链接来声明所有 C++ 函数__以免发生名称错用问题。
```
extern "C" {
  float FooPluginFunction ();
}
```
3. 插件放置位置
	- 在 Windows 和 Linux 上，可以手动管理插件
		- （例如，在构建 64 位播放器之前，将 64 位库复制到 Assets/Plugins 文件夹中，在构建 32 位播放器之前，将 32 位库复制到 Assets/Plugins 文件夹中），
	- 或者可以将 32 位版本的插件放在 Assets/Plugins/x86 中，将 64 位版本的插件放在 Assets/Plugins/x86_64 中。
	- 默认情况下，Editor 将首先查看特定于架构的子目录，如果该目录不存在，则从 Assets/Plugins 根文件夹中复制插件。

#### 使用适用于windows桌面平台的插件
4. 按名称查找来使用：
```
[DllImport ("PluginName")]
private static extern float FooPluginFunction ();
```
### 跨平台使用插件
1. 只需在 Plugins 文件夹中包含同一套功能(如:同一组函数脚本)的多个平台的版本的插件文件： .bundle（对于 Mac）、.dll（对于 Windows）和 .so（对于 Linux）文件。 
2. 然后便不需要您执行任何其他操作，Unity 会自动为目标平台选择正确的插件并将其包含在播放器中。




# C# Job System
1. 借助 Unity C# 作业系统，您可以编写简单安全的多线程代码来__与 Unity 引擎进行交互__以提高游戏性能

2. 可将 __C# 作业系统__与 __Unity 实体组件系统 (ECS) __结合使用，通过这种架构可轻松为所有平台创建高效的机器代码。

## C# Job System概述
1. 专为编写多线程代码
2. 将 __Burst 编译器__与 __C# 作业系统__配合使用可以提高代码生成质量，还可以__大大降低移动设备的电池消耗__。
3. C# 作业系统的一个重要特点是它与 Unity 内部使用的系统（Unity 的原生作业系统）相集成。
	- 用户编写的代码与 Unity 共享工作线程
	- 此协作避免了创建超过 CPU 核心数的线程（这种情况会导致争用 CPU 资源）
		- 线程数多于 CPU 核心数会导致线程相互竞争 CPU 资源，进而造成频繁的__上下文切换__
		- 上下文切换是__资源密集型的过程__，因此应尽可能避免

[Unity at GDC - Job System & Entity Component System](https://www.youtube.com/watch?v=kwnb9Clh2Is&list=RDCMUCG08EqOAXJk_YXPDsAvReSg&start_radio=1&t=8s)

## 你真的理解多线程吗

- 多线程是一种编程方式，利用了 CPU 在多个核心上同时处理多个线程的能力

### 主线程
- 默认情况下，在程序的开头会运行一个线程，这就是“主线程”。
- 主线程会创建新线程来处理任务。这些新线程并行运行，通常在完成后将其结果与主线程同步(过程中也可以，数据是共享的)。

### 线程池
- 如果线程的数目很多、线程的生命周期又都很短 -> 这种情况下可能会挑战 CPU 和操作系统处理能力的极限。
	- 设置一个__线程池__可以缓解__线程生命周期__的问题。
	- 但是，即使使用线程池，也可能会同时激活大量线程。 线程数多于 CPU 核心数会导致线程相互竞争 CPU 资源，进而造成__频繁的上下文切换__。
		- 使用unity的__C#作业系统__来直接避免上下文切换


## 作业系统
### 作业系统概述
- 作业系统通过__创建作业__而不是线程来管理多线程代码。

- 作业系统__跨多个核心__管理一组工作线程。
	- 此系统通常每个逻辑 CPU 核心对应一个工作线程，这样可以__避免上下文切换__（但可能会为操作系统或其他专用应用程序保留一些核心）。

- 作业系统将作业放入作业队列中以待执行。作业系统中的工作线程从作业队列中获取并执行所需项。作业系统会管理__依赖关系__并确保作业以适当的顺序执行。

- Unity的作业系统is安全的
	- Unity C# 作业系统可以检测所有潜在的竞争条件，并尽量避免可能导致的错误
### 作业
- 一般通用定义(wiki中)：
	- 一个作业是完成一项特定任务的一个小工作单位。
	- 作业会接收参数并对数据进行操作，其行为方式类似于方法调用。
	- 作业可以是独立的，也可依赖其他作业完成之后才能运行。
- Unity中的“作业”是 Unity 中对于任何__实现 IJob 接口__的结构的统称。

### 作业依赖关系

- 在复杂的系统中，如游戏开发所需的系统中，不太可能每个作业都是独立的，一个作业通常会为下一个作业准备数据。
- 作业知道并支持使系统顺利运转的依赖关系。 
	- 如果 jobA 依赖于 jobB，作业系统将确保 jobA 不会在 jobB 完成之前开始执行。
		- unity是采用__JobHandle__ 来实现的
			- 可以在代码中使用 JobHandle 作为其他作业的依赖项。如果一个作业依赖于另一个作业的结果，则可以将第一个作业的 JobHandle 作为参数传递给第二个作业的 Schedule 方法


### C#作业系统is安全的
#### 竞争条件
1. 编写多线程代码时，__总是存在__出现竞争条件的风险
	- 当一个操作的输出取决于不受其控制的另一个过程的时序时，即出现竞争条件
2. 竞争条件__并不总是错误__，但它是不确定行为的根源。
	- 当竞争条件确实会导致错误时，可能很难找到问题的根源
		- 1. 因为这种情况__取决于时序__，所以只有在极少数情况下可以复现问题。
		- 2. 对此情况进行调试可能会导致问题消失，因为断点和日志记录可能会改变各个线程的时序。
3. 竞争条件是编写多线程代码时遭遇的最大挑战。

#### Unity的安全作业系统
- Unity C# 作业系统可以检测所有潜在的竞争条件，并尽量避免可能导致的错误。

##### 安全作业系统的实现原理
1. 隔离数据，从而消除竞争条件
	- 1. 数据引用 -> 复制数据副本
		- 如果 C# 作业系统将主线程中对代码数据的引用发送给一个作业，则系统无法验证主线程在读取数据的同时是否该作业正在写入数据。这种情况下便会产生竞争条件。
			- C# 作业系统解决这个问题的方法是__向每个作业发送其需要操作的数据的副本，而不是对主线程中的数据进行引用__。此副本可以隔离数据，从而消除竞争条件。


## use作业系统
### 创建作业
### 调度作业
### 