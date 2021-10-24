[toc]


# HTC Vive的诞生
## Valve -> steamVR
valve将OpenVR和Steam结合在一起开发出SteamVR，用来与steam平台形成互补，是一个专门用来发布VR内容的平台

## HTC -> 硬件



# SteamVR

Requires installing the SteamVR runtime via Steam to use.
SteamVR info (http://steamvr.com)
documentation (https://valvesoftware.github.io/steamvr_unity_plugin/)


- SteamVR2.0的重要更新是加入了__Input System__
	- __Input System__的核心概念是动作（Action），基于动作的输入系统对于游戏引擎来说更有意义，Unreal一直在沿用这种方案，而Unity目前在开发中的输入系统也将遵循这一原则
	- 开发中需要放弃之前关于__“按下某个按键发生什么事情”的思想__，取而代之的是使用__“做出某个动作发生什么事情”的思想__

- SteamVR2.0将动作抽象为以下6种类型：Boolean、Single、Vector2、Vector3、Pose、Skeleton等类型
	- __Boolean__类型的动作代表只有两种状态的动作：True或False，比如抓取（Grab）动作，只有抓取或未抓取两种状态，不存在中间状态；（在Unity中对应类为：SteamVR_Action_Boolean）
	- __Single__类型的动作能够返回0~1之间的数值，比如Trigger键按下到松开的过程；（在Unity中对应类为：SteamVR_Action_Single）
	- __Vector2__类型动作能够返回二维数，比如Touchpad上的触摸或手柄摇杆；使用这样的数值能够控制物体在四个方向的运动，典型的应用是使用Touchpad控制无人机或小车的运动；（在Unity中对应类为：SteamVR_Action_Vector2）
	- __Vector3__类型的动作能够返回三维数值；（在Unity中对应类为SteamVR_Action_Vector3）
	- __Pose__类型的动作表示三维空间中的位置和旋转，一般用于跟踪VR控制器；（在Unity中对应类为SteamVR_Action_Pose）
	- __Skeleton__类型的动作能够获取用户在持握手柄控制器时的手指关节数据，通过返回数据，结合手部渲染模型，能够更加真实的呈现手部在虚拟世界的姿态，虽然不及像Leap Motion等设备获取手指输入那样精确，但是足以获得良好的沉浸感；（在Unity中对应类为：SteamVR_Action_Skeleton）；


## 动作（Actions）

### Actions的提出
- 因：
随着越来越多的VR设备推出，控制器类型逐渐趋向于碎片化；每当有新的控制器发布，都会给开发者带来一些额外的工作量：游戏项目需要修改交互代码以适配新的设备；
从开发层面上来看，不同的控制器具有不同的键值映射，所以，当现有VR应用程序移植到另外一个VR平台的时候，需要针对目标平台进行交互适配；

- 果：
	- Valve为Unity开发者推出了SteamVR Unity Plugin2.0（简称SteamVR2.0），能够使开发者在编程中专注于用户的动作，而不是具体的控制器按键；
	- [Input System]与之前处理用户输入有显著的不同，使用[SteamVR Input System]，开发人员可以在应用程序之外定义默认的动作并与按键进行绑定，而不需要将输入视为某一特定设备的特定按键；这样新的设备可以快速适配应用程序，无需更改代码；
		- 比如：当开发者检测玩家是否抓取某个物体的时候，不是检测Vive等控制器的Trigger键或Oculus Touch控制器的Grip键是否被按下，而是检测预定义的“Grab”动作是否为True即可；（作为开发者，可以在SteamVR中为Grab动作设置默认按键和阈值，当程序运行时，也可修改这些数值以满足玩家的个人偏好）；基于这种机制，不光能够解决控制器碎片化的问题，也可以快速适配未来发布的设备；
	- __本质上是为了编写的代码可以不加修改的在别的vr设备上使用(即，脚本语言的common化)，将需要更改的部分下移到专门的一层：按键(实际vr相关的)-动作(abstrct脚本相关的)映射层__


### SteamVR中Actions的使用

#### ActionSet
- 动作通过动作集进行逻辑上的分组，以方便进行组织和管理，在Unity中对应的类为SteamVR_ActionSet
- 相当于对杂乱排放的抽象出来的各个动作进行了一次分类，比如：天上飞相关的动作、水里游相关的动作、陆上跑相关的动作；又或者按人畜分：人会做的动作、动物会做的动作

##### 默认ActionSet
SteamVR插件默认包含了三套动作集：default、platformer、buggy，开发者也可以在[SteamVR Input]窗口中自行添加或删除动作集；


##### ActionSet使用

1. SteamVR插件对 ActionSet和 Action的管理，通过 windows -> steamVR input，在打开的小界面中可以设置ActionSet，可以+ - Action，然后当点击【Save and Generate】按钮后，SteamVR插件将为动作以及动作集生成可编程访问的对象类，将它们放置在项目的Assets\SteamVR_Input\ActionSetClasses目录下：
2. 使用组件[SteamVR_ActivateActionSetOnLoad]可以在场景中自动激活和停用指定的动作集；对应激活和停用的方法是在Start()和OnDestroy()中实现；
	- SteamVR_ActivateActionSetOnLoad.cs在\Assets\SteamVR\Input\SteamVR_ActivateActionSetOnLoad.cs

##### 使用内置动作
###### 在代码中使用动作和动作集
- 方式1：
在项目代码中，使用[SteamVR_Input]类可以静态引用每个动作和动作集，在每个动作集中，可以找到其包含的动作的引用；
```c#
//立钻哥哥：当检测到任意控制器发出default动作集中包含的Teleport动作时，执行Teleport()函数

void Update(){

if(SteamVR_Input._default.inActions.Teleport.GetStateUp(SteamVR_Input_Sources.Any)){

    Teleport();

    }

}

```

- 方式2：
1. 选择游戏对象[CameraRig]，为其挂载“SteamVR_ActivateActionSetOnLoad”组件，并指定启用“platformer动作集”
2. 编写一个cs来通过静态类SteamVR_Input使用动作
```c#
using UnityEngine;

using Valve.VR;

 

//立钻哥哥：监听输出动作集数据

public class YanlzVRGetMyMoveAction : MonoBehaviour{

    void Update(){

        /*注意：SteamVR2.2.0不能使用（SteamVR_Input.platformer了）

        if(SteamVR_Input.platformer.inActions.Move.GetChanged(SteamVR_Input_Sources.Any)){

            Vector2 pos = SteamVR_Input.platformer.inActions.Move.GetAxis(SteamVR_Input_Sources.Any);

            Debug.Log(“立钻哥哥：pos:” + pos);

        }

        */

 

        //立钻哥哥：SteamVR2.2.0使用GetAction获取动作集

        //SteamVR_Input.GetAction<SteamVR_Action_Vector2>(“platformer”, “Move”)

        if(moveAction != null && moveAction.GetChanged(SteamVR_Input_Sources.Any)){

            Vector2 pos = moveAction.GetAxis(SteamVR_Input_Sources.Any);

            Debug.Log(“立钻哥哥：pos: ” + pos);

        }

    }

 

    //立钻哥哥：SteamVR2.2.0使用GetAction获取动作集

    public SteamVR_Action_Vector2 moveAction = SteamVR_Input.GetAction<SteamVR_Action_Vector2>(“platformer”, “Move”);

    public SteamVR_Action_Boolean jumpAction = SteamVR_Input.GetAction<SteamVR_Action_Boolean>(“platformer”, “Jump”);

 

}    //立钻哥哥：public class YanlzVRGetMyMoveAction :MonoBehaviour{}

```





##### 使用自定义动作

##### 测试动作视窗
选择【Window -> [SteamVR Input Live View]】命令，即可打开一个测试输入窗口，此窗口将实时展示所有动作集合的状态；当一个动作的值发生变化时，对应右侧会突出显示绿色，然后逐渐消失




##### 动作绑定
- 是什么
创建动作以后，需要将动作进行默认绑定；

- how 
打开VR控制器，保持SteamVR客户端开启，在[SteamVR Input]窗口中，点击[Open binding UI]按钮，此时将使用操作系统默认的网页浏览器打开SteamVR动作绑定页面；




# HTC VIVE开发基础
此部分主要参考：
1. https://blog.csdn.net/VRunSoftYanlz/article/details/81989970


## 第一篇：快速入门篇

### A.1-开发环境配置
#### ViveSetUp
#### Unity下安装SteamVR Plugin

### A.2-SteamVR Plugins简单使用

### A.3-SteamVR输入控制

### A.4-Teleport系统
#### Teleport系统概述
在VR中玩家的移动有两种方式；
1. 第一种：靠头盔的移动（支持头盔移动的设备）；
2. 第二种：靠瞬移；（Teleport：即玩家从当前位置瞬间移动到另一个位置）

#### Teleport适用情况(何时才该使用Teleport)
1. 适用于较大的场景，超过Room-Scale的大小；（参考案例中《紫禁城》）
2. 适用于不能检测头盔移动的VR设备，如Oculus DK1 DK2；（设备本身只支持旋转，不支持位移；所以如果想位移必须借助Teleport）

- 看来Teleport系统属于SteamVR 而不属于某一硬件平台

#### Teleport分类
按照复杂程度和效果可以分为三类：Simple Line Teleport；Complex Line Teleport；Arc-Line Teleport
1. Simple Line Teleport
	- 从手柄处朝向正前方发射一条射线，在HitPoint处显示一个Marker标识要移动到的目标点；
	- [表现形式]：
		- 射线可以在指定的LayerMask中自由移动射线和Marker；但是当进入非指定LayerMask后射线则不刷新
	- 示意图：
		- ![]()
2. Complex Line Teleport
	- 从手柄处朝向正前方发射一条射线，在HitPoint处显示一个Marker标识要移动的目标点；但是解决了射线在指定LayerMask之外时也刷新；
	- [表现形式]：
		- 同样为一条射线，外加一个Maker；但是当在指定LayerMask之内会呈现绿色；在指定LayerMask之外会呈现红色；
	- 示意图：
		- ![]()
3. Arc-Line Teleport
	- 从手柄处朝手柄正前方发射一条弧线（Arc），弧度会随着手柄与地面的夹角变化而变换；并且在HitPoint处显示Marker；
	- [表现形式]：
		- 一条弧线，外加一个Marker；同样支持检测是否在指定的LayerMask之内，如果在则为正常颜色；如果不在则变为红色；
	- 示意图：
		- ![]()

#### Teleport代码实现




## 第二篇：基础夯实篇

## 第三篇：中级进阶篇

## 第四篇：高级成魔篇




# 疑问

1. SteamVR的渲染的定位系统怎么做的？？？CameraRig的世界坐标是，运行程序的那一刻的头显的真实坐标关联？？还是CameraRig的世界坐标是定位器的坐标？？
2. 不只可以从游戏对象的transform组件通过 transform.gameobject来获取它所属的游戏对象，还可以从游戏对象的Collidar组件来通过col.gameobject来获取它所属的游戏对象 ->>>> 是不是说明，可以从游戏对象的任意组件通过 .gameobjec获取它所附属的游戏对象？？？？？岂不说明.gameobjec这个属性在所有组件共有的部分，即Componet基类中的》？？？？

