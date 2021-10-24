[toc]

# RANSAC思想

- 认为最小二乘拟合的低效 is 由于点集中混进的outliners起到的反作用 (将拟合的直线拉偏了)
- 


# RANSAC使用步骤


![ransac流程图]()


## 1. 去除外点( 通过从all原始点集中选择inliners来实现 )

- 1. 根据 inlinerP 、 置信度confidence 、 每次的随机选点数目 ----> 确定 循环次数K
- 2. 设计每次循环的过程:
	- 进行一次选点--->拟合出model
	- 
	- wei每个选择下标之外的点进行 ---> 内外点判别机制 ---> inliner or outliners
	- 将各inliner的下标存入一个vector
	- 对inliner的数目进行计数：使用inliner数目来从K次循环中选出最优秀的一次循环(1.初始选点拟合出的model认为是最好的、2.使用此model筛选出的inliners再重新进行model的拟合)
		- 使用一个结构体 { inlinears下标vector , inlines数目 }  来进行best更新，这样当K次循环进行完后，best就是找的最优的

## 2. 用1.中区分出的内点集--->重新--->拟合model




# ransac案例

## ransac拟合Homo矩阵

### 1. 自动计算循环次数K

### 2. 设计每个循环过程：
#### - 1. 范围内随机取点

#### - 2. 由所选点拟合model
![]()
- 本质抽象为一个AX=b的求解问题
- AX=b的通用求解公式 
![]()
- C++使用Eigen进行svd分解： -> u、s、v
- 自编写svd分解算法：

#### - 3. 使用拟合出的H (model) -> 判别机制 -> 对all点进行筛选
- 判别机制规则：
- 
