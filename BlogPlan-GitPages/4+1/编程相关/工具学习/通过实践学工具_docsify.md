[toc]


# Centos7下使用docsify

## 缺点
1. 有的Centos只有命令行，无法使用浏览器来渲染-测试生成的网站的效果
2. Cetos下安装-卸载个工具还是挺麻烦的
3. 




# windows下使用docsify

## docsify + Github
### 1. 安装nodejs
### 2. 安装docsify
### 3. 


## docsify + 云服务器


# bug
## windows安装docsify失败
1. windows下使用 npm i docsify-cli -g 全局安装 docsify 打印信息成功，但是输入：docsify -v会显示，未安装的指令。
	- 解决方式：
		1. 删除-重装：不行
			- 运行npm root -g，查看docsify-cli装哪了
			- C:\Users\king-kong\AppData\Roaming\npm\node_modules
			- 进入C:\Users\king-kong\AppData\Roaming\npm\node_modules删除下面的docsify目录
			- 重新运行npm i docsify-cli -g
		2. 重新安装NodeJs：可以
			1. 删除NodeJs
			2. 重新下载NodeJs
			3. 设置环境变量。查看 node -v ; npm -v 是否正确。如果正确，进行下一步
			4. 运行npm i docsify-cli -g
			5. 运行 docsify -v


## docsify全局安装失败
- Centos7 + 使用docsify官网的全局安装命令 ，安装的过程很顺利没有报错，但是一旦运行docsify -v ```-bash: docsify: command not found```
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\docsify_bug1.PNG" style="zoom:50%; float: center;" />
		- 上面的报错属于node的缺少依赖包，单独定点的装缺的那个包我不会，我只能试试重装node

- 解决方式：	
1. 使用 ln -s 建立软连接
	- 不行


2. 重装node
	1. 卸载node
		1. yum remove nodejs npm -y
		2. 手动删除残留
			- 
	2. 重装node
		- [centos7安装nodejs网址](https://www.cnblogs.com/vessel/p/7903626.html)
		- __注意__：要写出原先的node，包括所有的node符号软连接，不然新装的node设置完 vi /etc/profile后，使用 source /etc/profile会失败
	3. 重新全局安装docsify
		- npm i docsify-cli -g
	4. 问题解决
		- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\docsify_bug2.PNG" style="zoom:50%; float: center;" />
		- 发现：原先的docsify无法使用并不是nodejs缺少依赖包，而是原先的nodejs就没有安装正确



