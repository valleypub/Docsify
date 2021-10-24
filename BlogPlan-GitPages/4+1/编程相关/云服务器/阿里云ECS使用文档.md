[toc]

[阿里云帮助中心-阿里云，领先的云计算服务提供商 (aliyun.com)](https://help.aliyun.com/product/25365.html?spm=a2c4g.11186623.6.540.219f2bb03VTArT)

## 1. 进入服务器

1. 登陆阿里云官网
https://cn.aliyun.com/

2. 进入控制台
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\控制台.PNG" alt="控制台" style="zoom:60%;" />
3. 进入ECS资源管理面板
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\ECS.PNG" alt="ecs" style="zoom:60%;" />
4. 进入实例
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\ECS\实例.PNG" alt="实例" style="zoom:60%;" />

## 2. 连接服务器
### 使用自带的Workbench远程连接

### 使用ssh进行远程连接
1. 打开cmd.exe
2. 检测是否windows已安装ssh，输入 ssh - V
	- 若显示下图，说明已安装ssh
		- ![]()
	- 如果未安装ssh，请先安装 [OpenSSH]()

3. 输入 ssh root@[ECS实例的公网IP]：如：ssh root@47.98.187.186
4. 输入 yes
