[toc]


# opencv的收获

1. opencv下使用FileStorage读写 xml 和 yml文件
	1. 像使用python的字典一样使用xml 和 yml文件，最常用的一种用法是，字符串下标作为键，里面存上对应的值(可以是多种类型)。只是对于FileStorage，xml和yml的区别只是内容嵌在的文件格式不同
		- FileStorage对于xml和yml的用法相同，只不过由于xml yml格式不同而同样的使用结果不同，下图为同样的输入内容和输入方式，结果的差异
	- xml +FileStorage
		编写方式，如下：
		<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\FileStorage+xml.PNG" alt="xml +FileStorage " style="zoom:60%; float:center;" />
		显示结果，如下：
		<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\xml显示结果.PNG" alt="显示结果" style="zoom:75%; float:center" />
	- yml + FileStorage
		code编写方式，如下：
		<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\FileStorage+yml.PNG" alt="yml + FileStorage" style="zoom:60%; float:center;" />
		显示结果，如下：
		<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\yml显示结果.PNG" alt="显示结果" style="zoom:75%; float:center;" />
	2. FileStorage FileNode FileNodeIterator一块使用
	<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\FileStorage+FileNode+FileNodeIterator.PNG" style="zoom:60%;" />
	3. 使用 "[" " ]"  "{" "}"来读写xml  yml


2. 遍历文件夹的函数
	1. 遍历文件夹下的all文件：
		- cv::glob()
	2. 遍历文件夹下的all指定后缀的文件：
	3. 遍历文件夹下的all子目录


3. cv::Size


4. 第一次赋值，第二次与第一次的进行比较的精妙写法
	<img src="C:\Users\king-kong\Desktop\要做的事情\picture\Opencv\第一次赋值-第二次与第一次比较.PNG" style="zoom:60%;" />


5. cornersMat(
6. resize(
7. cvtColor(

- cvRound()
- remap()

6. rotationMatrixToEulerAngles（）
7. stereoCalibrate()   +  findChessboardCorners()  +  drawChessboardCorners( 使用这一套来标定的



- cornerSubPix()和drawChessboardCorners()有什么用？？注释掉和不注释掉感觉没什么差别啊
	cornerSubPix()对检测到的角点作进一步的优化计算，可使角点的精度达到亚像素级别
```c++
 void cv::cornerSubPix(
        cv::InputArray image, // 输入图像
        cv::InputOutputArray corners, // 角点（既作为输入也作为输出）
        cv::Size winSize, // 区域大小为 NXN; N=(winSize*2+1)
        cv::Size zeroZone, // 类似于winSize，但是总具有较小的范围，Size(-1,-1)表示忽略
        cv::TermCriteria criteria 
     /*用于表示计算亚像素时停止迭代的标准，可选的值有cv::TermCriteria::MAX_ITER 、cv::TermCriteria::EPS（可以是两者其一，或两者均选），前者表示迭代次数达到了最大次数时停止，后者表示角点位置变化的最小值已经达到最小时停止迭代。二者均使用cv::TermCriteria()构造函数进行指定。
         //指定亚像素计算迭代标注，一般常用如下：
    cv::TermCriteria criteria = cv::TermCriteria(
                    cv::TermCriteria::MAX_ITER + cv::TermCriteria::EPS,
                    40,
                    0.01);
     */
     
    );
```

- 几种不同的检测角点的函数：有的要求输入img为gray，有的没有要求
	1. cv::goodFeaturesToTrack()提取到的角点只能达到像素级别，在很多情况下并不能满足实际的需求，这时，我们则需要使用cv::cornerSubPix()对检测到的角点作进一步的优化计算，可使角点的精度达到__亚像素级别__
		- 亚像素精度是什么
		- 亚像素&&超分辨
		
	2. 只是想检测棋盘格的角点的话可以使用专门的findChessboardCorners + cv::cornerSubPix()提升到亚像素 + drawChessboardCorners() 可以参考opencv的源码,棋盘格的检测是角点检测之后加上特定的筛选,选出棋盘格角点



- Mat类的常用方法
	1. 构造时：
		1. imread()
			- cv::Mat image_color = cv::imread("image.jpg", cv::IMREAD_COLOR);
		2. .clone()
			-  cv::Mat image_copy = image_color.clone();
		3. .empty()


- opencv常用裸方法：
	1. cvtColor()
		- cv::Mat image_gray; 
		- cv::cvtColor(image_color, image_gray, cv::COLOR_BGR2GRAY);
	2. cv::circle()：可用于一个Point2f型点绘制与图片(Mat型)上
		- cv::circle(image_color, corners[i], 5, cv::Scalar(0, 0, 255), 2, 8, 0);
	3. cv::namedWindow()
		- namedWindow("窗口名", WINDOW_NORMAL);
		- namedWindow("窗口名", WINDOW_FULLSCREEN); //会以最小的边进行自适应扩展来全覆盖，会导致长的边超出屏幕
	3. cv::imread()
	4. cv::imwrite()
	5. cv::imshow()
		- imshow("窗口名", img);，要与namedWindow()配合使用
	6. cv::waitKey(5);
	7. cv::resize(); 对原Mat图像进行缩放
		1. 绝对像素缩放
			- Mat img = imread("lol5.jpg");
			- Mat dst = Mat::zeros(512, 512, CV_8UC3); //我要转化为512 * 512大小的
			- resize(img, dst, dst.size());
		2. 相对缩放
			- Mat img = imread("lol5.jpg");
			- Mat dst;
			- resize(img, dst, Size(),0.5,0.5);//我长宽都变为原来的0.5倍
	8. cv::threshold();用于图像的按阙值二值化。此方法只适用于单通道图像。一般步骤：1.将彩色图 -> 灰度图 -> 二值图
		- cv::Mat image_bit;
		- auto temp = cv::threshold(image_gray, image_bit, 100, 255, cv::THRESH_BINARY_INV);
		- ![]()



----
__上述方法的实际使用组合实例__:

----
1. cv::goodFeaturesToTrack() + cv::cornerSubPix()角点检测示例:
```c++
	cv::Mat image_color = cv::imread("image.jpg", cv::IMREAD_COLOR);
 
    //用于绘制亚像素角点
    cv::Mat image_copy = image_color.clone();
    //使用灰度图像进行角点检测
    cv::Mat image_gray;
    cv::cvtColor(image_color, image_gray, cv::COLOR_BGR2GRAY);
 
    //设置角点检测参数
    std::vector<cv::Point2f> corners;
    int max_corners = 100;
    double quality_level = 0.01;
    double min_distance = 10;
    int block_size = 3;
    bool use_harris = false;
    double k = 0.04;
 
    //角点检测
    cv::goodFeaturesToTrack(image_gray,
        corners,
        max_corners,
        quality_level,
        min_distance,
        cv::Mat(),
        block_size,
        use_harris,
        k);
 
    //将检测到的角点绘制到原图上
    for (int i = 0; i < corners.size(); i++)
    {
        cv::circle(image_color, corners[i], 5, cv::Scalar(0, 0, 255), 2, 8, 0);
    }
 
    //指定亚像素计算迭代标注
    cv::TermCriteria criteria = cv::TermCriteria(
                    cv::TermCriteria::MAX_ITER + cv::TermCriteria::EPS,
                    40,
                    0.01);
 
    //亚像素检测
    cv::cornerSubPix(image_gray, corners, cv::Size(5, 5), cv::Size(-1, -1), criteria);
 
    //将检测到的亚像素角点绘制到原图上
    for (int i = 0; i < corners.size(); i++)
    {
        cv::circle(image_copy, corners[i], 5, cv::Scalar(0, 255, 0), 2, 8, 0);
    }
 
    cv::imshow("corner", image_color);
    cv::imshow("sub pixel corner", image_copy);
 
    cv::imwrite("corner.jpg", image_color);
    cv::imwrite("corner_sub.jpg", image_copy);
    cv::waitKey(0);
    return;
```




# 疑问
1. why 分别进行两次不同sacle的运算？？？？
	sacle == 1 如果能找到棋盘格角点，直接就退出了，只有找不到时才会进行scale == 2 再找一次


# bug
1. findChessboardCorners获取棋盘格角点函数返回值一直是0。图片拍得如下，挺清晰的。bordersize设置也合理。
	- 问题解决：棋盘格最外围的黑边影响了检测。why黑边会影响检测？？？
		1. 将bordersize去除最外围的两边
		2. 对彩色图黑白反转。