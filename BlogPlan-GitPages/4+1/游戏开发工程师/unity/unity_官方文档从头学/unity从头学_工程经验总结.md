[toc]



# unity五种数据储存方法
## PlayerPrefs
- 是什么
- why need it


[官方说明](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html)

### PlayerPrefs数据存储在哪里?
- 在Mac OS X上存储在~/Library/PlayerPrefs文件夹，名为unity.[company name].[product name].plist,这里company和product名是在project Setting中设置的
- 在windows下，playerPrefs被存储在注册的HKCU\Software[company name][product name]键下，这里company和product名是在project setting中设置的。
- 在Android上，数据存储（持久化）在设备上。数据保存在SharedPreferences中。

### PlayerPrefs常见使用方式

1. 当作查找缓存表来使用？？
```
	//1.先查询是否已经有记录
if (PlayerPrefs.HasKey(kLastRemotePeerId))
{
	//2. 如果有记录，直接读取记录中的值
	RemotePeerId.text = PlayerPrefs.GetString(kLastRemotePeerId);
}
else {
	//3. 如果没有记录，将值写入记录，方便下次使用
	PlayerPrefs.SetString(kLastRemotePeerId, RemotePeerId.text);
	NodeDssSignaler.RemotePeerId = RemotePeerId.text;
}
```


# unity资源的常用导入方式
## unitypackage导入Asset
Asset -> 

## 本机文件导入Packages
### 压缩包
window -> package manage
```+``` -> add from tarball
### 文件夹
window -> package manage
```+``` -> add from disk
进入文件夹根目录的package.json，双击这个文件自动导入

### URL

## 使用Package Manage下载


