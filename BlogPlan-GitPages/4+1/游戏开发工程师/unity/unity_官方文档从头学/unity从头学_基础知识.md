[toc]


# unity基础

## 1. 场景(scene)
- 场景就是对实际游戏中的场景的抽象
	- 如：每个关卡对应一个场景
- a sample scene that contains only a Camera and a Light.
- 单个场景相关的：
	- 创建
	- 使用
- 多个场景相关的：
	- 创建
	- 使用
	- scenes相互间的交互：
### Creating, loading, and saving scenes.
#### Creating a new scene
1. Unity creates every new scene from a scene template.



2. There are several ways to create a new scene:
- 1. Use the New Scene dialog to create a new scene from a specific scene template.
- 2. Use the menu or the Project window to create new scenes from your Project’s Basic scene template without opening the New Scene dialog.
- 3. Create a scene from a specific template directly from a __C# script__.
	- use the Instantiate method
		- The Instantiate method instantiates a new scene from a scene template. 
		- It returns the newly created Scene handle, and its matching SceneAsset. 
		- You can create this scene additively. If the scene contains assets that need to be cloned, you must provide a path for Unity to save the scene to disk.
```
Tuple<Scene, SceneAsset> SceneTemplate.Instantiate(SceneTemplateAsset sceneTemplate, bool loadAdditively, string newSceneOutputPath = null);
```

3. New scene events
- 只要创建scene就会triger一个event（不管是用什么方式创建的）
	- When you create a new scene from a template, either __from a script__ or __using the New Scene dialog__, Unity triggers an event. 
- 何时触发event
	- Unity triggers this event after the template is instantiated, and also after it triggers the EditorSceneManager.newSceneCreated or EditorSceneManager.sceneOpened events.
- unity创造这个event的目的是什么？
	- 平时也没用到过这个啊
- 此event的模板
```
public class SceneTemplate
{
    public delegate void NewTemplateInstantiated(SceneTemplateAsset sceneTemplateAsset, Scene scene, SceneAsset sceneAsset, bool additiveLoad);

    public static event NewTemplateInstantiated newSceneTemplateInstantiated;
}
```
#### Loading scenes
- 能不能像create scene那样也在C#脚本中进行loading scene？？？

#### Saving scenes



### Scene Templates
#### Scene Templates concept
1. Unity uses scene templates to create any new scenes. 
	- Scene templates are assets that are stored in a project.
	- They are similar to scenes, but are designed to be copied rather than used directly.
2. Think of a scene template as a pre-configured scene that contains all of the content you want to start with.
	-  For example, the default Basic template usually contains a Camera and a light.

3. Scene template的种类
	- Built-in templates：
		- Basic template 
			- creates a scene with a Camera and a light
		- Empty template 
			- creates an empty scene.
	- user-defined templates：

4. Built-in templates vs. user-defined templates
	- Built-in templates： 
		- 1. they are not assets stored in the project,
		- 2. cannot modify them.
	- user-defined：
		- 1. User-defined scene templates are assets that Unity stores in the project
		- 2. you create them from your own scenes. 

#### Creating scene templates: 
Describes the different ways to create a scene template.

- You can create a template from any Unity scene. After you create a template, you can create any number of new scenes from it.
#### Editing scene templates: 
Explains how to edit Scene template properties.
#### Customizing new scene creation: 
Explains how to attach a script to a scene template so you can run custom code when Unity creates a scene from the template.
#### Scene template settings: 
Describes project settings for scene templates. Most of these settings control how Unity closes and references scene dependencies when you create a new scene from a template.

#### Templates and scene dependencies
1. When you create a scene template, you can specify whether Unity clones or references its dependencies (the assets it includes) when you create a new scene from it.
	- To specify which assets Unity clones for a specific template, edit the template’s properties.
	- A typical template might contain a mix of cloned and referenced assets. Unity sets several asset types to clone by default.
	- To change whether Unity clones or references a given asset type by default, edit the Scene template project settings.

##### Cloning template assets
Cloned assets are copies of the original assets that the template scene uses. When Unity creates the new scene from the template, it automatically modifies the new scene to use any cloned assets. If you modify the cloned assets, it does not affect the template scene. If you modify the original assets in the template scene, it does not affect the new scene.

Cloning template assets is useful when you want new scenes to contain a starting set of assets that users might modify.

##### Referencing template assets
Referenced assets are the original assets that the template scene uses. When Unity creates the new scene from the template, the new scene points to the same assets as the template scene. If you modify those assets, it affects both the new scene and the template scene.

Referencing template assets is useful when you want new scenes to contain a default set of assets that users build on top of, but do not modify.

### Multi-scene editing(多场景编辑)

## 2. 游戏对象(GameObject)
### 游戏对象简介
1. 游戏中的每个对象（从角色和可收集物品到光源、摄像机和特效）都是游戏对象。
2. 游戏对象本身无法执行任何操作，不同对象的区别完全是由附加其上的组件决定的
	- 您需要向游戏对象提供属性(即添加组件or多个组件的组合)，然后游戏对象才能成为角色、环境或特效等等模拟世间一切事物。
		
		- 例如，通过将光源组件附加到游戏对象来创建光源
	- 游戏对象始终附加一个变换组件（表示位置和方向），并且无法删除此组件
		
		- 因为如果没有变换组件，游戏对象将在世界中没有位置。
	- Unity中的组件
		- 1. 内置组件：
			
			- 有很多
			- 还不够多(因为是common的)
		- 2. 使用C# script自定义组件
			
			- 只有这一种方式扩充组件？
			- 内置组件只是一个个C#脚本文件？
				- 使用MRTK-webrtc包，发现添加的组件其实是一个个C#脚本

### 内置游戏对象
- 使用 空对象 + 组件 -> 提前制作一些经常被复用的对象
#### 原始对象和占位对象
- Unity 可以使用通过建模软件创建的任何形状的 3D 模型。
- Unity内置了一些模拟简单形状的原始游戏对象
	- 即__立方体 (Cube)、球体 (Sphere)、胶囊体 (Capsule)、圆柱体 (Cylinder)、平面 (Plane)__ 和__四边形 (Quad)__。
		- 可以用来构建简单的形状
		- 也可用于快速创建__占位对象__和原型以便用于测试
### 自定义游戏对象
- 任意对象 = 空对象 + 组件

### 使用游戏对象

#### 停用游戏对(Deactivating GameObjects)
1. 可以通过将游戏对象标记为非活动来暂时从场景中移除此对象。
	- 1. 导航到 Inspector 并取消选中该游戏对象名称旁边的复选框(请参阅下图)![复选框]()
	- 2. 使用脚本中的 activeSelf 属性

2. 停用父游戏对象时，也会停用其所有子游戏对象。
	- 此停用会覆盖所有子游戏对象上的 activeSelf 设置，因此 Unity 会使父级下的整个层级视图将变为非活动状态。
	- 但，这不会更改子游戏对象上 activeSelf 属性的值，因此重新激活父对象时，子对象将恢复到其原始状态。
	- 这意味着无法通过读取 activeSelf 属性来确定子游戏对象当前是否在场景中处于活动状态。而应该使用 activeInHierarchy 属性，该属性将考虑父对象的覆盖效果。

3. 如果希望更改游戏对象的子游戏对象的 activeSelf 设置，但不更改父对象的设置，可以使用如下代码：
```
void DeactivateChildren(GameObject g, bool a) 
{
    g.activeSelf = a;
    
    foreach (Transform child in g.transform) 
    {
        DeactivateChildren(child.gameObject, a);
    }
}
```
### 标签 (Tag) 
#### 标签简介
- 标签是什么
	- 标签 (Tag) 是可分配给一个或多个__游戏对象__的参考词
		- 例如，可为玩家控制的角色定义“Player”标签，并为非玩家控制的角色定义“Enemy”标签。还可以使用“Collectable”标签定义玩家可在场景中收集的物品。到时候方便使用标签来对他们进行管理
- why need 标签
	- 标签有助于识别游戏对象以便于编写脚本。
		- 通过使用标签，不需要使用__拖放方式__手动将游戏对象添加到脚本的__公开属性__，因此可以节省在多个游戏对象中使用相同脚本代码的时间。
- 通过设置 GameObject.FindWithTag() 函数，可以查找包含所需标签的游戏对象
	- 例如下，该函数在具有“Respawn”标签的游戏对象位置实例化 respawnPrefab：
```
using UnityEngine;
using System.Collections;

public class Example : MonoBehaviour {
    public GameObject respawnPrefab;
    public GameObject respawn;
    void Start() {
    	//respawn是引用类型，如果没手动拖放建立引用(即没有给respawn赋一个对象的地址)，则初始化为null
        if (respawn == null)
            respawn = GameObject.FindWithTag("Respawn");
        
        Instantiate(respawnPrefab, respawn.transform.position, respawn.transform.rotation) as GameObject;
    }
}
```

- 只有__gameobject可以使用标签__？？组件可以使用标签来查找吗？？
	- 组件的inspector中没有这个框

- 每个gameobject只能与一个tag关联
	- 为什么gameobject不能与多个tag关联？有时一个物体是应该具有多个不同方面的 身份的，如：一个人又是学生、又是儿子、也是父亲、还是中国人
#### 创建新标签
- 1. 在inspector中创建
	- 在 Inspector 中，游戏对象的名称下面会显示 Tag 下拉菜单，![Tag下拉菜单](images/GOActiveBox1.png)
	- 要创建新标签，请选择 Add Tag…。随即在 Inspector 中打开标签和层管理器 (Tag and Layer Manager)。
	- 请注意：一旦命名了标签，以后就无法重命名。
- 2. 能否在C# script中创建？

#### 使用标签
- 1. 在inspector中设置使用tag
	- 在 Inspector 中，游戏对象的名称下面会显示 Tag 和 Layer 下拉菜单。要将现有标签应用于游戏对象，请打开 Tags 下拉选单，然后选择要应用的标签。游戏对象现在便与此标签关联。
- 2. 能否在C#脚本中设置？


### 静态游戏对象||动态游戏对象
- 是什么
	- 如果游戏对象__在运行时不发生移动__，则被称为静态游戏对象。如果游戏对象在运行时移动，则被称为动态游戏对象。
- why need 静态对象
	- 利用位置不变的特点来在 Editor 中预先计算来进行优化
		- 许多优化需要知道对象是否可在游戏过程中移动。有关静态（即非移动）对象的信息通常可在 Editor 中预先计算，因为此类对象不会因对象位置的变化而无效。
			- 例如，可以通过将多个静态对象组合成称为_批次_的单个大对象来优化渲染。
- 游戏对象的 Inspector 在右上角有一个 *Static* 复选框和菜单，用于向 Unity 中的各种不同系统告知该对象不会移动。
	- 对于每个系统，可以单独将对象标记为静态，因此可以选择在不能带来优势的情况下不计算对象的静态优化。


## 组件(Component)
### 组件简介
- 组件定义了游戏对象的行为
	- 没有组件的附加，游戏对象几乎什么都做不了
- 组件是灵魂核心，gameobject只是承载组件的躯壳
	- 内置的那些常用组件  only= 空游戏对象 + 组件的组合(由组件来定义他们是什么)
	- 内置的那些组件也只是一个个脚本？
		- unity一切的本质是C#脚本？？
### 内置组件

#### Transform组件
1. 游戏对象始终附加一个变换组件（表示位置和方向），并且无法删除此组件
2. 此组件定义游戏对象在游戏世界和 Scene 视图中的位置、旋转和缩放
3. Transform 组件支持__父子化__的概念
	- 可以使某个游戏对象成为另一个游戏对象的子代，并通过父代的 Transform 组件控制子代的位置。
	- 父子化关联是什么
		- __全局绝对__和__局部相对__的关系
		- 子对象的transform上的坐标是相对于父对象的位置坐标(在父对象的局部坐标系下的)，rotation,scale是怎样被局部相对的？？
		- 
	- why need 父子化关联？
		- 因为实际生活中的对象(物体)，实际上是存在亲子的这种抽象关系的，也就是说父子关系是对现实生活中的抽象关系本身的抽象
			- why unity 不对__兄弟关系__进行抽象？？？
		- 使用父子关系，可以方便的一个父亲对多个儿子进行管理
	- 什么情况应该建立父子联系？
		- 1. 需要对多个同级对象进行统一管理时，如: 排序
	- 子对象的__局部坐标__与__全局坐标__的转换
		- 通常使用子对象的局部坐标就足够了，但在游戏中通常需要找到这些对象在世界空间或__全局坐标__中的确切位置。变换组件的脚本 API 具有局部和全局位置、旋转和缩放的单独属性，还允许在局部和全局坐标之间转换任何点。
4. 使用transform组件注意事项
	- 在设置变换组件的父子关系时，一种有用的做法是在添加子项之前将父项的位置设置为 <0,0,0>。
		- 这意味着子项的局部坐标将与全局坐标相同，因此更容易确保子项处于正确位置。
	- __粒子系统__不受变换组件的__缩放比例__所影响。
		- 为了缩放粒子系统，需要修改系统的粒子发射器、动画器和渲染器中的属性。
	- 如果使用__刚体__进行物理模拟，请务必阅读刚体组件参考页面上的 Scale 属性。
	- 可通过偏好设置（菜单：__Unity > Preferences__，然后选择 Colors & keys 面板）更改变换轴（和其他 UI 元素）的颜色。
	- 更改缩放比例会影响子项transform组件的位置。例如，将父项的缩放比例调整到 (0,0,0) 将使所有子项相对于父项位于 (0,0,0) 位置。

##### Unity 中的旋转和方向
- 3D 应用程序中的旋转通常以两种方式之一表示：四元数或欧拉角。每种方式都有自己的用途和缺点。
	- 欧拉角:
		- 优点：
			- 1. 欧拉角具有直观的“可读”格式，由三个角度组成
			- 2. 欧拉角可表示通过大于 180 度转向从一个方向到另一个方向的旋转
		- 缺点：
			- 欧拉角受到万向锁 (Gimbal Lock) 的影响
	- 四元数：
		- 优点：
			
			- 四元数旋转不受万向锁的影响。
		- 缺点：
			- 1. 单个四元数不能表示任何方向超过 180 度的旋转
				- 
			- 2. 四元数的数字表示在直观上难以理解
			- 这些数字不代表角度或轴，您通常不需要直接访问它们
	
- unity结合使用两种方式的优点：在内部使用四元数表示，但在 Inspector 中显示等效的欧拉角值以便于进行编辑。
	- 为了便于理解，在Transform Inspector 中会使用欧拉角显示旋转
		- Unity 将 Inspector 中输入的用于旋转游戏对象的新值转换为该游戏对象的新四元数旋转值。
	- 为了不受万向锁影响，Unity 在内部将所有游戏对象的旋转存储为四元数，因为这种表示方式的好处超过了局限性。

- __旋转插值__
	- 在 Unity 自己的动画窗口中，有一些选项允许指定如何进行旋转插值：使用__四元数插值__还是__欧拉插值__
		- 欧拉插值：
			- 通过指定欧拉插值，即告诉 Unity 您希望使用角度指定全范围运动
		- 四元数插值：
			- 但是，使用四元数旋转，即表示仅希望旋转以特定方向结束，因此 Unity 会使用四元数插值并在__最短距离内__旋转到达该位置

#### Main Camera 游戏对象组件

#### 光源组件(light)
- 是什么||why need light
	- 网格和纹理定义了场景的形状和外观，光源定义了 3D 环境的颜色和氛围

- 添加光源
	- 使用GameObject添加：
		- 本质上光源对象只是提前给设置好组件了
	- 使用组件方式添加：
		- 可使用 Component > Rendering > Light 将光源 (Light) 组件添加到任何选定的游戏对象




### 自定义组件
1. 只有C#脚本一种创建组件的方式？？

从技术方面来说，编写的任何脚本都会编译为__组件__类型，因此 Unity Editor 会将脚本视为内置组件。可以定义要在 Inspector 中公开的脚本成员，并且 Editor 会执行您编写的任何功能。

#### 使用Script创建组件

### 使用组件
- 组件本身是对行为(虚的)的抽象，不能单独使用，只能附加在游戏对象上来使用
#### 游戏对象上的组件是如何工作的
#### 组件间的依赖关系
#### 与组件交互






## 3. 预制件(prefabs)
### prefabs简介
- 是什么
	- Unity 的预制件系统允许创建、配置和存储__游戏对象及其所有组件、属性值和子游戏对象__作为__可重用资源__。
	- 预制件资源充当__模板__，在此模板的基础之上可以在场景中创建新的__预制件实例__。 
		- 基于__预制件资源__可以创建任意数量的__预制件实例__
- why need 预制件
	- 一种更好的__同步-复用__的方式
		- 1. 预制件系统可以自动保持所有副本同步，一处改动，全部更新
			- 例如，如果要在场景中的多个位置或项目中的多个场景之间重用以特定方式配置的游戏对象，比如非玩家角色 (NPC)、道具或景物，则应将此游戏对象转换为预制件。使用这种方式比简单复制和粘贴游戏对象更好(这种不会进行同步)。
		- 2. 对预制件资源所做的任何编辑都会自动反映在该预制件的所有实例
			- 因此，只需要在预制件资源里进行改动即可
		- 3. 这并不意味着所有预制件实例都必须完全相同，也可以用于需要不同的情况
			- 如果希望预制件的某些实例与其他实例不同，则可以覆盖各个预制件实例的设置。
			- 还可以创建预制件的变体，从而将一系列覆盖组合在一起成为有意义的预制件变化。

- 如果游戏对象在一开始不存在于场景中，而希望在运行时实例化游戏对象（例如，使能量块、特效、飞弹或 NPC 在游戏过程中的正确时间点出现），那么应该使用预制件。
	
	- 好像是可以加快游戏对象构建的时间？ 预制件是不是也提前优化了一部分？

### 创建prefabs
#### 由gameobject -> prefabs
- 创建预制件资源极其简单，将一个游戏对象从 Hierarchy 窗口拖入 Project 窗口，即完成了创建
	- 该游戏对象及其所有组件和子游戏对象在 Project 窗口中成为新的预制件资源
	- 创建预制件资源的这一过程也会将原始游戏对象转换为预制件实例
	- 创建完成后，颜色上会有区分
		- 预制件实例以蓝色文本显示在 Hierarchy 窗口中，预制件的根游戏对象显示为蓝色立方体预制件图标
#### prefabs -> 预制件实例
- 可通过将预制件资源从 Project 视图拖动到 Hierarchy 或 Scene 视图，在 Editor 中创建预制件资源的实例
- 还可以使用脚本在运行时创建预制件的实例
#### 替换现有预制件




## 4. 层(layer)
- 是什么
	- unity中的层like ps中的层一样是一种粒度上的划分(通过抽象出一个更细粒度的中间层)，可将同一个scene中的gameobjects置于不同的层，来设置哪些游戏对象之间可以相互作用、哪些游戏对象是不相关的
		- 相机最常使用它们来渲染场景的一部分，灯光通常用它们来照明场景的一部分
		- 位于同一层的可以相互影响？不同层的相互无关？
- why need 层
	- 1. 

- 注意：每个GameObject只能分配一层。

### 层的实际使用

- 1. 第一步是创建一个新层，随后我们可以将这个层分配给__游戏对象__
	- 打开 Tags and Layers 窗口（主菜单：Edit > Project Settings，然后选择 Tags and Layers 类别）<img src="images/Layer-CreateNewLayer.png" style="zoom:100%;" />
	- 我们可以在某个空用户层中创建一个新层。

- 2. 现在可以将该层分配给一个或多个GameObjects。 
	- 


## 5. 显示屏(display)
- __UI对象__和__普通游戏对象__在显示屏上显示时走的是两个通道。
	- 无论UI元素位于的canvas的位置是位于什么地方，canvas都会自适应的投影到某一display上(某一个显示屏上).
		- canvs区域内的的ui元素才会投影，区域外的不进行投影；有点像 普通对象之于camera
		- 具体投到哪个display上(即投到哪个显示屏上)在canvas中设置的
	- 但是普通游戏游戏对象只有位于某一camera的roi下才会经过camera投到某一display上
		- 具体投到哪个display上(即投到哪个显示屏上)在camera中设置

- 是什么
- why need display
	- 有时我们有多个显示屏同时显示的需求



## 6. 约束

