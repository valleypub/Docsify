[toc]


# 网络通信模型及分类
## 分散式||集中式||分布式系统
### 分散式

- 是什么
- why need it
	- 优点
		
	- 缺点
		1. 容易导致共享的不同用户之间的数据不一致性。
		2. 数据冗余。

### 集中式
- 是什么
	通过一台主计算机保存共享的全部数据

- why need it
	- 优点
		1. 减少了数据冗余
		2. 减少了共享数据的不一致性
	- 缺点
		1. 可靠性不行


### 分布式 = 分散式 + 集中式

- 是什么
	1. 资源透明提供给用户。
		用户在使用资源时不需要知道资源是本地的or远程的，对于远程资源也可向本地资源一样任意调用，但，计算机网络需要先知道资源的位置，与资源所在的主机建立连接后才能使用。
	2. 高度内聚性。

## C/S B/S P2P网络通信架构
C/S B/S是在分散式系统、集中式系统、分布式系统基础上发展出来的。
### C/S

![]()

- 是什么
	- 客户端:
		主要负责界面和处理业务逻辑，并为用户提供网络请求服务的接口，如：数据查询请求。
	- 服务器端：
		一般以数据处理能力较强的DBMS作为后台，负责接受和处理用户对服务的的请求，并将这些服务__透明的__提供给用户。
		透明的意思是：

- 优缺点
	- 优点：
		1. 技术成熟
		2. 响应速度快
		3. 可以充分利用两端的硬件环境的优势，将任务合理分配到客户端和服务器端来实现。
	- 缺点：
		1. 针对性开发，不能灵活变更，维护和管理难度大，不利于扩展。

- CS架构一般采用__两层结构__

- 可以使用多种协议来进行网络传输，如：
	- http
	- ftp
	- 


### B/S

- 是什么
	- 只需维护一个服务器，客户端由专门开发的程序转换为浏览器。B/S是随着Internet的兴起，对C/S的改进和优化。
	- 和C/S无本质区别，是C/S的一种特例。特殊在这个模型必须使用HTTP。
- 优缺点
	- 优点：
		1. 分布性强
		2. 共享性强
			- 一台计算机可以访问任意一个Web服务器，用户只需要知道服务器的网址即可。
		3. 开发简单
			- 不需要提供专门的客户端软件。服务器端软件也按照统一的http协议来编写
		4. 维护方便
		5. 可扩展性、高灵活
	- 缺点：
		1. 数据安全性
			- 解决方案：
				- https


- B/S采用的是__三层结构。
	- __在数据管理层(server)、用户界面层(Client、浏览器)之间加了一层，称为中间价(Middleware)。
	- 三层架构是伴随着中间件技术的成熟而兴起的，核心概念是：利用中间件将应用分别表示为界面层、业务逻辑层、数据存储层3个不同的处理层。
	- 中间价作为构造三层结构的基础平台，具有如下主要功能：
		1. 负责客户机与服务器之间的连接和通信
		2. 负责服务器和数据库之间的连接和通信
		3. 实现应用与数据库之间的高效连接。
		4. 具有中间价的三层结构在层与层之间相互独立，任一层的改变不会影响到其他层的功能。
		![三层结构]()


### P2P

- 是什么

- 优缺点
	- 优点：
	- 缺点：

# 网络程序通信机制
## 端口与套接字
### 端口
#### 物理端口
RJ45端口

SC端口


#### 逻辑端口(进程标识)

http--80端口

ftp--21端口

smtp -- 25端口



- 端口号的分配规则:
|端口号|功能|
|----|----|
|0|不使用，或作为特殊的使用|
|1~255|保留给特定服务|
|256~1023|保留给其他服务|
|1024~4999|可以用作任意客户的端口|
|5000~65535|可以用作用户的服务器端口|

### 套接字

- 是什么
	套接字是支持TCP/IP网络通信的基本操作单元，是不同主机间的进程进行双向通信的端点，使用套接字便于区分不同应用程序进程间的网络通信和连接。如图1-4所示，有三台建立了通信连接的主机。
	对通信的一对主机来说，套接字包括发送方IP、发送方端口号、接收方IP、接收方端口号、协议五部分。

- why neet 套接字
	- 套接字屏蔽了TCP/IP协议栈的复杂性，使得在网络编程者看来，两个网络进程间的通信实质上就是他们各自所绑定的套接字间的通信。即，套接字就是抽象出来的一层，用来帮助我们高效简单的使用TCP/IP协议栈。

- 套接字抽象层的工作步骤流程：
	![]()

## 基于套接字的网络进程通信机制



# C#网络开发基本类

## DNS类
- 是一个静态类



### 实战案例
1. 显示本机的IP地址、主机名等信息
![]()


## Ping相关类
### Ping类

### PingOptions类


### PingReply类


### 实战案例
1. 使用Ping PingReply PingOptions来检测目标主机是否可达
![]()


## Socket相关类

### 套接字和Socket类的关系
- 套接字是什么
	一个套接字既保存了__本机的IP地址和端口__，也保存了__对方主机的IP地址和端口__，同时还有__双方通信的协议信息__。

- Socket类是什么
	- Socket类是套接字的代码实现，套接字是一种抽象概念，需要借助来Socket类来实际实现
		- System.Net.Sockets命名空间提供了Socket类

- Socket通信模型
![]()


### 套接字类型和使用Socket实现
__套接字有三种类型：__
1. 流套接字
	- 用来实现TCP通信。提供了：__面向连接的__、__可靠的__、__数据无错的__、__无重复的__、__保证顺序的(收发的数据顺序相同)__数据传输服务。
2. 数据报套接字
	- 用来实现UDP通信，以独立的数据报形式发送数据。提供了：面向无连接的、不可靠的、可能有错的(直接接收端丢弃？)、可能重复的(直接丢不会重复？)、不保证顺序的(数据分片后到达时序不同？)
	- 优缺点：
		- 优点：
			1. 由于不需要建立连接，也不需要确认，所以传输速度更快。
			2. UDP有消息边界。UDP把上层应用程序交下来的报文添加首部后直接交给IP层，既不拆分，也不合并，这样就保留了这些报文的边界。所以在使用UDP时，无须考虑边界问题，因此UDP在使用上比TCP简单。__这些边界有啥用？？？__
			3. UDP可以一对多传输。由于UDP传输数据不需要建立连接，也不需要维持连接状态，所以一台服务器可以向多个客户机同时传递相同的消息。__利用UDP的广播和组播功能可以同时向网上的所有客户发送消息，这一点也比TCP方便。__
		- 缺点：


3. 原始套接字
	- 原始套接字用来实现IP数据包通信，用于直接访问协议的较低层，常用于侦听及分析数据包，广泛应用于高级网络编程，也是一种经常使用的黑客手段。



__套接字类型需要使用Socket来实际实现：__
1. Socket构造函数：
	- public Socket(__AddressFamily__ addressFamily, __SocketType__ socketType, __ProtocolType__ protocolType);
2. 各参数含义：
	- __addressFamily__：指网络类型，使用AddressFamily枚举指定Socket使用的寻址方案，常见的有：
		- AddressFamily.InterNetwork（表示IPv4的地址）
		- AddressFamily.InterNetmorkV6（表示IPv6的地址）。
	- __socketType__和__protocolType__：这两个枚举类型的参数必须对应，共同指明Socket使用哪种协议的哪种套接字。表2-5列出这两个参数的组合。
		<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\配套的.PNG" style="zoom:50%;" />	
3. 常用搭配：
	- 流套接字：
		- Socket socket=new 	Socket(AddressFamily.InterNetwork,SocketType.stream,ProtocolType.Tcp) 



### Socket类的介绍：
1. Socket类的__常用属性__
![](C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\Socket类的属性.PNG)
2. Socket类的__常用方法__
	- Bind()
		- 用于Socket与本地IP地址和端口号关联。
		- 一般客户端的都会自动选择一个ip + port，但是serer端需要手动指定ip + port。这样是有原因的。因为客户端(使用Connect())接入server时需要使用server端的ip+port，故我们需要在server端自己选择一组ip+port来使用并记录下来给client来接入server;而client却不需要知道自己本机构建socket使用的ip+port，因为在client接入server时，底层会自动地将client使用的ip+port告知server端（server端的accept()的返回值中会包含客户端的socket信息），来实现双方的连接建立。client是怎么告知server的？？？？
	- Listen()
		- 用于等待客户端发出连接请求，其中的backlog为用户的__最大连接数__，超过该参数值的其他客户不能与服务器进一步通信。
	- Accept()
		- 该方法__创建新的Socket (该套接字中既包含了本机的IP地址和端口号，也包含了客户端的IP地址和端口号。然后就可以利用此套接字与该客户端进行通信了)。__以处理连接请求。当程序执行到该方法时__会处于阻塞状态__，直到有新的客户机请求连接。该方法__返回包含客户端信息的套接字句柄__。
	- Connect()
		- 客户机独有。通过__输入远程设备的IPEndPoint对象(ip+port)__，建立于远程设备的连接。客户端与服务器端建立连接之前，系统不会执行Connect语句下面的语句，而是处于阻塞状态。
	- Send()和Receive()
		- 这两个方法在完成客户端的连接后，将数据发送到连接到的Socket上以及将数据从连接的Socket接收到缓冲区的指定位置。__当Receive方法没有可读的数据时，将一直处于阻塞状态。__
	- ShutDown()
	- Close()
		- 该方法关闭远程主机连接，并释放所有与Socket关联的资源。关闭后，Connected属性将设置为false。
		- 对于面向连接的协议，先调用Shutdown方法，再调用Close方法，以确保在已连接的套接字关闭之前，已发送和接收该套接字上的所有数据。



### 面向连接的套接字
#### 工作流程

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\有连接套接字工作流程.PNG" style="zoom:30%;" />

##### Connect时的三次握手
![]()

##### Close时的四次挥手
![]()

#### 实战
1. 客户端程序

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\有连接_client.PNG" style="zoom:33%;" />

2. 服务器端程序

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\有连接_server.PNG" style="zoom:33%;" />


### 无连接的套接字
#### 工作流程

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\无连接套接字工作流程.PNG" style="zoom:30%;" />


#### 实战
1. 接受端程序

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\无连接_接收端.PNG" style="zoom:33%;" />

2. 发送端程序

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\C#网络编程\无连接_发送端.PNG" style="zoom:33%;" />


## 数据流concept
- 是什么
	当通过网络传输数据，或对文件数据进行操作时，需要将数据转化为数据流的形式。数据流（stream）是对__串行传输的数据（以字节为单位）的一种抽象表示__，数据源可以是文件、外部设备、主存、网络套接字等。
- 数据流分为:
	- 文件流
	- 内存流
	- 网络流

### NetworkStream类（网络流）
__是什么__
1. NetworkStream类相当于在网络数据的源端和目的端之间架起了一个数据桥梁，使得读取和写入数据只针对这个通道进行。==但NetworkStream类只支持面向连接的套接字。==
	![]()


__why need 网络流？？__
1. socket不是有send 吗 为什么还要使用网络流

__网络流(NetworkStream类)收发数据流程__

![]()

__NetworkStream类常用属性和方法__

![]()


__NetworkStream类 + Socket__

__NetworkStream类 + TcpClient__


## 网络数据的编码与解码




### C#中的编码与解码类
#### Encoding类
__是什么__
1. Encoding类位于System.Text命名空间中，主要用于在不同的编码和Unicode之间进行转换。

__Encoding类常用的属性和方法__

![]()



__实例：unicode字符串转为UTF-8字符串__
```
string unicodeString="unicode字符串pi(\u03a0)";￼  

//Encoding不是静态类，需要实例化来使用
Encoding Unicode=Encoding.Unicode;￼     
Encoding utf8=Ecoding.UTF8;

//将抽象字符串(字符序列)，按unicode字符集来编码为bit流(按Bytes分块)
byte[] unicodeBytes=unicode.GetBytes(unicodeString);

//在byte[]级别进行转换
byte[] utf8Bytes = Encoding.Convet(Encoding.Unicode,Encoding.UTF8,unicodeBytes);

//再将01序列 ->按utf-8字符集 -> 抽象字符串
string utf8String=utf8.GetString(utf8Bytes);

```

#### Encoder类 和 Decoder类

- 是什么
	- 使用GetBytes() 和Decoder类的GetChars() 来将 "抽象字符序列" -> bytes流 -> “抽象字符序列”，这也一个转换的功能。
	- Encoder类 和 Decoder类实例的构造方式比较特殊，且两者要采用同一种字符集来编解码，如：Encoding.ASCII、Encoding.UTF8


- __why 有了Encoding 还需要 Encoder + Decoder？？__
	1. 在网络传输和文件操作中，如果数据量比较大，需要将其划分为较小的块。__对于跨块传输的情况，直接使用Encoding类的GetBytes方法编写程序比较麻烦__，而Encoder和Decoder由于维护了数据块结尾信息，则可以轻松地实现跨块字符序列的正确编码和解码，因此它们在网络传输和文件操作中很有用。


- Encoder Decoder编解码的步骤：
	1. 获取Encoder Decoder实例
		- //获取ASCII编码的Encoder实例￼：
			Encoder ASCiiEncoder=Encoding.ASCII.GetEncoder();￼
		- //获取Unicode编码的Encoder实例￼：
			Encoder unicodeEncoder=Encoding.Unicode.GetEncoder();

	2. 使用Encoder实例的GetByteCount()方法，计算转换后产生的bytes数组的长度
	3. 使用Encoder实例的GetBytes()方法 + 2.中求出的长度 -> 将字符序列转换为bytes数组
	4. 使用Decoder实例的GetCharCount()方法，计算bytes数组按指定的字符集(如：utf8)转换为的字符序列的长度
	5. 使用Decoder实例的GetChars()方法 + 4.中求出的字符序列长度 -> 将bytes数组转换为字符序列
	![实例]()


# C#网络传输程序开发

## TCP网络程序开发
### 使用Socket进行TCP网络传输


### 使用TCP类进行TCP网络传输

因为使用Socket来进行网络传输实在是太罗嗦低效率了，为了简化网络编程的复杂度，.NET对套接字进行了封装，封装后的类就是TcpListener类和TcpClienr类。
#### TcpListener类
##### TcpListener类的常用属性和方法
1. 常用属性：
2. 常用方法：
	![]()
	1. TcpListener类构造函数。构造了TcpListener对象后，就可以__监听__客户端的连接请求了。有如下两种方式构造：
		1. TcpListener（IPEndPoint iep）
		2. TcpListener（IPAddress localAddr, int port）
	2. AcceptSocket()
		- 同步阻塞方式下获取并返回一个用来接收和发送数据的套接字对象，同时从传入的连接队列中移除该客户端的连接请求。该套接字包含了本地和远程主机的IP地址和端口号，然后通过调用Socket对象的Send方法和Receive方法和远程主机进行通信
	3. AcceptTcpClient()
		- 方法用于在__同步阻塞方式__下获取并返回一个可以用来接收和发送数据的封装了Socket的TcpClient对象。
	4. Start()
		- Start方法被调用后，将自己的LocalEndPoint和底层Socket对象绑定起来，并自动调用Socket对象的Listen方法开始监听来自客户端的请求。如果接收了一个客户端请求，Start方法会自动将该请求插入请求队列，然后继续监听下一个请求，直到调用Stop方法停止监听。当TcpListener接收的请求超过请求队列的最大长度或小于0时，等待接收连接请求的远程主机将会抛出SocketException类型的异常。
	5. Stop()
		- 程序执行Stop方法后，会立即停止监听客户端连接请求，并关闭底层的Socket对象。等待队列中的请求将会丢失，等待接收连接请求的远程主机会抛出套接字异常。


----

__TcpListener和TcpClient一样都提供了同步方法和异步方法。__

----


#### TcpClient类
##### TcpClient类的常用属性和方法
1. 常用属性：
2. 常用方法：
	![]()
	1. 构造函数。
		1. TcpClient()。
			- 该构造函数创建一个默认的TcpClient对象，该对象自动选择客户端尚未使用的IP地址和端口号。创建该对象后，即可用Connect方法与服务器端进行连接。
		2. TcpClient（AddressFamily family）
			- 该构造函数创建的TcpClient对象也能自动选择客户端尚未使用的IP地址和端口号，__但是使用AddressFamily枚举指定了使用哪种网络协议__。创建该对象后，即可用Connect方法与服务器端进行连接。
		3. TcpClient（IPEndPoint iep）
			- 当客户端的主机有一个以上的IP地址时，可使用此构造函数选择要使用的客户端主机IP地址。创建该对象后，即可用Connect("serverIP", serverPort)方法与服务器端进行连接。
		4. TcpClient（string hostname, int port）
			- 这是使用最方便的一种构造函数。该构造函数可直接指定服务器端域名和端口号，而且==无须使用connect方法==。客户端主机的IP地址和端口号自动选择。


#### 使用TcpClient TcpListener编写TCP应用程序一般步骤：

##### 编写服务器端TCP应用程序一般步骤：
1. 创建一个TcpListener对象
2. 然后调用该对象的Start方法在指定的端口进行监听。示例代码：
￼![]()
3. 在单独的线程中，首先循环调用AcceptTcpLient方法接收客户端的连接请求，从该方法的返回结果中得到与该客户端对应的TcpClient对象，并利用该对象的GetStream方法得到NetworkStream对象；然后利用该对象得到其他使用更方便的对象，例如BinaryReader对象、BinaryWriter对象，为进一步与对方通信做准备。示例代码：
![]()
￼
4. 每得到一个新的TcpClient对象，就创建一个与该客户对应的线程，在线程中与对应的客户进行通信。例如：
```c#
Thread threadReceive=new Thread(ReceiveMessage);￼
threadReceive.Start();
```
其中，ReceiveMessage是接收消息的方法。
5. 根据传送的情况确定是否关闭与客户机的连接。
```c#
if(br！=null)￼{￼       
	br.Close();￼
}￼
if(bw！=null)￼   
{￼
	bw.Close();￼     
}￼     
if(tcpClient！=null)￼     
{￼         
	tcpClient.Close();￼     
}
```
在关闭连接之前，要先关闭读写流br和bw。
6. 在停止服务后，服务器可以断开监听：
```c#
￼tcpListener.Stop();
```
##### 编写客户端TCP应用程序一般步骤：
1. 利用TcpClient的构造函数创建一个TcpClient对象。
```c#
private TcpClient tcpClient;￼
tcpClient=new TcpClient();
```
2. 使用Connect方法与服务器连接。
```c#
tcpClient.Connect(remoteHost.HostName,5656);
```
3. 使用TcpClient对象的GetStream方法得到网络流，然后利用该网络流与服务器进行数据传输。
```c#
if(tcpClient！=null)￼{￼        
statusStrip1.Invoke(showStatus,"连接成功！");￼           networkStream=tcpClient.GetStream();￼
br=new BinaryReader(networkStream);￼  
bw=new BinaryWriter(networkStream);￼
}
```
4. 创建一个线程监听指定的窗口，循环接收并处理服务器发送过来的信息。
```c#
￼Thread threadReceive=new Thread(ReceiveMessage);￼   
threadReceive.Start();
```
其中，ReceiveMessage方法用来循环接收消息。
5. 完成工作后，向服务器发送关闭消息，并关闭与服务器的连接。






### 同步和异步
利用TCP开发应用程序时，.NET框架提供两种工作方式，一种是同步工作方式（syschronization），另一种是异步工作方式（asynchronous）。

#### 同步TCP
- 是什么
	- 同步工作方式是指利用TCP编写的程序执行到__监听（accept）__或__接收（receive）__语句时，在未完成当前工作（侦听到连接请求或收到对方发来的数据）前不再继续往下执行。

##### 使用同步TCP的一般步骤为：
###### 服务器端
1. 创建一个包含采用的网络类型、数据传输类型和协议类型的__本地套接字对象__，并将其与服务器的IP地址和端口号__绑定__。这个过程可以通过Socket类或者TcpListener类完成。
2. 在指定的端口进行__监听__，以便接收客户端的连接请求。
3. 一旦__接收__了客户端的连接请求，就根据客户端发送的连接信息创建与该客户端对应的Socket对象或者TcpClient对象。
4. 根据创建的Socket对象或者TcpClient对象，分别与每个连接的客户进行数据传输。
5. 根据传送信息情况确定是否关闭与对方的连接。

###### 客户端
1. __创建__一个包含传输过程中采用的网络类型、数据传输类型和协议类型的Socket对象或者TcpClient对象。
2. 使用__Connect__方法与远程服务器建立连接。
3. 与服务器进行数据传输。
4. 完成工作后，向服务器发送关闭信息，并关闭与服务器的连接。
	- 通过发送一些特殊的字符串来控制连接关闭


##### 实例




#### 异步TCP
- 是什么
	异步工作方式是指程序执行到监听或接收语句时，不论当前工作是否完成，都会继续往下执行。


### 实战：使用TCP实现网络聊天室
#### 基于同步TCP的网络聊天室开发

#### 基于异步TCP的网络聊天室开发



## UDP网络程序开发
### 使用Socket实现UDP

### 使用UdpClient类实现UDP
- __.NET库中的UdpClient类对基础Socket进行了封装__，发送和接收数据时不必考虑底层套接字在收发时必须要处理的细节问题，在一定程度上降低了UDP编程的难度，提高了编程效率。

- TCP有TcpListener和TcpClient两个类，而UDP只有UdpClient一个类，位于System.Net.Sockets命名空间中。这是__因为UDP是无连接的协议，所以只需要一种封装后的Socket__。

#### UdpClient类

UdpClient类的__常用属性__
![]()
UdpClient类的__常用方法__

1. 构造方法：UdpClient拥有6种重载的构造函数，对于IPv4来说，常用的重载形式有4种。因为UDP接收端发送端均使用UdpClient类，故UdpClient类的构造对于发送端和接受端分别有不同的适合的构造方式。
	1. public UdpClient（）
		- 此构造函数创建一个新的UdpClient对象，并__自动分配__合适的__本地__IPv4地址和端口号，但该构造函数__不执行套接字绑定__。如果使用这种构造函数，在发送数据报之前，必须先调用Connect方法，而且只能将数据报发送到Connect方法建立的远程主机。用法如下：
			1. UdpClient udpClient = new UdpClient();￼
			2. udpClient.Connect("www.cqut.edu.cn",51666); //指定默认远程主机和端口号￼
			3. Byte[] sendBytes = Encoding.Unicode.GetBytes("你好！");￼ //约定编解码字符集
			4. udpClient.Send(sendBytes,sendBytes.Length); //发送给默认主机
	2. public UdpClient（int port）
		- 这种形式是创建UdpClient对象最方便、最简单的方式。__这个port是本地的port__，可以直接指定，也可以端口号置为0，表示让系统自动为其分配一个合适的端口号，这样就不会发生端口号冲突的情况。
	3. public UdpClient（IPEndPoint localEp）
		- 接收端UDP使用这种比较合适，因为localIPEndPoint是一个IPEndPoint（网络端点）类型的对象实例，__封装的是本地的IP + 端口号__
		- 。这样一来，只要远程主机使用这个IPEndPoint中的IP和port，就可以直接向本机的指定端口发送数据报。用法如下：
			1. IPAddress  localIp = Dns.GetHostAddress( Dns.GetHostName() )[0];￼   
			2. IPEndPoint  localIPEndPoint = new IPEndPoint(localIp ,51666);￼    
			3. UdpClient  udpClient = new UdpClient(localIPEndPoint );
	4. public UdpClient（string hostname, int port）
		- __这个string hostname, int port是对方端的__，本地端会自动分配合适的IP地址和port。__这种构造相当于将Connect合为一体了，故只能用于向特定端发送数据 or 从特定端接收数据__。用法如下：
			1. UdpClient udpClient=new UdpClient("www.cqut.edu.cn",51666);






#### 使用UdpClient类实现UDP的一般步骤


### 同步和异步


### 实战：UDP的广播||组播程序开发 
#### 多播
- 是什么

- 优缺点
	- 优点:
		不需要像组播那样多了加入组播组和退出组播组的步骤。即，对于恰好是想要想整个子网广播的情况最适合。
	- 缺点：
		粒度太大，只能向整个子网为单位广播。但是，对于跨子网的、子网内有的主机不想接的情况都不行


- 广播分两种类型：
	1. 本地广播：只向某一子网中的all主机发送消息
		- 为了让发送的消息能被子网内all主机收到，发送的广播消息必须包含一个特殊的IP地址：这个IP地址的主机号的二进制表现形式全为1，例如：子网号为192.168.0.0的广播地址为192.168.0.255
	2. ~~全球广播：向全球all网络设备发送消息。路由器会自动过滤全球广播，这种方式已经被弃用了。~~
		- ~~全球广播的广播消息包含的特殊IP地址为:255.255.255.255。~~

- IP广播的使用步骤：
	1. 

#### 组播
- 是什么
	
- why need it
	用来弥补广播的不足。

- 优缺点
	- 优点：
		1. 可以跨多个子网。组播组是开放的，任何位于不同子网的都可以随时加入组播组、随时退出组播组。一旦加入，便会被广播，一旦退出，就不会再被广播。
		2. 可以自定义广播到哪些主机，是通过引入一个组播组的概念实现的。
	- 缺点：

- 注意：
	1. 组播地址范围是224.0.0.0～239.255.255.255的D类IP地址。任何发送到组播地址的消息都会被发送到组内的所有成员设备上。
	2. 大多数的组播是临时的，仅在有成员的时候才存在，用户创建一个新的组播组时，只需从地址范围内选出一个地址，然后为这个地址构造一个对象，就可以开始发送消息了。
		- ==这些是公网，万一和另一个人冲突了怎么办？？？==
	3. 使用组播时要注意TTL（Time to live，生存周期）值的设置。TTL是允许路由器转发的最大次数，默认情况下，TTL的值为1，如果使用默认值，则只能在子网内发送。可以使用下列两种方式来更改ttl:
		1. UdpClient对象提供了一个Ttl属性，可以利用它修改TTL的值。
		2. 在UdpClient对象使用JoinMulticastGroup加入组播组时设置。
			- udpClient.JoinMulticastGroup(IPAddress.Parse("224.100.0.1"),8);

- IP组播的使用步骤：

#### 基于广播和组播的网络会议程序开发
- 是什么
	通过Internet实现群发功能的形式有两种：
	1. 一种是利用广播向子网中的所有用户发送信息，例如各种通知、公告、集体活动日程安排等；
		- ==西电导航里的群发通知，也是这么做的??????==
	2. 另一种是利用组播向Internet上不同的子网发送信息，例如集团向其所属的公司或用户子网发布信息公告等。


- 组播和广播可以结合着使用。
	- 登录的时候，用到了广播。进入会议、讨论聊天和更新成员列表则用到了组播。


- 功能介绍：

- 具体实现：


## RawSocket网络程序开发



## P2P网络程序开发

- 是什么
	在P2P技术尚未风行之前，几乎所有的网络应用都是采用C/S架构或者B/S架构。P2P架构与传统架构C/S不同，使用P2P技术实现的每个计算机节点既是客户端，也是服务器，其功能的提供是对等的，每个计算机节点根据自己的计算能力，同时承担了一部分服务器功能

### P2P相对于C/S的优缺点

### P2P系统的分类
使用P2P方式架构的系统可以分为两大类：
1. 一类是单纯型P2P，没有专用的服务器；
	__单纯型P2P系统中的各个节点之间直接交互信息__。这种方式的优点是不依赖于专用的服务器，任何一台计算机只要安装同一个P2P应用软件，就可以和其他安装这个软件的计算机直接通信。
2. 另一类是混合型P2P，即单纯型和专用服务器相结合的架构。
	混合型P2P将单纯型P2P和C/S架构相结合，它和传统C/S的区别在于：传统C/S架构的所有资源都存放在服务器中，所有的传递内容都经过服务器；__而对于混合型P2P来说，此时的服务器仅仅起到促成各节点协调和扩展的作用，一般称这种服务器为索引服务器__。在这种架构下，资源不是全部存储在服务器上，而是分布在各个计算机上。



### 主流P2P应用分类
依据技术实现上的差别，当前P2P网络应用大致可以分为文件共享类应用、即时通信类应用，多媒体传输类应用。
1. 文件共享类应用：
	文件共享类应用俗称“文件下载”，是大家平时上网下载东西时最常用到的。例如，迅雷、BT等软件都是文件下载的典型应用。
2. 即时通信类应用：
3. 多媒体传输类应用：
	多媒体传输类应用也称“流媒体播放”，是近年来悄然兴起的Internet视频直播软件应用。这类软件使用网状结构，支持多种格式的流媒体文件，节点间动态查找就近连接。

### P2P通信步骤
在所有的P2P应用中，对等节点首先必须能够彼此发现对方，一旦找到提供P2P服务的计算机节点，就可以直接与它通信。即P2P应用的通信由__发现__、__连接__和__通信__3个步骤组成。
1. 发现阶段
	- 一台计算机要和另一台计算机通信，__必须知道对方的IP地址和监听端口号__。
2. 连接阶段和通信阶段
	- 完成对等节点定位和资源搜索之后，就可以根据需要，选择TCP、UDP或者其他协议完成数据传输。
		- 如果选择TCP，则首先需要在对等结点之间建立连接，而后利用该连接在对等结点之间传送数据；
		- 如果选择UDP，则无须建立连接，直接在对等节点之间通信即可。


### .NET下的P2P程序开发
#### PNRP协议
- 是什么
	1. 对等名称解析协议（Peer Name Resolution Protocol, PNRP），完成对等名称的注册和解析。
		- 名称注册：
			- 任何资源若要被网络上的其他主机识别到，首先必须注册到P2P网络。名称注册就是将包含对等节点信息的对等名发布到云中，以便其他对等节点解析。
		- 名称解析：
			- 名称解析是指利用对等名称获取注册到云中的资源所在对等节点的IP地址和端口号的过程。
	2. PNRP只负责让对等端相互间知道各自的IP + port，这样就完成了P2P的发现阶段，后续的连接、通信阶段，就只是前面讲的普通的使用TCP/UDP等传输层协议了。可以说，单纯性P2P的核心就是PNRP协议，只不过像BT下载那种P2P应用，基于TCP/UDP层设置了别的复杂的理论优化，如：将大文件切成小文件，从多个对等端上接受(即，PnP)来实现的下载速度快。






# Internet应用程序开发

## FTP网络程序开发

### FTP原理及规范

#### FTP协议||文件传输服务
- 文件传输任务
	1. 信息共享 -> 文件传输需求 -> 文件传输服务程序 <- 基于FTP协议设计
	2. 文件传输服务是由FTP应用程序提供的，而FTP应用程序遵循的是TCP/IP中的文件传输协议，它允许用户将文件从一台计算机传输到另一台计算机，并且能保证传输的可靠性。

- FTP协议：	
	- 是应用层协议，是在RFC959中说明的。该协议定义了远程计算机系统和本地计算机系统之间传输文件的一个标准。
		- TCP/UDP不是能传输文件吗？？why还要专门定义一个FTP应用层协议来传文件。

- FTP功能：
	1. 提供文件的共享，包括程序文件和数据文件。
	2. 支持间接使用远程计算机。
	3. 使用户不因各类主机文件存储器系统的差异而受影响。
	4. 利用TCP提供可靠且有效的传输。



- 注意：
	- 一般来说，传输文件的用户需要先经过认证以后才能登录远程服务器，然后访问远程服务器中的文件。__而大多数的FTP服务器往往提供一个GUEST的公共账户来允许未注册用户访问该FTP服务器。__


#### FTP与HTTP区别
- 同：
	1. 传输层协议均基于TCP协议
- 异：
	1. 

#### FTP的特点：why对于文件上传|下载需求 FTP比HTTP smtp 更适合？？？？


### .NET下FTP相关类

### 实战：


## SMTP与POP3网络程序开发技术


### 邮件发送&&SMTP

- 是什么
	- 邮件发送需求 -> 基于TCP的SMTP应用层协议的设计 -> 基于SMTP协议的程序(SMTP协议的具体实现)

- SMTP的2种工作方式：
	1. 一种是使用匿名方式发送邮件，称为SMTP；
	2. 另一种是客户端必须提供用户名密码认证，称为ESMTP（Extentded SMTP）

- 客户端发送电子邮件的过程：
	1. 先通过客户端将邮件发送到SMTP邮件服务器	----	__上传__
		1. 客户端先与服务器__建立连接__
			1. 客户端发送“EHLO Local”命令，服务器收到后返回“220”响应码，表示服务器准备就绪。
			2. 客户端发送“AUTH LOGIN”命令，服务器收到后返回“334”响应码，表示要求用户输入用户名。
			3. 客户端发送经过Base64编码处理的用户名，服务器收到并经认证成功后返回“334”响应码，表示要求用户输入密码。
			4. 客户端发送经过Base64编码处理的密码，服务器收到并经认证成功后返回“235”响应码，表示认证成功，用户可以发送邮件。
		2. 客户端开始发送__邮件的信封__
			1. 客户端发送“MAIL FROM：＜发信人的地址＞”命令，服务器收到后返回“250”响应码，表示请求操作就绪。
			2. 客户端发送“RCPT TO：＜收信人的地址＞”命令，服务器收到后返回“250”响应码，表示请求操作就绪。
		3. 客户端开始发送__邮件数据__
			1. 客户端发送“DATA”命令，表示开始向服务器发送邮件数据，包括邮件的首部和正文。
			2. 客户端发送邮件首部。
			3. 客户端发送正文。
		4. 客户端和服务器__断开连接__

	2. 再通过当前的服务器发送到下一个目标SMTP邮件服务器	----	__中转__

#### SMTP的特点：why邮件发送smtp比http ftp适合？？


### 邮件接收&&POP3

- POP3
	- POP3允许客户端连接到服务器并且将所有的邮件下载到客户机的邮箱中。
	- POP3邮局服务器通过__侦听TCP端口110__提供POP3服务。
	- __客户端读取邮件之前，需要先与服务器建立TCP连接__。连接成功后，POP3服务器会向该客户端发送确认消息。然后客户端根据服务器回送的信息决定下一步的操作。
	- POP3规定__每条命令均由命令和参数两部分组成__，每条命令都以回车（CR）换行（LF）结束，命令和参数之间由空格间隔。
	- POP3服务器回送的__响应信息由状态码和附加信息（可选）组成__。所有响应也都以回车（CR）换行（LF）结束。其中，状态码有以下两种:
		- +OK：表示正确执行了客户端发送的命令。
		- -ERR：表示服务器执行命令失败。


#### POP3的特点：why邮件接收pop3比http ftp 高效


### .NET下的邮件收发相关类

### 实战：邮件客户端程序设计






## 基于HTTP的Web程序开发技术

- 是什么
	- (万维网下任意传输Web页面)需求 -> HTTP协议 -> Web服务器(HTTP协议的实现)

### HTTP协议概述

- 是什么
	- [两点]之间传输[超文本数据]的约定和规范。
		- 两点之间可能是 服务器 <->本地浏览器，也可以是 服务器 <-> 服务器，可不可以是 本地浏览器 <-> 本地浏览器 ？？？？




#### HTTP发展和演进
##### HTTP/1.0
###### HTTP请求
- 在早期的HTTP 1.0中，定义了3种最基本的请求类型：GET、POST和HEAD。
- 客户端程序用大写指令将请求发送给服务器，后面跟随具体的数据。由于这些请求的类型实际上是告诉服务器采用什么方法（method）来处理客户端的请求，所以也将这些请求的类型称为请求的方法。

###### HTTP响应


##### HTTP/1.1
###### HTTP请求
- HTTP 1.1提供了8种HTTP请求的方法
	![]()
	- 虽然HTTP 1.1定义了大量的请求类型，但是对于程序员来说，一般关心的只有GET请求和POST请求。


- HTTP请求的书写格式：
	在HTTP请求中，第一行必须是一个请求行（request-line），说明请求类型、要访问的资源以及使用的HTTP版本；紧接着是标头（header）部分，说明服务器要使用的附加信息，这部分一般由多行组成；标头之后是一个空行（blank line），表明标头结束；空行之后是请求的主体（request-body），主体中可以包含任意的数据。如下：
```
    ＜request-line＞￼ 
    ＜headers＞￼   
    ＜blank line＞￼   
    [＜request-body＞]

```

- 注意：
	1. 一是请求的方法名称区分大小写
	2. 二是HTTP服务器至少应该实现GET和HEAD方法，其他方法都是可选的
	3. 如果服务器不支持客户端发送的请求方法，则服务器将返回错误并立即关闭连接




###### HTTP响应

###### HTTP状态码


##### HTTP/2
###### HTTP请求


###### HTTP响应


##### HTTP/3

###### HTTP请求


###### HTTP响应





#### HTTP请求||HTTP响应


#### HTTP协议特点：why传输Web文档 使用HTTP比使用FTP SMTP更高效？？？

1. HTTP底层__基于TCP__方式工作
	- HTTP采用TCP传输数据，因此__不会丢失数据__，__也不会出现乱序__的情况。
2. HTTP是__无状态的__
	- 无状态”的含义是，客户端发送一次请求后，服务器并没有存储关于该客户端的任何状态信息。即使客户端再次请求同一个对象，服务器仍会重新发送这个对象，而不管之前是否已经向客户端发送过这个对象。

3. HTTP使用__元信息作为标头__。
	- HTTP通过添加标头（header）的方式向服务器提供本次HTTP请求的相关信息，即在主要数据前添加一部分信息，称为元信息（metainformation）。例如，传送的对象属于哪种类型，采用的是哪种编码等。


#### HTTPS 和 HTTP

### .NET下的HTTP相关类




### 实战：基于HTTP的多线程文件下载器





## Web Service程序开发技术













# 其他

1. TCP传输时，为什么Accept会返回新的socket对象？？是为了server连接多个client吗才专门弄一个socket用来接收链接的吗？？

2. TCP传输时，C#只支持发送bytes[]数组，故对于源信息(字符串 or 数值类型)双端要使用一致的字符集来编解码，如:都是用Encoding.ASCII，Encoding.UTF8等。
3. 组播地址范围是224.0.0.0～239.255.255.255的D类IP地址是公网，万一和另一个人冲突了怎么办？？？
4. 西电导航里的群发通知，是使用udp的IP广播做的？？？还是IP组播？？还是广播+组播？？or别的方式？？
5. 单纯性P2P应用 == PNRP(使用资源名来获取IP + port) + 普通的TCP/UDP传输。但是像BT下载那样明显不是普通的TCP/UDP，使用切片-索引 + 从多个主机上接受，这不是相当于PnP了吗？？？


6. TCP/UDP不是能传输文件吗？？why还要专门定义一个FTP应用层协议来传文件。
	- TCP/UDP是传输层协议，他只提供了一种最基本的数据传输能力(因为他要保证common，故只支持传byte[])，但是应用层协议是一般都是针对于特定的需求设计的，应用层协议 = 传输层协议(能力) + 面各项任务的控制优化


7. 我觉得应用层协议的学习 不同于 传输层以下的TCP/IP协议栈的学习。
	- TCP/IP协议栈是一个简单纯粹的、通用的东西，它就像一个管道，他的学习就是单纯的搞懂裸数据传输的机制就可以。
	- 而应用层协议都是基于TCP/IP协议栈 + 对于特定需求的优化，学习他们我们需要进行对比学习来掌握应用层协议为什么这么设计的本质，不搞懂__为什么非他不可__其实就没有搞懂应用层协议。如：
		1. why 文件传输方面 FTP 比 HTTP SMTP更高效？？
		2. why 邮件收发方面 SMTP比 HTTP FTP更高效？？ 邮件本身不也是文件吗？？why不能用FTP非要在弄一个？？
		3. why Web页面文档的传输方面 HTTP比 FTP SMTP更高效？？Web页面本身不也是(Html + css + js)文件？？？ why不直接使用FTP来传
			- 因为 超文本 != 普通文本，超文本多了一些特点，针对这些特点可以做专门的与优化。


8. 结合C版本的从零搭建一个HTTP服务器 + C#网络书里的HTTP部分 + 小林的图解网络的HTTP部分 ->弄明白HTTP的本质，并搭建出我的HTTP服务器，给Unity后端做服务 

## .NET的学习
### OpenFileDialog类

