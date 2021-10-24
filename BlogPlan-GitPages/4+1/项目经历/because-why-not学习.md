[toc]


# callscene场景的学习
1. 同一个个canvas上如何实现多个用户选择界面？
- panel设置不透明度+canvas上同一层级的渲染顺序特点

2. Asset中的一个脚本文件 == 一个声明的类类型，将脚本挂载到游戏对象上 == 对类进行实例化。
3. 挂载在游戏对象上的脚本 和游戏对象上的Tranform这样的组件一样
	- 可以使用GetComponet<>()来向获取游戏对象上Transfoorm组件一样获取游戏对象上的脚本组件，如：
		- ```GetComponet<Transform>()```  ```GetComponet<PPTUpDown>()```
	- __注意：__在脚本中使用```GetComponet<Transform>()``` == ```this.GetComponet<Transform>()```，__其中__脚本中使用的this指的是脚本所挂载在的游戏对象
		- 这就是为什么，可以在脚本A中使用GetComponet<脚本B>()来获取和脚本A挂载在同一游戏对象的同一级别的脚本组件

4. 任意游戏对象A上的任意组件(如：Transform组件 、自定义脚本组件 、)均可以通过gameObject字段来获取他所附加在的游戏对象。这样就形成了双向指向：游戏对象A可以找到他上面的所有组件，他的每一个组件也都可以找到他(游戏对象A)，这一点很有用，如：
	- 使用挂载在游戏对象A上的脚本来控制游戏对象A的Active



### Unity下的特殊类的学习
5.  PlayerPrefs类的使用
	- 一般PlayerPrefs类主要就是当作一个存储的查找表来用的，有点像一个缓存字典(由一个个键值对组成)
		- ==PlayerPrefs底层由什么数据结构实现的==
	- 使用一般就是2步：1.存键值对(set)，2.取键对应的值(查找)  3. 删除键值对
	- PlayerPrefs.GetString非null判断直接换为了 PlayerPrefs.GetString(Key，为null时使用的替代值)
	- 可以封装PlayerPrefs提供的底层SetString GetString SetInt GetInt，来实现我们需要的字符串变量缓存系统，如下：实现了：SaveSettings  LoadSettings  ResetSettings 

```c#
//PlayerPrefs.SetInt(Key,（int）Value)
 private static void PlayerPrefsSetBool(string name, bool value)
    {
        PlayerPrefs.SetInt(name, value ? 1 : 0);
    }
    
// PlayerPrefs.GetString(Key,(string)Value)

//PlayerPrefs.DeleteKey(Key)

///<summary>
///一般PlayerPrefs类主要就是当作一个存储的查找表来用的：一般涉及：1.存(set)，2.取(查找) 3. 重置
///</summary>

    private void SaveSettings()
    {
        PlayerPrefsSetBool(mPrefix + PREF_AUDIO, uAudioToggle.isOn);
        PlayerPrefsSetBool(mPrefix + PREF_VIDEO, uVideoToggle.isOn);
        PlayerPrefs.SetString(mPrefix + PREF_VIDEODEVICE, GetSelectedVideoDevice());
        PlayerPrefs.SetString(mPrefix + PREF_ROOMNAME, uRoomNameInputField.text);
        PlayerPrefs.SetString(mPrefix + PREF_IDEALWIDTH, uIdealWidth.text);
        PlayerPrefs.SetString(mPrefix + PREF_IDEALHEIGHT, uIdealHeight.text);
        PlayerPrefs.SetString(mPrefix + PREF_IDEALFPS, uIdealFps.text);
        PlayerPrefsSetBool(mPrefix + PREF_REJOIN, uRejoinToggle.isOn);
        PlayerPrefsSetBool(mPrefix + PREF_LOCALVIDEO, uLocalVideoToggle.isOn);
        PlayerPrefs.SetInt(mPrefix + PREF_FORMAT, uFormatDropdown.value);

        PlayerPrefs.Save();
    }

	private void LoadSettings()
    {
        uAudioToggle.isOn = PlayerPrefsGetBool(mPrefix + PREF_AUDIO, true);
        uVideoToggle.isOn = PlayerPrefsGetBool(mPrefix + PREF_VIDEO, true);
        //can't select this immediately because we don't know if it is valid yet
        mStoredVideoDevice = PlayerPrefs.GetString(mPrefix + PREF_VIDEODEVICE, null);
        uRoomNameInputField.text = PlayerPrefs.GetString(mPrefix + PREF_ROOMNAME, Application.productName + "_address");
        uIdealWidth.text = PlayerPrefs.GetString(mPrefix + PREF_IDEALWIDTH, "320");
        uIdealHeight.text = PlayerPrefs.GetString(mPrefix + PREF_IDEALHEIGHT, "240");
        uIdealFps.text = PlayerPrefs.GetString(mPrefix + PREF_IDEALFPS, "30");
        uRejoinToggle.isOn = PlayerPrefsGetBool(mPrefix + PREF_REJOIN, false);
        uLocalVideoToggle.isOn = PlayerPrefsGetBool(mPrefix + PREF_LOCALVIDEO, true);
        uFormatDropdown.value = PlayerPrefs.GetInt(mPrefix + PREF_FORMAT, 0);

    }

	public void ResetSettings()
    {
        //将各个键的值设为初始值
        PlayerPrefs.DeleteKey(mPrefix + PREF_AUDIO);
        PlayerPrefs.DeleteKey(mPrefix + PREF_VIDEO);
        PlayerPrefs.DeleteKey(mPrefix + PREF_VIDEODEVICE);
        PlayerPrefs.DeleteKey(mPrefix + PREF_ROOMNAME);
        PlayerPrefs.DeleteKey(mPrefix + PREF_IDEALWIDTH);
        PlayerPrefs.DeleteKey(mPrefix + PREF_IDEALHEIGHT);
        PlayerPrefs.DeleteKey(mPrefix + PREF_IDEALFPS);
        PlayerPrefs.DeleteKey(mPrefix + PREF_FORMAT);
        PlayerPrefs.DeleteKey(mPrefix + PREF_REJOIN);
        PlayerPrefs.DeleteKey(mPrefix + PREF_LOCALVIDEO);
        //再当下的设置
        LoadSettings();
        CheckSettings();
    }

    
```


6. Unity脚本内使用Application类，Application类的几个字段对于脚本编写很有用，如：
	- Application.platform
	- Application.unityVersion
	- Application.companyName
	- Application.productName
	- Application.dataPath
	- Application.streamingAssetsPath
	- Application.persistentDataPath
	- [Application官方文档](https://docs.unity.cn/cn/2019.4/ScriptReference/Application.html)
```
    Debug.Log("platform is " + Application.platform);
    Debug.Log("dataPath is " + Application.dataPath);
    Debug.Log("streamingAssetsPath is " + Application.streamingAssetsPath);
    Debug.Log("persistentDataPath is " + Application.persistentDataPath);
    Debug.Log("unityVersion is " + Application.unityVersion);
    Debug.Log("productName is " + Application.productName);
    Debug.Log("companyName is " + Application.companyName);
    Debug.Log("platform is " + Application.persistentDataPath);
      
```

7. Unity的几个特殊的目录，有的目录编辑器Editor模式下可用，但是打包成程序exe后却消失了，
	- Editor模式下能用的：
	- 打包后也能用的: Resources、streamingAssets、Plugins，Assets，这几个文件夹在原始工程中 -> 打包后依然会存在，且打包时分别有各自的特点
		- Resources: 无论多少个叫Resources的文件夹都可以。Resources文件夹下的资源不管你用还是不用都会被打包进来
		- Plugins: 是怎么打包的？？是只选择一部分打包进去吗？？选择的哪一部分？？明显感觉到打包后的文件比原工程中的Plugins中的文件少了好多

8. 为什么使用Debug.Log("streamingAssetsPath is " + Application.streamingAssetsPath);输出是platform is C:/Learning/Unity/unity-project/BecauseWhyNot/Assets/StreamingAssets 但是我进入工程目录发现Asset下并没有StreamingAssets？？？
	- ==Application.streamingAssetsPath只提供文件夹路径(即，只是一个字符串)，StreamingAssets不会是要我们自己在Assets下创建的吧？？？==
		- 是的，一些重要的文件夹都是要我们自己创建的：Resources 、StreamingAssets 、Editor。而且最有趣的是，Resources 可以创建多个，位置也任意，Resources文件夹下的资源不管你用还是不用都会被打包进.apk或者.ipa
	- 如果程序运行期间使用了Application.streamingAssetsPath，但是StreamingAssets文件夹没有手动创建怎么办？？
	- ==StreamingAssets是只读的(运行期间只读的？？)，我们只能提前将文件放进StreamingAssets下，在程序运行时在动态的从StreamingAssets下读取？？？？==
	- ==StreamingAssets下的资源读取(动态加载)也不是随意的，请使用 UnityWebRequest 类来访问资源==，如下面的加载方式：

```



```


9. ~~使用Resources文件夹 + 使用Resources.Load()来运行时动态加载文件时发现，本机的Resources和Unity里的Resources是不同步的，具体表现是：1. 一般的Assets文件夹，将文件拖进本机的Assets目录下，Unity中的Assets目录下也会出现拖进的文件，而将文件拖进本机的Assets下的Resources目录并不会出现在Unity中的Assets下的Resources目录下，将文件拖进Unity中的Assets下的Resources目录下也不会出现在本机的Assets下的Resources目录下。2. 使用Resources.Load()只能动态读取拖进Unity中的Assets下的Resources目录下的文件，而不能读取本机的Assets下的Resources目录下的文件。==但是，使用WebRequest却可以读取本机的~~
	- 我智障了，Resources是同步的，我之前是工程开错了，将fbx文件拖进工程A的Resources文件夹，当然不会出现在工程B的Unity的Resources文件夹下了。同一个工程肯定是实时同步的


### Unity各种特殊文件夹的使用学习

1. 有哪些特殊文件夹
	- Resources
	- streamingAssets
	- Editor
	- Assets
	
2. 这些文件夹的打包前后的文件内容、使用等特点
	- 
2. 这些文件夹可能是需要我们自己创建的，通过手动或在脚本中创建

3. 这些文件夹存在的目的不同，即面向的任务是不一样的（面向的任务(使用场景)的不同特点 -> 这些文件夹各自不同的特点）
	- Resources一般面向的任务是
		- Resources的特点是：
			- 可以在任意地方同名的多个文件夹
			- 打包的时候不管Resources里的文件用没用到会全部打包（win下：是全部打包进一个Resources文件夹下）
			- 可读写。
			- 动态读写时，请使用Resources.Load()
				- 动态读取时是在打包后的工程中的Resources文件夹下顺序遍历的吗？？？
	- StreamingAssets一般面向的任务是
		- StreamingAssets的特点：
			- StreamingAssets只能有一个，那就是在Assets/StreamingAssets目录，因为使用时一般通过Application.streamingAssetsPath(只是一个字符串，这个字符串不会变，没创建StreamingAssets时他就存在了)来访问的
			- 打包时的规律：
				- ==程开发阶段放进Asets/streamingAssets文件夹内的文件会原封不动的打包进打包后工程的streamingAssets文件夹内，哪怕这个文件压根就没用到。== Assets Resources Plugins均没有这个特点
					- 
			- 只读。且请使用WebRequest来进行动态文件加载

4. 一般只用作动态加载时，使用streamingAssets文件夹最好，因为在工程开发阶段放进Asets/streamingAssets文件夹内的文件会原封不动的打包进打包后工程的streamingAssets文件夹内，哪怕这个文件压根就没用到。而且也能通过Application.streamingAssetsPath来读取。==相比之下，Resources Plugins都会在打包时进行一些处理。==

5. Asets/streamingAssets文件夹 和 Assets文件夹有什么区别？？可以使用Assets文件夹(对应Application.dataPath)来替代Asets/streamingAssets文件夹作为存放动态加载文件的文件夹？？？
	- 可以。
	- Asets/streamingAssets文件夹 和 Assets文件夹的区别是:==打包时的区别==
		- Asets/streamingAssets文件夹下的所有文件会自动全部复制进打包后的/streamingAssets文件夹下
		- 但是,Assets文件夹下的文件不会自动复制进xxx_Data文件夹下，但是，我们手动复制进来后，也能达到和使用Asets/sngAssets文件夹一样的效果