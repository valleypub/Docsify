[toc]

# H可用的两种情况
## 同一平面上
- 公式证明
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0085.PNG" style="zoom:50%;" />

## t=0，光心纯旋转R
- 公式推导
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0086.PNG" style="zoom:33%;" />

## 总结H可用的情况
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0087.PNG" alt="使用H的common" style="zoom:50%;" />

- H的好处：
	- 是2d-2d的变换


## 系数在H求解&&2d-2d的影响
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0088.PNG" alt="H的公式推导" style="zoom:50%;" />


## 对于t!=0 && 不在同一平面上，使用R，t

- 由于t!=0 -> 存在对极几何约束 -> F -> E -> R,T
- 

# 图像拼接过程

## 1. 总系统设计
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0083.PNG" alt="总流程图" style="zoom:50%;" />

## 2. RANSAC拟合H

### 1. 去除外点( 通过从all原始点集中选择inliners来实现 )

- 1. 根据 inlinerP 、 置信度confidence 、 每次的随机选点数目 ----> 确定 循环次数K
- 2. 设计每次循环的过程:
	- 进行一次选点--->拟合出model
	- 
	- wei每个选择下标之外的点进行 ---> 内外点判别机制 ---> inliner or outliners
	- 将各inliner的下标存入一个vector
	- 对inliner的数目进行计数：使用inliner数目来从K次循环中选出最优秀的一次循环(1.初始选点拟合出的model认为是最好的、2.使用此model筛选出的inliners再重新进行model的拟合)
		- 使用一个结构体 { inlinears下标vector , inlines数目 }  来进行best更新，这样当K次循环进行完后，best就是找的最优的

### 2. 用1.中区分出的内点集--->重新--->拟合model

### 注意
#### 1. 随机函数对H的影响
#### 2. 解AX=b的问题
- 1. 使用A+来对任意奇异矩阵求解
	- 由于计算机float算不准，误差很大

- 2. 使用SVD分解的V的最后一列作为解
	- 对于矮宽型A适用
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\IMG_0084.PNG" alt="证明" style="zoom:50%;" />


## 3. 确定基准图像->统一坐标系
- 1. 计算基于基准图像的uv坐标系的GlobalPoints
- 2. 遍历all GlobalPoints 确定 上、下、左、右四点 -> 确定最终大图的尺寸
## 4. 图像拼接
### 正向拼接
- 1. 根据finalPicture尺寸 -> 初始画图片
- 2. 将GlobalPoints逐像素填入进去
	- 1. 将GlobalPoints由基准图UV坐标系 -> 大图的uv坐标系
	- 2. 遍历填BGR

<img src="C:\Users\king-kong\Desktop\要做的事情\picture\正向拼接.jpg" alt="结果图" style="zoom:50%;" />

### 反向拼接
#### 采用剪枝的方式
- 1. 尾次剪纸
<img src="C:\Users\king-kong\Desktop\要做的事情\picture\反向拼接.jpg" style="zoom:50%;" />

- 2. 首次剪纸
![首次剪纸](C:\Users\king-kong\Desktop\要做的事情\picture\反向拼接_剪枝.jpg)
#### 采用融合的方式


