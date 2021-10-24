[toc]


# bug

1. 通过使用subst可以解决 电脑原先有E盘+初次安装node.js时设置了E盘 -> 后续运行node-v14.17.5-x64.msi时会报invalid Driver E的问题，此时，使用subst 设置虚拟盘符可以解决
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\dos\invalidDriveD问题.PNG" alt="invalidE的问题" style="zoom:60%;" />
	- 解决方案：
	- subst E: %TEMP%    //建立虚拟盘符映射
	- 再次运行node-v14.17.5-x64.msi手动更改安装目录为C盘下
	- subst E: /d		//解除虚拟盘符映射
- 但是，明明没有E盘，为啥会出这个问题？？
