[toc]



# C++代码编译为DLL的写作要求


方法使用_declspec(dllexport)修饰符

1. 但是为什么 全局变量不需要特殊的修饰，就可以在别的地方随意使用？？
2. 而且_declspec(dllexport)修饰的方法，也可以所以调用别的_declspec(dllexport)修饰的方法，



	_declspec(dllexport) void closeAllKinect()
		{
			//closeAzureKinect();
			//closeAzureKinect2();
			//closeAzureKinect3();

