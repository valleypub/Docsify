[toc]

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