[toc]






##### HTTP/2 -> HTTP/3

- HTTP/2的缺点：
	1. 因为丢失-重传 -> all http任务队头阻塞
	2. TCP和TLS的握手时延
	3. 网络迁移需要重新连接，而UDP是无连接的

