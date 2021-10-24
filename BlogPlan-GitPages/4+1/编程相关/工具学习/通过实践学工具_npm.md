[toc]


- 是什么？


- 为什么有的包(软件，如：docsify)可以使用npm来进行安装？？


- 如何查看npm将包 下载-安装的位置
	- 全局安装查询：
		- npm root -g


- npm下载这些东西，不会对各软件进行独立的划分，而是一股脑地全部存在 C:\Learning\Node.js\node_modules\npm\node_modules这个文件夹下？？？？如：全局安装docsify，会将docsify中的color模块直接在C:\Learning\Node.js\node_modules\npm\node_modules下？？？

# npm
- 是什么
	- 全称是Node Package Manager，一个拥有三大美德的程序员 Isaac Z. Schlueter用 JavaScript （运行在 Node.js 上）写的一个包依赖集中管理工具。用来解决：当依赖的包太多，需要跑到不同的网站上去下载各种软件的问题。
		- 程序员的三大美德：
			- 懒惰：是这样一种品质，它使得你花大力气去避免消耗过多的精力。它敦促你写出节省体力的程序，同时别人也能利用它们。为此你会写出完善的文档，以免别人问你太多问题。
			- 急躁：是这样一种愤怒----当你发现计算机懒洋洋地不给出结果。于是你写出更优秀的代码，能尽快真正的解决问题。至少看上去是这样。
			- 傲慢：极度的自信，使你有信心写出（或维护）别人挑不出毛病的程序。



- why need it


- npm工作机理
	1. 买个服务器作为代码仓库（registry），在里面放所有需要被共享的代码
	2. 发邮件通知 jQuery、Bootstrap、Underscore 作者使用 npm publish 把代码提交到 registry 上，分别取名 jquery、bootstrap 和 underscore（注意大小写）
	3. 社区里的其他人如果想使用这些代码，就把 jquery、bootstrap 和 underscore 写到 package.json 里，然后运行 npm install ，npm 就会帮他们下载代码
	4. 下载完的代码出现在 node_modules 目录里，可以随意使用了。
	- 这些可以被使用的代码被叫做「包」（package），这就是 NPM 名字的由来：Node Package(包) Manager(管理器)。



- 参考的网络文档
	- https://zhuanlan.zhihu.com/p/24357770


