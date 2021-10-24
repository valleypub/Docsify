[toc]


这是对这本书中，我欠缺的一些知识点的记录。

# 第一章 Unity基础

## prefabs

1. 如何创建prefabs
	- 在Scene中完成对gameobject的配置后，然后从Hieracy中将GameObject拖到Project窗口及创建了Prefabs，且Project中的Prefabs和场景中的GameObject是相关联的。且还有如下特点：
		1. 删除场景中的gameobject实例并不会影响到Project窗口中的Prefabs
		2. 修改场景中的实例然后Apply后，会将修改自动同步到Project的Prefabs中
		3. 修改场景中的实例然后Revert后，会将场景中的实例退回到Project中的Prefabs的设置
		4. 修改Project的Prefabs，会将修改自动同步到场景中的实例上


## 实例化

1. Instantiate()的使用
	Instantiate()实例化Prefabs 为场景中的对象

2. 运行中动态实例化对象可能会造成比较多的内存开销，增加系统垃圾回收的时间。
	解决方案：使用==缓存池==避免动态内存申请


## 动态读取资源的方式

1. Resource文件夹 + ```Resources.Load<T>()``` 




# 第二章 太空射击游戏


1. 材质球边缘无法透明化，选择cultout
2. 如果一个物体不需要接受光线，可以使用简单的shader如：unlit / Texture 
	- 不需要接受光线指的是什么？？？


3. 摄像机视角与scene视角一致的方式
	1. 选中Main camera
	2. 在scene中拖拽的方式调整合适的位置
	3. 菜单栏 -> GameObject -> Align With View，自动调整MainCamera的transform参数


4. 设置gameobject的Lighting 组件的Cast Windows 是用来设置这个组件会不会投到别的物体上阴影


5. 默认新建的script组件，都会出现在Component -> Scripts -> Player；为了便于管理脚本，也可以使用特性```[AddComponentMenu("MyGame/Player")]```来统一自定义脚本在菜单栏中的位置。
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[AddComponentMenu("MyGame/Player")]
public class Player : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

```

6. Input.GetKey(KeyCode.UpArrow) 配合  +=  speed * Time.deltaTime来实现长按递增递减功能

```c#
if(Input.GetKey(KeyCode.UpArrow)){//GetKey表示长按
	
	moveH += speed * Time.deltaTime;

}
```

7. 不要再Update()中使用this.transform.xxx。
	每次使用this.transform时，都会在此游戏对象中查找Transform组件，然后再执行xxx操作
	替代方案：在Start()中，进行一次Transform m_transform = this.transform，然后保存下来这个引用，后续在Update()中使用m_transform.xxx，就不会每次在进行一次extra查询操作了。
	==同理:==，不仅游戏对象的transform组件，游戏对象上的一切组件(如：CharacterController  MeshRenderer 等)他们的引用都应该提前在Start() or Awake()中进行一次获取终身使用的方式。


8. 在Start()中调用Destroy(this.gameObject, time)来一定时间后销毁自身

9. Prefabs 配合 Intantiate() 来运行中动态动态触发产生游戏对象：如：子弹，敌人
10. 设置Tag的两种方式
	1. 选中Hieray中的任一游戏对象，在Inspector中点击Tag下拉菜单，使用addTag来新建
	2. Edit -> Project Setting -> Tag ang Layer来设置

11. 使用Pythics系统的BoxCollidar组件
	1. 选中BoxCollidar组件的 Is Trigger == true，然后可以使用OnTriggerEnter()方法
	2. OnTriggerEnter()方法重载自MonoBehavior函数，在碰撞体互相碰撞时会触发


12. 对于两个物体，只要一方设置了Rigibody 和 BoxCollidar组件，就能双方是都使用OnTriggerEnter()？？？？ or双方都要设置Rigibody 和 BoxCollidar组件？？


13. 各种Collidar组件的区别是什么？？？

14. this.transform.Translate()的使用：
```
m_transform.Translate( new Vector3(rx, 0, -speed * Time.deltaTime));
```

15. 确定两个游戏对象连线的方向：B指向A
```
Vector3 relativePos = B.position - A.position;

Instantiate( m_rocket, B.position, Quaternion.LookRotation(relativePos));

```


16. OnBecameVisible()回调函数 + Render组件的使用，实现超出屏幕就销毁的功能

```

```

17. 使用.unitypackage来导入导出文件
	- 导出文件时：
		1. 在Project窗口中，使用ctrl多选要导出的文件(可以是任何资源文件：文件夹、prefabs、图片、音频、视频)
		2. 鼠标右键 -> export package
	- 导入文件时：
		1. 菜单栏 -> asset -> import package -> custom package

18. AudioSource组件的public void PlayOneShot(AudioClip clip) 配合 AudioClip来使用。


19. 使用 StartCoroutine() + yield return + Instantiate() + Random来实现敌人生成器
```

```

20. 设置原本不可见的游戏对象(一般是只有脚本组件，没有render组件的gameobject)在scene视图中可见，在game视图中不可见。使用：Gizmos文件夹 + OnDrawGizmos()函数 + Gizmos.DrawIcon()
```

```


21. 使用多个Canvas + 对canvas使用SetActive()来实现 “登陆界面”，“死亡-重新挑战界面”功能

22. 可以在cs脚本内使用 button.onClick.AddListener(方法or委托对象名) 来实现在inspector中点击onclick + 拖动同样的效果


23. 在cs脚本中使用static限制成员来实现

24. 使用UnityEngine.SceneManagement; + OnButtonGameStart() + SceneManager.LoadScene("sceneName")来实现scene跳转
	- ==SceneManager静态类还有哪些有用的方法？？==
	- ==OnButtonGameStart()这个函数是属于MnoBehavior中的都是On开头的？？想这样的函数还有那些？？==



25. 使用==Layer==实现  发出的射线只与指定层碰撞
	1. 脚本中设置LayerMask
	2. 


26. Vector3提供了很多移动、旋转物体的方法
	1. MoveTowards(源pos，目标pos，距离)，返回的是朝这个方向移动指定距离后的新位置


27. Unity官方建议每间隔固定帧手动清理一次内存。如：使用Time.frameCount实现每30update帧，进行一次System.GC.Collect()。也可以在场景切换or场景关闭时手动使用System.GC.Collect()进行一次清理
```

```

28. Unity的缓存池技术。如使用缓存插件：Pool Manager或Pool Boss
	- 好处：
		- 通过提前创建出来，可以避免运行时间的内存开销



29. Collider组件的学习
	- GameObject 与另一个 GameObject 碰撞时，Unity 会调用 OnTriggerEnter。
	- 当两个 GameObjects 碰撞时，OnTriggerEnter 会在 FixedUpdate 函数上发生。涉及的碰撞体并不始终在初始接触点处。
	- __注意：__两个 GameObjects 都必须包含 Collider 组件。其中一个必须启用 Collider.isTrigger，并包含 Rigidbody。如果两个 GameObjects 都启用了 Collider.isTrigger，则不会发生碰撞。如果两个 GameObjects 都没有 Rigidbody 组件，情况同样如此。
	- 官方参考：
		- [Collider类官方介绍](https://docs.unity.cn/cn/current/ScriptReference/Collider.html)
		- [Collider.OnTriggerEnter(Collider)官方介绍](https://docs.unity.cn/cn/current/ScriptReference/Collider.OnTriggerEnter.html)


30. FixedJoint组件？？？


31. 射线经常和LayerMask一起配合使用，


## 太空射击游戏的改进

1. 飞船增加 调速功能、放大缩小功能、飞行方向改变功能、喷射火焰功能
2. 第三人称游戏改为伪第一人称游戏，这样我们可以看到飞船在3D Scenen中穿行的视角
3. 将2D的移到3D，摆放多个行星，飞船在行星间穿梭、行星上的降落等功能
4. 增加 万有引力、流星雨、黑洞等功能





# 第三章:第一人称射击游戏
1. 实际项目中，模型比较复杂时，这是需要两组模型：
	1. 一个具有较高的质量，用于显示。
	2. 一个专门用于物理碰撞。为了提高性能，碰撞模型做的相对简单。
	3. __使用时：__将物理模型套在显示模型的外层，然后将Mesh Collider碰撞检测组件添加到表层的(不可见的)物理碰撞模型上


### 一个第一人称的游戏对象是怎么在unity中做出来的？？

![一个游戏对象的组件拼装图]()

2. 使用CharacterController来模拟现实中的游戏主角，这个组件有以下很多有用的方法。基本上这些方法都是让CharacterController组件尽可能完全模拟出现实中游戏主角所能有的一切特点（如：移动、物理碰撞、.....  ）
	- 移动：.Move()。__在移动的同时还会自动计算移动体与场景之间的碰撞。__（这个自动计算的意思是，不需要额外的添加Collidar组件只用CharacterController就能进行物理碰撞检测？？？）
	- 


3. 使用Screen.lockCursor = true; 来锁定鼠标。==鼠标能锁定，那是不是键盘、等别的也能锁定？？？==


4. 使用transform组件的.TransformPoint()来移动到精确的位置。。






# 塔防游戏




# 第六章 Web服务器

1. 弱联网游戏is什么



2. why 网络服务器Web server 多，却不怎么见多Tcp Server???


3. Apache Nginx这些是干什么的？？why need 他们？？


4. netstat -a -n -o，如何定点查端口??如何关闭PID进程？？


## WWW类的用法



# 分类总结
## Physics系统的常用组件
- 应该将物理系统按抽象功能进行划分，每个抽象功能又可能有多种不同的实际实现。就像，SteamVR为了common按抽象的Action对输入系统进行划分一样。如果，如果也按抽象的物理Atrributes来划分，编程的时候也基于物理Atrributes来进行编程，就更容易掌握物理系统的本质
	- 如：
	- 物理系统
		- 碰撞检测组件
		- 力组件
		- 


### 碰撞检测组件(Collidar)
- why need 碰撞检测组件？？
	一般，我们之所以想检测监听碰撞事件，就是想将__碰撞事件发生__时开始做一些特殊的事情(即：在碰撞时运行一些特殊的方法)。如：vr中用碰撞检测来模拟手是否拿捏住物体，，，



- 一般主要用来检测监听"接触(碰撞)"的发生，然后在"接触(碰撞)"的发生

#### Box Collidar



#### Mesh Collidar



### 







