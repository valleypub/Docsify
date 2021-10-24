[toc]



## 前言

- 研究一下粒子系统的渲染的本质
- 以脚本方式使用 cpu粒子系统(particle system)   gpu粒子系统(Visual Effect Graph)的经典模式
	- ParticleSystem API来使用C#脚本高度自定义粒子系统

- unity提供两种粒子系统方案，根据需求来选择最适合的：
	- ![两种粒子系统解决方案的概要对比情况](C:\Users\king-kong\Desktop\要做的事情\picture\unity\2种粒子系统的对比图.PNG)




- StandardAssets要自己安装才能使用，比如：一些material 
https://assetstore.unity.com/packages/essentials/asset-packs/standard-assets-for-unity-2018-4-32351?_ga=2.31862781.256443471.1627004494-44388462.1603200264&_gl=1*1glew5i*_ga*NDQzODg0NjIuMTYwMzIwMDI2NA..*_ga_1S78EFL1W5*MTYyNzAwNDQ5NC4yMy4xLjE2MjcwMTExMDUuMA..

## Particle System
- cpu版的
	- 内置粒子系统在 CPU 上模拟粒子行为
- cpu版的优点
	- 可以使用 C# 脚本与系统及其中的各个粒子进行交互
	- 粒子系统可以使用 Unity 的基础物理系统，从而与场景中的碰撞体进行交互
	- 结构简单
		- 每个粒子系统抽象成一个 particle system组件，对particle system组件进行设置来实现想要的粒子效果
			- 使用C#脚本方式
			- 使用inspector进行设置


### 脚本方式使用Particle System

## Visual Effect Graph
- gpu版的
- 是什么
	- is __a Unity package__ that uses a Scriptable Render Pipeline to render visual effects. 
- why need it

### how to use it 
#### requirement
##### Unity Editor版本 与 Visual Effect Graph包版本药兼容
![]()
##### Render pipeline 与  Visual Effect Graph包版本 要兼容

- Every Visual Effect Graph package works with a Scriptable Render Pipeline package of the same version. If you want to upgrade the Visual Effect Graph package, you must also upgrade the render pipeline package that you’re using.
	- For example, the Visual Effect Graph package version 6.5.3-preview in Package Manager works with the High Definition RP package version 6.5.3-preview.


- 渲染管线上
	- HDRP
		- The Visual Effect Graph supports every platform that HDRP supports.
		- 
		- __Note__: When you download the HDRP package from the Package Manager, Unity automatically installs the Visual Effect Graph package.
	- URP
		- 从2019.3版本开始支持urp方式的
		- it is not yet out of preview for URP, which means it only supports a subset of platforms that URP supports
		- It also does not support every feature that it does with HDRP, and also only supports unlit particles

##### 

#### install
#### create - Creating Visual Effect Graphs Assets
##### Visual Effect Graphs Assets概述
- 是什么
	- 


#### use - Using Visual Effect Graphs in Scenes
- 要想使用visual effect graph 首先要将上步创建的asset加入scene，2种加入方式
	- 1. 从asset栏drag into Hierarchy Window栏
		- 1. 可以不指定对象的直接拖进去，会自动新建一个对象
		- 2. 不能以拖动的方式直接将visual effect资源添加到已存在的对象上，但可以在已存在的对象上使用add component -> effect -> visual effect来添加这个组件
	- 2. 从Project Window栏drag into Scene View Window栏 -> 会自动在Hieraty栏中生成一个对象，这个对象上带有visual Effect组件

- 这一步相当于将visual effect asset与gameObject进行了关联绑定，后面我们只需要更改visual effect asset，即可将更改应用到所有的关联的游戏对象上
#### edit
#### preview - Previewing a graph’s effect

### 以脚本的方式使用 visual effect graph

### 以可视化编程的方式使用 visual effect graph



## 在一个unity工程中使用visual effect graph功能的完整过程
1. 确保要部署的硬件平台支持vfx
2. 选择兼容的链：visual effect graph包版本|unityEditor版本|渲染管线版本
3. install
4. 



## 疑惑
1. visual effect graph | visual effect graph asset | visual effect graph window | visual effect component 几个概念究竟是什么
	- visual effect graph asset可以drag into visual effect component的Asset Template引用栏

2. 渲染管线究竟是什么
	- why 在总工程中引入 vfx后，由于更改了hdrp使原先的渲染图片出现了问题


## 问题
1. 在总工程中引入 vfx后，由于更改了hdrp使原先的渲染图片出现了问题