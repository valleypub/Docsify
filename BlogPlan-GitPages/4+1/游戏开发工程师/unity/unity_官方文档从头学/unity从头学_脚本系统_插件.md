[toc]

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


