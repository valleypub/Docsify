[toc]


- 使用color argb32 1920 1080 4 的是可以的，直接可以使用videoReceiver的startRender()来进行2D渲染
	- ok


- 对于自定义的数据组装发送，写专门的render函数
	- 

# 剩余的test:

- 能流畅的最大的图片size

- 远端的声音方面的问题，这个没有改动，能否正常工作

- 整套系统用户界面的开发，尤其是虚拟用户界面，keyboard的使用

- 信令服务器的公网部署问题，对于位于两个校区的距离，使用网络穿透后，fps会降低多少 



- 目前测试出主要是transform变换主要浪费时间
	- 8294400 + 576×640×2 = 9031680 还能保证24fps，而且采用rgb+d直接连接的方式来连接，彩色部分不会有大的失真
	- 2211840 = 576 640 6使用了

- 既然transform没法用，就只能在显示端进行加速反投影
	- 使用C#的并行循环
		- 什么时候该用，什么时候不该用
		- 自动控制并发数量or主动控制并发数量
		- https://docs.microsoft.com/zh-cn/dotnet/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop
	- 这一部分改变能提升3frame左右 <img src="C:\Users\king-kong\Desktop\要做的事情\picture\C#\并行for编程1.PNG" style="zoom:50%;" />
	- 这一部分改变几乎没有提升：
		- ![](C:\Users\king-kong\Desktop\要做的事情\picture\C#\并行for编程2.PNG)
	- 这一部分改变我本以为代码比较多，能影响较高的，结果只提升了2frame
```
//不要在循环体内使用new会触发频繁的gc
            Vector3 uv_depth = new Vector3(0.0f, 0.0f, 0.0f);
            Vector3 uv_color = new Vector3(0.0f, 0.0f, 0.0f);
            float UV_X = 0.0f;
            float UV_Y = 0.0f;
            //由16bit的深度图数组 -> float型的 x y z
            for (int i = 0; i < Depth16_1.Length; i++)
            {
                #region 求实际xyz
                ushort depthtemp = Depth16_1[i];
                float tempZ = (float)depthtemp / 1000.0f;
                xyzArr[i].x = colmap_cam_1[i % 640] * tempZ;
                xyzArr[i].y = rowmap_cam_1[i / 640] * tempZ;
                xyzArr[i].z = tempZ;
                #endregion

                #region 求对应color
                uv_depth.x = xyzArr[i].x;
                uv_depth.y = xyzArr[i].y;
                uv_depth.z = xyzArr[i].z;

                uv_color.x = Vector3.Dot(R11, uv_depth);
                uv_color.y = Vector3.Dot(R12, uv_depth);
                uv_color.z = Vector3.Dot(R13, uv_depth);
                uv_color = uv_color + T1;

                //在rgb图中的uv坐标
                UV_X = (uv_color[0] / uv_color[2]);
                UV_Y = (uv_color[1] / uv_color[2]);

                if ((UV_X >= 0 && UV_X < 1920) && (UV_Y >= 0 && UV_Y < 1080))
                {
                    int temp = (int)(UV_X + UV_Y * 1920);
                    colorArr[i].b = (float)rgbdByte[4 * temp] / 255.0f;
                    colorArr[i].g = (float)rgbdByte[4 * temp + 1] / 255.0f;
                    colorArr[i].r = (float)rgbdByte[4 * temp + 2] / 255.0f;
                    colorArr[i].a = (float)rgbdByte[4 * temp + 3] / 255.0f;

                }
                #endregion

            }

            //#region 并行for投影
            //Parallel.For(0, Depth16_1.Length, (i) => {

            //    Vector3 uv_depth = new Vector3(0.0f, 0.0f, 0.0f);
            //    Vector3 uv_color = new Vector3(0.0f, 0.0f, 0.0f);
            //    float UV_X = 0.0f;
            //    float UV_Y = 0.0f;

            //    ushort depthtemp = Depth16_1[i];
            //    float tempZ = (float)depthtemp / 1000.0f;
            //    xyzArr[i].x = colmap_cam_1[i % 640] * tempZ;
            //    xyzArr[i].y = rowmap_cam_1[i / 640] * tempZ;
            //    xyzArr[i].z = tempZ;

            //    uv_depth.x = xyzArr[i].x;
            //    uv_depth.y = xyzArr[i].y;
            //    uv_depth.z = xyzArr[i].z;

            //    uv_color.x = Vector3.Dot(R11, uv_depth);
            //    uv_color.y = Vector3.Dot(R12, uv_depth);
            //    uv_color.z = Vector3.Dot(R13, uv_depth);
            //    uv_color = uv_color + T1;

            //    //在rgb图中的uv坐标
            //    UV_X = (uv_color[0] / uv_color[2]);
            //    UV_Y = (uv_color[1] / uv_color[2]);

            //    if ((UV_X >= 0 && UV_X < 1920) && (UV_Y >= 0 && UV_Y < 1080))
            //    {
            //        int temp = (int)(UV_X + UV_Y * 1920);
            //        colorArr[i].b = (float)rgbdByte[4 * temp] / 255.0f;
            //        colorArr[i].g = (float)rgbdByte[4 * temp + 1] / 255.0f;
            //        colorArr[i].r = (float)rgbdByte[4 * temp + 2] / 255.0f;
            //        colorArr[i].a = (float)rgbdByte[4 * temp + 3] / 255.0f;
            //    }

            //});
            //#endregion
```

- C#并行循环优化还是不太行（因为cpu本身就12个core,真正的并行最大也就12倍？？而且线程创建和切换也要时间故->不太行，)，要使用gpu来进行simd加速
- 使用gpu进行加速



# bug
1. why 颜色是绿色的
2. why 真刷新率降得这么多？？
3. 为什么粒子系统显示的数据会 随着缩放因子变化，而旋转呢？？
4. 将每次进行marshal.copy + bytetovectorTest 变为 times只进行一次，就不会crash了
	- 目前已知有两种情况会引发crash:
		- 1. particleSystem相对于Main camera的位置
		- 2. ByteToVectorTest(bgrdByte);语句只能运行一次，如果运行多次会crash
	- 解决办法：
		- why将他们放在一个块语句内就能解决了？？？
			- ![块语句内就能解决](C:\Users\king-kong\Desktop\要做的事情\picture\C#\块语句内解决crash.PNG)
5. 为什么显示的color色号有问题？？看起来偏蓝？？
	- 是shader的问题，要自己设置or写一个shader，因为我曾经使用微软官方自带的组件渲染出来的是很真实的，没有偏蓝现象，但是那个是2d下的texture，不知道3d下能否通用or要自己写一个


6. 想写死一个关都关不住的Unity程序很简单，只需要使用多线程(ru：parrallel.for() + 对同一个资源同时进行资源争用or清理 ru：![parllel+array.clear引发的bug](C:\Users\king-kong\Desktop\要做的事情\picture\C#\写一个bug.PNG)


7. 解决开机两次的问题
	- 发现每次要开启、关闭、再开启，是因为第一次开启显示的画面是静止的
		- 1. 通过偶然的一次粒子系统发现，之所以静止，是因为现实的frame是上一次的，因为本次关闭了粒子系统组件，第一次却显示粒子系统组件
		- 2. 而且我发现，就算刚开始没连接Azure Kinect第一次也会显示画面，而且关闭，再开启，无论多少次只要不连接Azure Kinect就会一直显示之前的画面 -> 说明 这些frame一定是关闭后未被清理，而且存在了程序环境中的某个位置(全局变量？？？)，而且可以被渲染接口作为frame来获取到
	- 解决bug：
		- 是只opencKinect()忘了closeKinect()，但是如果第一次没关Kinect，第二次再openKinect时Kinect会自动关闭(通过观察Kinect镜头上的光熄灭了)，这就让第三次能正常开启了。表现为两次开机问题
			- 使用OnDisable() , OnDestroy() , OnAppicationQuit()中调用closeKinect()均可以，但是这三个monoBehavior方法还是有缺点
		- 但是，为什么Kinect第二次还是有画面？？虽然是第一次期间捕获的画面(通过一次偶然禁用particle system发现的)而且只有一张不会变化？？？



8. 解决掉帧极其严重的问题


9. 使用 videocapture + scene可以接收到scene的屏幕数据，可以进行连接，但是vidoe的数据发不过去
	- 是信令服务器的握手的标识符的问题
		- peerconnection中的标识符反一下就好了
	- 因为出场时all ,is  Local : Unity  Remote : PC，而我只改了VideoChat中的，故只有这个是负的，故只有这个负的videoChat可以和别的正的peerConnection进行握手(正负相反才行)。





10. 使用Azure Kinect时，即使只是将相加连上pc，而不管是否仍使用webcam or custom，unity都会直接crash(直接闪退)
	- 是Azure Kinect使用7通道的 声卡导致的，这是一个chrome开源的 webrtc 引擎的一个bug至今未修复，只能避免掉他
	- 在计算机管理中禁用Azure Kinect的声卡：注意有两处，都要禁用，不然仍会闪退
		- ![第一处]()
		- ![第二处]()


----------------------------------------------------------------------------------------------------------------------------------------
至此，局域网下，两台之间传输自定义数据可以实现

----------------------------------------------------------------------------------------------------------------------------------------


- 如何实现公网下进行传输？？？

11. 将node-dss信令服务器移到公网云服务器上运行后，为什么unity上连接不上？？会报![node报错]()
12. 将在windows上能npm start成功的信令服务器 移到 云服务器上why就不行了？？？
	- 问题出在了 npm install这一步



13. why使用stun无法进行校园网穿透，使用because-why-not的turn服务器才可以？？但是使用turn传输大数据量9000000B却能做到18fps左右，说明这个服务器并不是使用的中继传输，因为中继是60kbps左右贷款太低，说明使用的还是stun，只是一般turn服务器都是内部集成的有stun，只是他集成的这个stun是可以使用的(不像谷歌的在中国被禁用了)
14. 如何自己部署一个stun放到实验室的云服务器上？？

----------------------------------------------------------------------------------------------------------------------------------------
下一步：
		进行采集-和粒子渲染加速

进行深度数据的摆放研究 -> to 减小 webrtc的有损压缩对深度数据的较大的影响

编译一个corturn放在服务器上

进行声音同步测试

----------------------------------------------------------------------------------------------------------------------------------------
15. 如何进行采集-和粒子渲染加速
	- 使用gpu版的粒子系统进行粒子显示
		- 线程组的划分设计会对并行性能产生影响吗

16. 使用particlesystem时，一运行直接crash的原因是
	- 很乱，很随机
		- 有时crash后加上 Array.clear()就好了
		- 有时去掉两个Array.clear()一样没问题
		- 好像和Array.clear()没什么关系，好像是使用了并行循环获取颜色后引发的crash，且就算立马改过来，后几次仍然会有问题，再重启一次就好了



17. 粒子系统渲染的慢是因为渲染的点太多了吗？我目前渲染的单台相机 1920*1080 = 2073600个点

18. 实际使用mycustomsource + videoRenderTest_preCompile两个脚本
	- videoRenderTest    videoRenderTest_depth未使用


19. mrtk-webrtc中可选的传输数据格式：bgra32  I420间的区别？？ 这两种有什么不一样？？网上有说法是：对于不同的格式的源采用的编码器不同
	- 速度上？？
	- 质量上？？

20. 要想在我的unity应用里面使用visual effect graph + visual effect graph依赖于HDRP + 中途换RP还很复杂推荐在使用前确定好使用哪一个 -> 整个过程中只能使用一种HDRP管线？？？对于我的AR整个项目而言足够吗？？？除了粒子系统还有那些部分需要用到渲染管线？？






21. 为什么本地使用粒子系统渲染会崩溃？？？
	- 是不是因为没有clear?? 不是。
	- 把那些原本是2dtexture使用的变量全部清理掉后 + 重新布局了粒子的更新位置后，就好了

22. 感觉发送9031680个数据还是太大了，就是使用原生的渲染方式帧率也只能达到10fps左右



23. 内置粒子系统粒子数达到几百万时，会在最上层出现底层循环的渲染错误，是不是有与粒子数目太多造成的？？


24. 重写一个只测试粒子数目大小的render代码文件
	- 通过单独测试显示部分，发现之所以降帧是因为使用内置的Particle System那一套![]()，只适合处理千量级或几万的粒子数级别，一旦增大到1920 1080 = 2073600个粒子数目时，只是渲染这一项就会耗时408ms，具体可以查看testParticlSystem项目


25. 目前，但用粒子系统显示数据的话，使用videoRenderParticleSystem脚本，关于那个使用预编译指令三合一的只在测试时使用，只因调试起来实在是不方便


26. 通过testParticleSystem项目测试发现，粒子系统渲染耗时的时间分布如下：
	- 使用原始遍历的方式:
	- <img src="C:\Users\king-kong\Desktop\要做的事情\picture\webrtc-hololence\粒子系统时间分布.PNG" alt="粒子系统时间分布图" style="zoom:60%;" />
	- 使用CSahrp并行循环进行加速
		- 使用并行循环效果还不错，能保证在2070000粒子数目的情况下，做到几十毫秒级，但是，SetParticle()这一步没法使用并行循环来提速 -> 2070000粒子数时时延高达170ms下不来 -> 短板效应 -> 整体时延下不来
		- ![]()





----------------------------------------------------------------------------------------------------------------------------------------
下一步：

深度噪声排版问题



----------------------------------------------------------------------------------------------------------------------------------------


----------------------------------------------------------------------------------------------------------------------------------------
下一步：
hololence2移植测试，和优化

----------------------------------------------------------------------------------------------------------------------------------------







