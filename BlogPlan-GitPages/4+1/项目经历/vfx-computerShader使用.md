[toc]


# compute shader
## 讲解文档
https://www.jianshu.com/p/ec9ba6c3a155

https://blog.csdn.net/qq_42115447/article/details/105452924

https://www.bilibili.com/read/cv3356979?from=search

## GPGPU
ComputeShader可以用做通用计算，也就是gpu负责主要的计算过程，最后再将结果传递给cpu，这类非图形计算被称为GPGPU。ComputeShader虽然位于渲染流水线之外，但它支持读写GPU资源，我们可以将运行结果直接传递到渲染管线，从而来完成一些图形处理的效果，这样就没有了从显存到内存的时间开销(此类过程速度很慢)。
也就是说CPU将需要计算的粒子参数传给GPU来计算，由于GPU是用平行架构处理大量的并行数据，所以大量并行无序数据的少分支逻辑（少if）适合GPGPU，将这些复杂的轨迹运算丢给GPU效率会比CPU大得多得多。



- 为什么要有线程组的概念？？？是应为无法对每一个pixel进行real-simd吗？？，每一个线程组代表的是什么？？如果不能做到基于每个像素的simd，那线程组的划分肯定是有影响的，如何根据gpu来划分硬件才能充分利用性能将时延降到最低？？？
- 线程组为什么要有上限？？threadX * threadY * threadZ <= 1024

- compute shader的C# <-> shader的数据传递这一块讲的很混乱，有用buffer的、有不用buffer的(给人一种可以相互访问的错觉)




# Visual Effect Graph


