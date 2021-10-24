[toc]



# Unity入门

1. 菜单栏 -> edit -> render setting 
	- 设置环境光(ambient light)
	- 设置fog
		- 雾效功能会对性能产生一定影响
		- 


2. Lightmap功能
	- 对静态模型进行处理
	- 无法对动态模型进行烘焙(预计算)
		- 取消了static选项的对象
	- 菜单栏 -> window -> render
		- 也可以直接在对象的inspector中
			- 勾选static选项 -> 在mesh render中就会出现lightmapping选项

3. LightProbe


4. Terrain地形系统
5. SkyBox天空盒
	- 制作自定义的skybox
		- 1. 在project视图中create -> Material -> shader -> skybox
			- skybox的种类有多种，如:6slided，通过6张图片来
	- 使用自定义的skybox
		- 将skybox Material 拖到MainCamera上，
			