[toc]


- 是什么


- why need 协程
	- 有些指令我们将它们组织在一个方法内，但是不想要一镜到底的依次执行完，而是想要根据外部的每一update()帧来执行一条指令、并记住此次执行到的位置。
		- 如：
			1. 假设需要逐渐减少对象的 Alpha（不透明度）值，直至对象变得完全不可见。
	- 普通方法(使用return返回的)如果放在update()中会一次性执行完，但是如果使用yield return ... + IEnumerator就可以将一个方法在每一次的update()中执行一部分就返回，剩下的在下一帧的update中执行，如下：
```

IEnumerator Fun(){

	//第一帧中执行的代码
	frameUpdate1CodeHere;
	yield return null; //此帧中在这里返回，后面的在下一次的Update中在继续
	
	//第二帧中执行的代码
	frameUpdate2CodeHere;
	yield return null; //此帧中在这里返回，后面的在下一次的Update中在继续
	//yield return new WaitForSecond(5) 和yield return null一样也是此帧执行到的位置和下一帧开始的位置？？只不过会多等个几秒再返回？？？

}

```


- 协程的声明
	- 在 C# 中，声明协程的方式如下：
		- yield return null 行是暂停执行并随后在下一帧恢复的点
		- 在 yield 语句之间可以正确保留任何变量或参数。
```
IEnumerator Fade() 
{
    for (float ft = 1f; ft >= 0; ft -= 0.1f) 
    {
        Color c = renderer.material.color;
        c.a = ft;
        renderer.material.color = c;
        yield return null;
    }
}
```



- 协程的使用
	- 要将协程设置为运行状态，必须使用 StartCoroutine 函数，如：
```
void Update()
{
    if (Input.GetKeyDown("f")) 
    {
        StartCoroutine("Fade");
    }
}
```



# 参考文档
1. https://blog.csdn.net/fdyshlk/article/details/72667814#:~:text=yield%20return,new%20WaitForSeconds%EF%BC%8C%E8%BF%99%E4%B8%AA%E8%A6%81%E6%B3%A8%E6%84%8F%E7%9A%84%E6%98%AF1%C2%B7%E5%AE%9E%E9%99%85%E6%97%B6%E9%97%B4%E7%AD%89%E4%BA%8E%E7%BB%99%E5%AE%9A%E7%9A%84%E6%97%B6%E9%97%B4%E4%B9%98%E4%BB%A5Time.timeScale%E7%9A%84%E5%80%BC%E3%80%82%202%C2%B7%E8%A7%A6%E5%8F%91%E9%97%B4%E9%9A%94%E4%B8%80%E5%AE%9A%E5%A4%A7%E7%AD%89%E4%BA%8E1%E4%B8%AD%E8%AE%A1%E7%AE%97%E5%87%BA%E7%9A%84%E5%AE%9E%E9%99%85%E6%97%B6%E9%97%B4%EF%BC%8C%E8%80%8C%E4%B8%94%E8%AF%AF%E5%B7%AE%E7%9A%84%E5%A4%A7%E5%B0%8F%E5%8F%96%E5%86%B3%E4%BA%8E%E5%B8%A7%E7%8E%87%EF%BC%8C%E5%9B%A0%E4%B8%BA%E5%AE%83%E6%98%AF%E5%9C%A8%E6%AF%8F%E5%B8%A7%E5%A4%84%E7%90%86%E5%8D%8F%E7%A8%8B%E7%9A%84%E6%97%B6%E5%80%99%E5%8E%BB%E8%AE%A1%E7%AE%97%E6%97%B6%E9%97%B4%E9%97%B4%E9%9A%94%E6%98%AF%E5%90%A6%E6%BB%A1%E8%B6%B3%E6%9D%A1%E4%BB%B6%EF%BC%8C%E5%A6%82%E6%9E%9C%E6%BB%A1%E8%B6%B3%E5%88%99%E7%BB%A7%E7%BB%AD%E6%89%A7%E8%A1%8C%E3%80%82


2. [协程-unity官方说明](https://docs.unity.cn/cn/2019.4/Manual/Coroutines.html)

3. [MonoBehaviour.StartCoroutine官方说明](https://docs.unity.cn/cn/2019.4/ScriptReference/MonoBehaviour.StartCoroutine.html)
4. [WaitForSeconds在协程中的应用](https://docs.unity.cn/cn/2019.4/ScriptReference/WaitForSeconds.html)