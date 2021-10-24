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

