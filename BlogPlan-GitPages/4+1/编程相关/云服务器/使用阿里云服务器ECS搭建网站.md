[toc]



## 网站服务器架构
https://zhuanlan.zhihu.com/p/43806635

- 服务器硬件上安装的 lamp lnmp 等都是什么，结合网站服务器架构想想为什么需要使用他们？？
- lamplamp(linux + __apache__ + mysql +php) 还是 lnmp(linux + __nginx__ + mysql + php)
	- 下面是几点：
		- 要省内存的话lnmp是最好的选择,但似乎不太稳定,有时会比较常502
		- 目前很多网站都开始用Nginx了，并发数要好一些，淘宝网甚至根据Nginx专门制作了一个开源项目Tengine
		- 每种语言都有最好的固定搭档的，是经过市场考验的
			- JSP最好的组合就是j2EE+Tomcat+mysql
			- linux + __apache__ + mysql +php
			- linux + __nginx__ + mysql + php

- php是什么？？为什么web环境要考虑php


- java环境 php环境 js环境(nodejs等) 的区别是什么
	- 任务领域(服务器领域、浏览器领域) -> 开发语言(java php javascript) -> 运行环境(tomcat     nodejs)


- 服务器架构是通用的(https://zhuanlan.zhihu.com/p/43806635)，但是具体的每一部分的实现可以是多样的：
	- 应用服务器：
		- php服务器
		- apache tomcat服务器
		- nodejs
	- 数据库相关：
		- mySQL
		- redis
	- 文件
	- 可以自由的进行组合，当然，也有一些经过实践检验的classic组合：LNMP LAMP 


## 问题
- wordPress是什么，WordPress主要是简化了哪一部分的工作？？如果没有WordPress我们该怎么做
- WordPress 宝塔建站 等的区别是什么？？

## 实战
### 使用ECS快速搭建云上博客
本教程使用Apache作为后端服务器，并在云服务器上创建一个MySQL数据库用来存储数据。
#### 登陆云服务器
#### 配置环境
##### 配置Apache
##### 配置MySQL
1. 下载|安装MySQL
wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql-community-server
2. 启动MySQL
systemctl start mysqld.service
3. 查看MySQL运行状态
systemctl status mysqld.service
4. 查看MySQL初始密码
grep "password" /var/log/mysqld.log
5. 修改MySQL密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Kang.81163';
6. 登录数据库
mysql -uroot -p


##### 配置PHP
WordPress是使用PHP语言开发的博客平台。参考以下操作安装PHP

1. 安装php
yum -y install php php-mysql gd php-gd gd-devel php-xml php-common php-mbstring php-ldap php-pear php-xmlrpc php-imap
2. 创建php测试页面
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php

3. 重启Apache服务
systemctl restart httpd

4. 访问测试
打开浏览器，访问http://47.98.187.186/phpinfo.php ，显示如下页面表示PHP安装成功。
<img src="C:\Users\king-kong\Desktop\BlogPlan\picture\服务器\php成功输出.PNG" alt="tu" style="zoom:50%;" />

##### 配置WordPress

##### 发布Blog