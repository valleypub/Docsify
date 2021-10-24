[toc]



# c# 核心

## 关键字

### public protected private

### get set 

### readonly

### static


	常规用法:


	 public static IceServer DefaultIceServer
	    {
	        get{
	            return new IceServer(TurnUrl, TurnUser, TurnPass);
	        }
	    }


​	    


	public static readonly string BackupStunUrl = "stun:stun.l.google.com:19302";


​	

	public static bool HasAudioPermission()
	    {
	#if UNITY_ANDROID && UNITY_2018_3_OR_NEWER
	        if (Application.platform == RuntimePlatform.Android)
	        {
	            return UnityEngine.Android.Permission.HasUserAuthorizedPermission(UnityEngine.Android.Permission.Microphone);
	        }
	#endif
	        //Assume true for all other platforms for now
	        return true;
	        
	    }



### using(){};语句

- 1. 当我们做一些比较占用资源的操作，而且该类或者它的父类继承了IDisposable接口，这样就可以使用using语句，在此范围的末尾自动将对象释放，常见的using使用在对数据库的操作的时候
- 2. 该类或者它的父类继承了IDisposable接口，才能使用using(){};

```
using (MemoryStream stream = new MemoryStream())
            {
                try
                {
                    // 创建序列化类
                    BinaryFormatter bf = new BinaryFormatter();
                    //序列化到stream中
                    bf.Serialize(stream, t);
                    stream.Seek(0, SeekOrigin.Begin);
                    return stream.ToArray();
                }
                catch (Exception ex )
                {
                    Console.WriteLine(ex.Message);
                    return null;
                }
            }
            
            等价于<======================================>等价于
            
		MemoryStream stream = new MemoryStream();
				try
                {
                    // 创建序列化类
                    BinaryFormatter bf = new BinaryFormatter();
                    //序列化到stream中
                    bf.Serialize(stream, t);
                    stream.Seek(0, SeekOrigin.Begin);
                    return stream.ToArray();
                }
                catch (Exception ex )
                {
                    Console.WriteLine(ex.Message);
                    return null;
                }
            	 finally
    			{
      				if (stream != null)
        			((IDisposable)stream ).Dispose();
   				}
            

```

### 委托--方法名的本质
- 1. 将函数名赋值给委托变量
- 2. 即使委托变量做为形参
```
		//将方法名直接赋值给，同符号、同返回值的委托对象

		public delegate void OnReceive( NetPacket packet );
         // 每个消息对应一个OnReceive函数
        public Dictionary<string, OnReceive> handlers = new Dictionary<string, OnReceive>();;
         // 处理服务器接受客户端的连接
        public virtual void OnAccepted(NetPacket packet)
        {
        }
        public void AddHandler(string msgid, OnReceive handler)
        {
            handlers.Add(msgid, handler);
        }
		AddHandler("OnAccepted", OnAccepted);

```



## C#下的多线程读写保护机制？

### lock(对象资源){ }语句 
- 1. lock锁的是资源，本质上是对资源的一种读写保护机制。
- 2. 一般用于多个线程-对同一个对象读写时的保护。(同一时间只允许一个代码段{ }[因为一个{}只能属于一个线程，故相当于实现了同一时间只能一个线程访问资源]操作此资源)
- 3. 对象资源在被lock(对象名){}锁住期间({ }代码段)，只能由此代码段执行，别的线程不能访问此对象资源
- 4. 可以lock的资源包括：对象、只有对象能被lock？？

```
// 存储网络数据的队列
        private Queue Packets = new System.Collections.Queue();
        
        
         // 数据包入队
        public void AddPacket( NetPacket packet )
        {
            lock (Packets)
            {
                Packets.Enqueue(packet);
            }
        }

        // 数据包出队
        public NetPacket GetPacket()
        {
            lock (Packets)
            {
                if (Packets.Count == 0)
                    return null;
                return (NetPacket)Packets.Dequeue();
            }
        }

```


## 序列化(对象流序列化)技术

- 1.是对象永久化的一种机制。
```
一般程序在运行时，产生对象，这些对象随着程序的停止运行而消失，但如果我们想把某些对象（因为是对象，所以有各自不同的特性）保存下来，在程序终止运行后，这些对象仍然存在，可以在程序再次运行时读取这些对象的值，或者在其他程序中利用这些保存下来的对象。这种情况下就要用到对象的序列化。
```
#### 二进制序列化

#### json序列化

#### xml与SOAP序列化









