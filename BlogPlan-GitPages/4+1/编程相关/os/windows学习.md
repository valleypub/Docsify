[toc]


### 注册表是什么？
- 是什么
	- 是一个数据库，管理配置系统运行参数的核心数据库



### NTFS
https://docs.microsoft.com/zh-cn/windows-server/storage/file-server/ntfs-overview

### SMB
https://docs.microsoft.com/zh-cn/windows-server/storage/file-server/file-server-smb-overview




## cmd下常用的exe应用

### 端口查询相关
1. netstat -ano	
	- 列出所有端口的情况
	- 可以看到本机网卡的内网ip和NAT对应的外网IP

2. netstat -aon|findstr "端口"
	- 查看具体被占用的端口。ru:netstat -aon|findstr 80